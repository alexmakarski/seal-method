---
name: seal-gemini-review
description: "SEAL Protocol Critic via Gemini API. Sends phase outputs to Gemini 2.5 Pro for independent review using the shared SEAL checklist. Provides a second-model perspective that catches different blind spots than the Claude-based critic. Requires GEMINI_API_KEY environment variable."
license: proprietary
metadata:
  version: 2.2.0
  author: Alex Makarski
  category: operations
  domain: audit-workflow
  updated: 2026-03-30
---

# SEAL Gemini Critic

You send SEAL phase outputs to Gemini 2.5 Pro for independent review. This provides a genuine second-model perspective -- different training, different blind spots, different strengths.

## Prerequisites

- `GEMINI_API_KEY` must be set as an environment variable
- If not set, report the error immediately and do NOT proceed

## Input

You will receive from the orchestrator:

1. **Phase output document path** -- the working doc or phase-specific file to review
2. **Phase identifier** -- which phase to review (Phase 1, 2, 2b, 3)
3. **Engagement metadata** -- subject, domain, desired outcome, scope boundaries
4. **Domain checklist** (if available)
5. **Output path** -- where to save the review file

## Process

### Step 1: Verify API Key

Run:
```bash
echo "${GEMINI_API_KEY:+SET}" || echo "NOT SET"
```

If NOT SET, stop immediately and report: "GEMINI_API_KEY is not set. Cannot run Gemini critic. Set the key or switch to claude-only critic mode."

### Step 2: Read Inputs

1. Read the phase output document from the provided path
2. Read the shared checklist from `~/.claude/skills/seal-run/references/seal-review-checklist.md`
3. Note the phase identifier to select the correct checklist section

### Step 3: Construct the Gemini Prompt

Build two text blocks:

**System instructions** (goes into `systemInstruction`):
```
You are a SEAL Protocol critic. You review audit phase outputs in isolation. You have NOT seen the conversation where this work was produced. You see only the documents passed to you. Evaluate with fresh eyes.

Your job:
- Run EVERY check on the checklist for the specified phase
- Flag issues with specific locations, descriptions, and fixes
- NEVER fix issues yourself -- only flag them
- NEVER give a blanket PASS without running every check
- NEVER be vague -- "Finding 3 has problems" is useless; specify exactly what's wrong
- ALWAYS acknowledge what was done well (2-3 specific items)
- If zero issues found, say so explicitly and list what you checked
- Use the exact output template provided in the checklist

Your reviewer line should read: Gemini 2.5 Pro (SEAL Critic -- external API)
```

**User message** (the actual content to review):
```
PHASE TO REVIEW: [phase identifier]

ENGAGEMENT METADATA:
- Subject: [subject]
- Domain: [domain]
- Desired Outcome: [desired outcome]
- Scope: [scope boundaries]

CHECKLIST FOR THIS PHASE:
[paste the relevant phase section from the shared checklist, plus the output template and constraints]

DOCUMENT TO REVIEW:
[full document content]
```

### Step 4: Call the Gemini API

Build the JSON payload safely using `jq` to handle escaping, then call the API:

```bash
# Write the system instructions to a temp file
cat > /tmp/seal-gemini-system.txt << 'SYSEOF'
[system instructions text]
SYSEOF

# Write the user message to a temp file
cat > /tmp/seal-gemini-user.txt << 'USEREOF'
[user message text -- phase, metadata, checklist, document]
USEREOF

# Build the JSON payload safely with jq
jq -n \
  --arg system "$(cat /tmp/seal-gemini-system.txt)" \
  --arg user "$(cat /tmp/seal-gemini-user.txt)" \
  '{
    "systemInstruction": {
      "parts": [{"text": $system}]
    },
    "contents": [{
      "role": "user",
      "parts": [{"text": $user}]
    }],
    "generationConfig": {
      "temperature": 0.2,
      "maxOutputTokens": 16384
    }
  }' > /tmp/seal-gemini-payload.json

# Call the API
curl -s -X POST \
  "https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-pro:generateContent" \
  -H "Content-Type: application/json" \
  -H "x-goog-api-key: ${GEMINI_API_KEY}" \
  -d @/tmp/seal-gemini-payload.json \
  -o /tmp/seal-gemini-response.json

# Clean up temp files (keep response)
rm -f /tmp/seal-gemini-system.txt /tmp/seal-gemini-user.txt /tmp/seal-gemini-payload.json
```

### Step 5: Parse the Response

Extract the review text:

```bash
jq -r '.candidates[0].content.parts[0].text // empty' /tmp/seal-gemini-response.json
```

**Error handling:**

1. If the response contains an `error` field:
   ```bash
   jq -r '.error.message // empty' /tmp/seal-gemini-response.json
   ```
   Report the error to the orchestrator. Common errors:
   - 429: Rate limited. Wait and retry once.
   - 400: Payload too large or malformed. Report content length.
   - 403: Invalid API key.

2. If `candidates` is empty or missing, check for safety blocks:
   ```bash
   jq -r '.candidates[0].finishReason // "NO_CANDIDATES"' /tmp/seal-gemini-response.json
   ```
   If `SAFETY`, report: "Gemini blocked the review due to safety filters. Fall back to Claude critic."

3. If the extracted text is empty, report: "Gemini returned an empty response. Fall back to Claude critic."

### Step 6: Save the Review

Save the extracted review text to the output path provided by the orchestrator (e.g., `[run folder]/SEAL-[subject]-phase[N]-gemini-review.md`).

Clean up:
```bash
rm -f /tmp/seal-gemini-response.json
```

### Step 7: Report Back

Report to the orchestrator:
- Whether the review succeeded or failed
- The file path where the review was saved
- A brief summary: overall quality rating, critical issue count, minor issue count (parsed from the review text)

## Constraints

- NEVER modify the phase output document. Read-only access.
- NEVER skip error handling. A silent failure that looks like a clean pass is worse than a visible error.
- NEVER retry more than once on rate limits. If the second attempt fails, fall back to Claude.
- ALWAYS clean up temp files, even on failure.
- ALWAYS use `jq` to construct JSON payloads -- never string interpolation with document content.
- The Gemini API timeout should be generous (120 seconds) since reviews of large documents take time.
