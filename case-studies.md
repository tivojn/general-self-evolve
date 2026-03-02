# Self-Evolve Case Studies

Real-world examples from self-evolve sessions. Referenced from SKILL.md learned patterns.

---

## Case Study 1: 83 Rounds of Green Tests, 5 Critical Bugs

**Project:** CLI tool bridging an AI agent app to Telegram/Discord
**Symptoms:** 560+ unit tests passing, zero lint warnings, zero type errors. Agents hallucinating, delegation broken, files silently dropped.

### Bugs Found Only by Live Testing

1. **Shared session IDs** — All delegated agents shared one session (`-team`), causing Agent B to read Agent A's conversation history. The LLM mimicked Agent A's personality. Unit tests mocked each call independently so the shared state was invisible.

2. **Truncated delegation context** — Only the next sentence (max 200 chars) after an @mention was forwarded. The full user question was lost. Unit test verified "message < 200 chars" and passed — testing what was written, not what should have been written.

3. **Silent delegation failures** — When a delegated agent call failed, the user saw nothing. Unit test checked "returns null on error" — correct behavior at the function level, but nobody tested the user experience.

4. **Config passthrough gaps** — API options (url, timeout) were correctly passed to the primary call but silently dropped during delegation. Mocks didn't check whether options propagated.

5. **Internal content leakage** — Chain-of-thought `thinking` items were passed through to users. Never appeared in test fixtures because the developer didn't know the API returned them.

### Key Takeaway

Mocks test your assumptions about the system. Live tests test the actual system. 83 rounds of "improving" a codebase with only unit tests created a perfectly-formatted, thoroughly-tested codebase that was fundamentally broken.

---

## Case Study 2: The Misdiagnosis Trap

**Problem:** Agents couldn't generate selfie images via delegation.
**First diagnosis:** Agents missing `image_generation` tools in preference config.
**Action:** Added tools AND fixed the response parser simultaneously.
**Result:** It worked.
**Truth:** The agents already had `code_runner|bash` which calls nanobanana for image generation. The tools were unnecessary — the parser fix was the real solution. Had to roll back the tool changes.

### The Pattern

When you change two things and the bug goes away, you don't know which fix mattered. Always:
1. Check raw API response FIRST to see what the system actually returned
2. Change one thing at a time
3. Verify your diagnosis independently before acting on it

---

## Case Study 3: Think Bigger — Three Narrow Fixes That Should Have Been One

**Round 1:** Added `.pptx` and `.xlsx` to a file extension whitelist. User asked "what about audio? video?" The whitelist approach was wrong — should have inverted the logic to exclude code/config files instead.

**Round 2:** Extracted only `image_url` from `flowResults`. User asked "what about pptx/docx?" Had to add `text` type extraction too. Should have extracted ALL content types from the start.

**Round 3:** Skipped `flowParams` scanning when `flowResults` had images. A directory path still got through and crashed delivery. Had to add `isFile()` check. `existsSync` returns true for directories — should have been obvious.

### The Pattern

Every narrow fix required a follow-up fix for the next type/scenario. The generalized fix (exclude-list instead of allow-list, extract all content types, validate file vs directory) would have covered all cases in one pass.

---

## Case Study 4: Stale Sessions Cause Ghost Bugs

**Problem:** Team standards file was updated (color bans removed). Agent confirmed the update. But when asked "can you use emerald green?", agent still refused.

**Root cause:** The running agent's LLM context had the old rules cached from the session. The file on disk changed, but the agent's conversation memory still contained the old rules.

**Same pattern, different symptom:** Agent confused a docx request with a prior pptx conversation because the session carried stale context. Using `--reset` (new session ID) fixed it instantly.

### The Pattern

Config/knowledge-base changes don't propagate to running agent sessions. After any config change:
1. Sync preference files (`agents sync`)
2. Force new sessions (`--reset`)
3. Explicitly tell agents to re-read their workspace files
4. Retest with the specific scenario that was broken

---

## Case Study 5: "All Good" Was Never True

Timeline of a single session where every "done" report was premature:

| Agent Says | User Pushes | What Was Actually Found |
|---|---|---|
| "5 bugs fixed, tests pass" | "Prove it — do live tests" | Had never run a single live test |
| "19/20 live tests pass" | "Test for hallucination with multiple rounds" | Didn't test identity persistence |
| "12/12 identity rounds pass, zero hallucination" | "Ask Mavis to delegate selfie to Elena" | `channels send` had no delegation support at all |
| "Delegation works, Elena responded" | "She only sent her portrait, not a new selfie" | Response parser wasn't extracting generated files |
| "Fixed parser, Elena generates selfies" | "What about pptx, docx, audio?" | Missing file extensions in whitelist |
| "Added extensions" | "Think bigger — what about ALL file types?" | Whitelist approach was wrong, needed exclude-list |
| "Fixed for all types" | "Why is Discord still showing portrait?" | Services running stale mirror code, never redeployed |
| "Redeployed, Discord fixed" | "Vivienne pptx timed out on Discord" | Default timeout too short for long operations |

8 rounds of "done" → push → find more. The agent's instinct to summarize and stop was wrong every time. The user's instinct to test harder was right every time.

---

## Case Study 6: The Parser Is the Bottleneck, Not the Agent

In one session, every "agent can't do X" turned out to be "agent DID do X, parser dropped the result":

| What User Saw | What Actually Happened |
|---|---|
| Agent sent portrait instead of selfie | Agent generated new image in `flowResults.image_url` — parser only checked `flowParams` and `text` |
| Agent didn't send pptx | Agent generated pptx — `.pptx` wasn't in the extension whitelist |
| Agent didn't send audio | Agent generated audio — `.m4a`/`.ogg` weren't in the extension whitelist |
| Portrait file leaked alongside selfie | Parser treated input reference files in `flowParams` as output deliverables |

### The Pattern

When an agent "can't" produce something, `curl` the API directly and read the raw JSON response before blaming the agent. The agent almost certainly produced it — your parsing/delivery code dropped it.
