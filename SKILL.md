---
name: general-self-evolve
description: "Point at any repo. Evaluate, plan, bootstrap credentials, then autonomously improve it. Works with any tech stack — code quality, tests, CI/CD, docs, deps, and more."
version: 1.4.0
author: community
category: automation
---

# General Self-Evolve Skill

> **North Star:** The user points this skill at a repo and walks away. The skill improves the project AND improves itself — autonomously, non-stop, no human in the loop. Every run makes the next run smarter, faster, and more capable. The goal is full autonomy: evaluate → fix → live test → learn → evolve the skill → repeat.

Turn any repository into a self-improving project. Evaluate it, gather what's needed from the user (tokens, logins, cookies), store config, then autonomously execute improvements.

**Trigger on:** "self-evolve", "self-evolve this repo", "evolve this project", "bootstrap self-evolution", "auto-improve", "general-self-evolve", "evaluate and improve", "make this project self-evolving", "keep going", "keep evolving", "self-evolve forever", "evolve for 2 hours", "self-improving", "autonomous agent", "heartbeat system", "pattern crystallization", "foundry", "ralph loop", "recursive self-improvement", "agent that builds agents", "self-writing code"

---

## How It Works — The Dual Loop

Two loops running simultaneously. The inner loop improves the PROJECT. The outer loop improves THIS SKILL.

```
┌─────────────────────────────────────────────────────┐
│  OUTER LOOP: Skill Self-Evolution                   │
│  Every run updates SKILL.md + case-studies.md        │
│  Next run inherits all lessons from previous runs    │
│                                                     │
│  ┌─────────────────────────────────────────────┐    │
│  │  INNER LOOP: Project Improvement             │    │
│  │  1. EVALUATE   → Scan repo, find gaps        │    │
│  │  2. NEEDS      → Gather credentials          │    │
│  │  3. BOOTSTRAP  → Set up .self-evolve/        │    │
│  │  4. EXECUTE    → Fix, build, test, commit    │    │
│  │  5. LIVE TEST  → Test against real infra     │    │
│  │  6. LEARN      → Track outcomes              │    │
│  │  7. NON-STOP   → Keep going autonomously     │    │
│  │  8. PARITY     → (Optional) Mirror CLI       │    │
│  └──────────────────────────┬──────────────────┘    │
│                             │                       │
│  9. META-EVOLVE ← lessons ──┘                       │
│     Update SKILL.md with generalized patterns       │
│     Update case-studies.md with real examples        │
│     Next session starts smarter                     │
└─────────────────────────────────────────────────────┘
```

**The goal:** Run 1 needs human guidance. Run 10 needs a nudge. Run 50 runs unattended. Each run compounds — more patterns, fewer blind spots, better testing instincts.

**Files:**
- `SKILL.md` — Generalized rules and heuristics (this file)
- `case-studies.md` — Real examples with full context (referenced from SKILL.md)

---

## Phase 1: EVALUATE

Scan the repo comprehensively. Run these checks:

### 1.1 Tech Stack Detection

```bash
# Detect languages, frameworks, package managers
ls -la                                    # root structure
cat package.json 2>/dev/null              # Node.js
cat requirements.txt pyproject.toml setup.py 2>/dev/null  # Python
cat Cargo.toml 2>/dev/null                # Rust
cat go.mod 2>/dev/null                    # Go
cat Gemfile 2>/dev/null                   # Ruby
cat pom.xml build.gradle 2>/dev/null      # Java
cat Makefile CMakeLists.txt 2>/dev/null   # C/C++
```

### 1.2 Infrastructure Detection

```bash
# CI/CD
ls .github/workflows/ 2>/dev/null         # GitHub Actions
cat .gitlab-ci.yml 2>/dev/null            # GitLab CI
cat Jenkinsfile 2>/dev/null               # Jenkins
cat .circleci/config.yml 2>/dev/null      # CircleCI

# Containers
cat Dockerfile docker-compose.yml 2>/dev/null

# Config / Env
cat .env.example .env.template 2>/dev/null
cat .envrc 2>/dev/null                    # direnv

# Linting / Formatting
cat .eslintrc* .prettierrc* .editorconfig 2>/dev/null
cat .flake8 .pylintrc .ruff.toml 2>/dev/null
cat .rubocop.yml 2>/dev/null
```

### 1.3 Quality Assessment

Check for the presence and quality of:

| Area | What to Check | Status Values |
|---|---|---|
| **Tests** | Test directory, test files, coverage config | none / partial / good |
| **CI/CD** | Workflow files, build scripts | none / basic / comprehensive |
| **Docs** | README quality, API docs, inline comments | none / minimal / good |
| **Linting** | Linter config, formatter config | none / configured / enforced |
| **Types** | TypeScript, type hints, type checking | none / partial / strict |
| **Security** | Dependency audit, secret scanning | none / basic / hardened |
| **Dependencies** | Lock files, outdated deps, vulnerabilities | stale / current / managed |
| **Git Hygiene** | Branch protection, commit conventions, hooks | loose / conventional / strict |
| **Error Handling** | Try/catch patterns, logging, monitoring | minimal / adequate / robust |
| **Performance** | Caching, profiling, benchmarks | unknown / measured / optimized |

### 1.4 External Dependencies Detection

Scan for services the project depends on:

```bash
# Scan for API keys, service references, URLs
grep -r "API_KEY\|SECRET\|TOKEN\|PASSWORD\|CREDENTIALS" --include="*.env*" --include="*.yml" --include="*.json" --include="*.toml" -l .
grep -r "amazonaws.com\|googleapis.com\|api.openai\|api.anthropic\|api.stripe\|twilio\|sendgrid\|firebase\|supabase" -l .
grep -r "redis://\|mongodb://\|postgres://\|mysql://\|amqp://" -l .
```

### 1.5 Generate Evaluation Report

Save to `.self-evolve/evaluation.md`:

```markdown
# Project Evaluation
**Date:** YYYY-MM-DD
**Repo:** /path/to/repo
**Tech Stack:** [detected]
**LOC:** ~X,XXX (src/)

## Scores
| Area | Score | Notes |
|---|---|---|
| Tests | partial | Jest configured, 23% coverage |
| CI/CD | basic | GitHub Actions, build only |
| ... | ... | ... |

## Top Opportunities (prioritized)
1. [HIGH] Add test coverage — currently 23%, target 60%
2. [HIGH] Add linting — no eslint config found
3. [MED] Update dependencies — 12 outdated packages
4. [MED] Add pre-commit hooks — no husky/lint-staged
5. [LOW] Add API documentation — endpoints undocumented

## External Dependencies
- OpenAI API (found in src/ai.ts)
- PostgreSQL (found in docker-compose.yml)
- Stripe (found in src/billing/)

## Credential Requirements
See Phase 2 output.
```

---

## Phase 2: NEEDS

After evaluation, generate a clear checklist of what's needed from the user.

### 2.1 Credential Types

| Type | Example | How to Collect |
|---|---|---|
| **API Key** | OpenAI, Stripe, Anthropic | User pastes key |
| **OAuth Token** | GitHub, Google, Slack | User logs in via browser, skill saves token |
| **Bot Token** | Telegram, Discord | User creates bot, pastes token |
| **Cookie** | Twitter/X, services without API | User logs in browser, skill extracts cookies |
| **SSH Key** | Server access, Git deploy | User provides path or generates |
| **Database URL** | PostgreSQL, MongoDB, Redis | User provides connection string |
| **Service Account** | GCP, AWS | User provides JSON key or IAM credentials |

### 2.2 Generate Needs Checklist

Save to `.self-evolve/needs.md`:

```markdown
# What I Need From You

## Required (blocking)
- [ ] `GITHUB_TOKEN` — GitHub PAT with repo/workflow scope (for creating PRs, managing CI)
      → Create at: https://github.com/settings/tokens/new
      → Scopes needed: repo, workflow
- [ ] `OPENAI_API_KEY` — Found references in src/ai.ts
      → Get from: https://platform.openai.com/api-keys

## Required (one-time manual action)
- [ ] **Browser login to X/Twitter** — Need cookies for bird CLI
      → I'll extract cookies after you log in via Chrome
- [ ] **OAuth login to Google** — For Gmail/Calendar access
      → Run: `gog auth login`

## Optional (enhances capabilities)
- [ ] `TELEGRAM_BOT_TOKEN` — For sending notifications about improvements
      → Create via @BotFather on Telegram
- [ ] `SENTRY_DSN` — For error monitoring
      → Get from: https://sentry.io/settings/projects/
```

### 2.3 Interactive Collection

When the user provides credentials, store them immediately:

```bash
# User provides a token
echo "GITHUB_TOKEN=ghp_xxxxxxxxxxxx" >> .self-evolve/.env

# After browser login, extract cookies
# (example: using bird for Twitter)
bird check  # verify cookie extraction works

# Mark as collected in needs.md
# Update checkbox: - [x] `GITHUB_TOKEN` — collected ✓
```

**IMPORTANT:** Never echo/log/display credential values. Only confirm "collected" or "failed".

---

## Phase 3: BOOTSTRAP

Set up the self-evolution infrastructure in the repo.

### 3.1 Directory Structure

```
.self-evolve/
├── .env                    # Credentials (MUST be in .gitignore)
├── config.json             # Skill settings and preferences
├── evaluation.md           # Phase 1 output
├── needs.md                # Phase 2 output
├── plan.md                 # Prioritized improvement plan
├── log.md                  # Execution history
├── patterns.json           # Learned patterns and outcomes
└── scripts/                # Generated automation scripts
    ├── check-deps.sh       # Dependency update checker
    ├── run-tests.sh        # Test runner with coverage
    └── lint-fix.sh         # Auto-fix linting issues
```

### 3.2 Config File

`.self-evolve/config.json`:

```json
{
  "version": "1.0.0",
  "repo": "/path/to/repo",
  "techStack": {
    "language": "typescript",
    "framework": "next.js",
    "packageManager": "pnpm",
    "testFramework": "jest",
    "linter": "eslint"
  },
  "evolution": {
    "mode": "autonomous",
    "commitStyle": "conventional",
    "branchStrategy": "feature-branches",
    "maxChangesPerRun": 5,
    "requireTests": true,
    "autoCommit": true,
    "autoPush": true,
    "createPRs": false
  },
  "runtime": {
    "duration": "1h",
    "mode": "nonstop",
    "selfAnswer": true,
    "commitInterval": "per-task",
    "pushInterval": "per-task",
    "maxConsecutiveFailures": 3
  },
  "credentials": {
    "collected": ["GITHUB_TOKEN", "OPENAI_API_KEY"],
    "pending": ["TELEGRAM_BOT_TOKEN"],
    "manual": ["twitter_cookies"]
  },
  "schedule": {
    "frequency": "daily",
    "activeHours": {"start": "08:00", "end": "22:00"}
  }
}
```

### 3.3 Gitignore Update

```bash
# Ensure .env is never committed
echo ".self-evolve/.env" >> .gitignore
echo ".self-evolve/patterns.json" >> .gitignore
```

### 3.4 Generate Plan

`.self-evolve/plan.md` — prioritized, actionable:

```markdown
# Evolution Plan
**Generated:** YYYY-MM-DD
**Status:** active

## Queue (ordered by priority)

### 1. [READY] Add ESLint + Prettier
- **Risk:** low
- **Files:** package.json, .eslintrc.js, .prettierrc
- **Steps:** Install deps → create configs → run fix → commit
- **Validation:** `npx eslint . --max-warnings 0`
- **Depends on:** nothing

### 2. [READY] Add test coverage to src/utils/
- **Risk:** low
- **Files:** src/utils/*.ts, src/utils/__tests__/*.test.ts
- **Steps:** Create test files → write tests → verify coverage
- **Validation:** `npm test -- --coverage --threshold 60`
- **Depends on:** nothing

### 3. [BLOCKED] Set up GitHub Actions CI
- **Risk:** medium
- **Files:** .github/workflows/ci.yml
- **Steps:** Create workflow → test locally with act → push
- **Validation:** Workflow runs green on push
- **Depends on:** GITHUB_TOKEN

### 4. [READY] Update outdated dependencies
- **Risk:** medium
- **Files:** package.json, pnpm-lock.yaml
- **Steps:** Run audit → update non-breaking → run tests → commit
- **Validation:** `pnpm audit` clean, all tests pass

## Completed
(none yet)

## Skipped
(none yet)
```

---

## Phase 4: EXECUTE

The autonomous improvement loop. For each task in the plan:

### 4.1 Execution Cycle

```
For each issue or task:
  1. FIND      — Identify the issue (from plan, live test, or code review)
  2. REASON    — Understand root cause. Check raw data before assuming.
  3. FIX       — Change ONE thing. Not two. One.
  4. REVIEW    — Read the diff. Does it make sense? Is it generalized?
  5. RETEST    — Run the SAME test that found the bug. Then run related tests.
  6. VERIFIED? — If not, go back to step 2. If yes, continue.
  7. COMMIT    — Conventional commit with clear description of what and why.
  8. PUSH      — Immediately. Don't batch. Each fix = one commit + one push.
  9. DEPLOY    — If services run from mirrors/containers, redeploy now.
  10. LEARN    — If the fix taught a generalized lesson, update THIS SKILL.
  11. NEXT     — Move to next issue immediately.
```

### 4.2 Execution Rules

**ALWAYS:**
- Create a new branch for each improvement (never commit directly to main)
- Run existing tests before AND after changes
- Use conventional commits: `feat:`, `fix:`, `chore:`, `docs:`, `test:`, `ci:`
- Log every action with timestamp and outcome
- Stop immediately if tests break and revert
- Commit and push after every verified fix (never batch — each fix = commit + push immediately)
- Self-answer questions using best-effort reasoning (see Phase 6.3)
- Keep going without pausing — move to next task immediately

**NEVER:**
- Push to main/master directly
- Delete or overwrite user code without backup
- Modify .env files that aren't in .self-evolve/
- Make changes outside the repo directory
- Spend more than 10 minutes on a single task before reassessing
- Wait for user input during autonomous execution
- Continue if 3+ consecutive tasks fail (stop and generate end-of-run report)

### 4.3 Validation Matrix

| Change Type | Validation Steps |
|---|---|
| Dependencies | `install` → `build` → `test` → `audit` |
| Linting/Format | `lint --fix` → `build` → `test` |
| Tests | `test` → `coverage check` |
| CI/CD | `act` (local) or dry-run → `build` → `test` |
| Docs | Markdown lint → link check |
| Refactor | `build` → `test` → `coverage diff` (must not decrease) |
| New Feature | `build` → `test` → manual review flag |

### 4.4 Commit Format

```
<type>(<scope>): <description>

<body with what changed and why>

Self-Evolved-By: general-self-evolve v1.2.0
```

### 4.5 Log Entry Format

Append to `.self-evolve/log.md`:

```markdown
## [2026-03-02 14:30] Round 3: Add ESLint + Prettier
- **Status:** success
- **Branch:** self-evolve/add-eslint
- **Changes:** 4 files added, 1 modified (+142 insertions)
- **Tests:** 47/47 passing (cumulative: 47 total)
- **Duration:** 3 min
- **Commit:** abc1234
```

**Cumulative test tracking:** Always log the TOTAL test count across the project, not just tests for the current task. This creates a trajectory (e.g., `0 → 38 → 50 → 72 → 91 → 125`) that shows project health growth over time.

---

## Phase 5: LIVE TEST (MANDATORY)

**Unit tests passing does NOT mean the software works.** This phase is non-negotiable. After every batch of code changes (every 5 rounds, or after fixing core bugs), test the actual running system against real infrastructure.

### The Lesson That Created This Phase

A project passed 83 rounds of self-evolution — 560+ unit tests, zero lint warnings, zero type errors. The codebase looked perfect. But it had **5 critical functional bugs** invisible to unit tests: shared state causing identity bleed, truncated context, silently dropped config, invisible failures, and internal content leaking to users. All 560 unit tests passed. The system was broken. **Mocks hide real bugs.**

See `case-studies.md` (Case Study 1) for the full breakdown.

### 5.1 When to Run Live Tests

| Trigger | Action |
|---|---|
| After fixing core logic bugs | Run immediately — don't wait for batch |
| Every 5 rounds of code changes | Mandatory live test sweep |
| After any delegation/routing change | Test the full delegation chain |
| After API client changes | Test against real API |
| After service lifecycle changes | Test deploy/start/stop cycle |
| Before declaring "maturity plateau" | MUST pass live tests first |

### 5.2 Live Test Tiers

#### Tier 1: CLI Smoke Tests (always possible)

Run every CLI command and verify it doesn't crash:

```bash
# Config commands
app config get key
app config set key value
app config unset key

# Status/health commands
app status
app doctor
app health
app info
app version

# List commands
app agents list
app channels list
app channels status
```

**Pass criteria:** Every command exits 0, produces expected output format.

#### Tier 2: Integration Tests (requires running services)

Test actual data flow through the system:

```bash
# Send a message through the system
app channels send --channel telegram --name botname --message "Test from CLI"

# Verify in the target service (Telegram, Discord, Slack, etc.)
# - Message arrived?
# - Formatting correct?
# - Response received?
```

**Pass criteria:** Messages arrive at destination, responses flow back.

#### Tier 3: E2E Feature Tests (requires Playwright or equivalent)

Test complex multi-step features through the actual UI:

```
1. Open the service's web interface (Telegram Web, Discord, etc.)
2. Send a message that triggers delegation: "@Agent1 ask @Agent2 about X"
3. Verify:
   - Agent1 receives the message
   - Agent1 correctly delegates to Agent2
   - Agent2 responds with its own personality (not Agent1's)
   - The response reaches the user
   - No chain-of-thought or internal content leaked
```

**Pass criteria:** Full feature works end-to-end as a user would experience it.

### 5.3 Live Test Checklist Template

Save to `.self-evolve/live-test-results.md`:

```markdown
# Live Test Results
**Date:** YYYY-MM-DD
**Round:** N (after rounds X-Y of changes)

## Tier 1: CLI Smoke Tests
| Command | Status | Notes |
|---|---|---|
| `app status` | PASS/FAIL | |
| `app doctor` | PASS/FAIL | |
| ... | | |

## Tier 2: Integration Tests
| Test | Status | Notes |
|---|---|---|
| Send message via CLI | PASS/FAIL | |
| Receive response | PASS/FAIL | |
| ... | | |

## Tier 3: E2E Feature Tests
| Test | Status | Notes |
|---|---|---|
| Agent delegation A→B | PASS/FAIL | |
| Agent identity preserved | PASS/FAIL | |
| Error shown on failure | PASS/FAIL | |
| ... | | |

## Bugs Found
1. [BUG] Description → Fixed in commit abc1234
2. [BUG] Description → Created issue #N

## Verdict
PASS / FAIL (with count: X/Y tests passed)
```

### 5.4 Live Test Rules

**ALWAYS:**
- Run Tier 1 after every batch of changes (zero-cost, always possible)
- Run Tier 2 whenever services are available
- Run Tier 3 for any feature involving multi-component interaction
- Fix bugs found during live testing IMMEDIATELY (do not defer)
- Add a unit test for every live-test-discovered bug to prevent regression
- Log live test results in `.self-evolve/live-test-results.md`
- **RETEST after every fix** — do not assume a fix works. Run the same live test again.
- **Keep looping** — test → find bug → fix → retest → find next bug → fix → retest until clean

**NEVER:**
- Declare a codebase "mature" or "at plateau" without passing live tests
- Skip live tests because unit tests pass — **unit tests test your mocks, not your system**
- Treat live test failures as low priority — they are the highest priority bugs
- Defer live testing to "later" — it's part of the evolution loop, not a separate activity
- **Stop after one round of live testing** — the first round ALWAYS finds bugs. Fix them and retest. The second round finds more. Keep going.
- **Report results and ask "want me to fix this?"** — just fix it. Non-stop. Don't ask permission to fix bugs you found.
- **Blame external systems without investigating** — if the feature doesn't work, dig deeper. Check configs, tool assignments, API responses, logs. The bug may be a missing config, not a code error.

### 5.5 Bug Discovery Protocol

When a live test finds a bug:

```
1. REPRODUCE  — Confirm the bug is real, not a test environment issue
2. RAW DATA   — Check the raw API/system response (curl, logs) before assuming what's broken
3. ROOT CAUSE — Read the actual production code path, trace the bug
4. GENERALIZE — Ask "what are ALL the cases this applies to?" Fix the general case, not just the symptom
5. ONE CHANGE — Change one thing at a time. Don't bundle fixes — you won't know which one worked
6. FIX        — Fix the code
7. UNIT TEST  — Add a unit test that would have caught this bug
8. RE-TEST    — Run the SAME live test again to confirm the fix
9. EXPAND     — Run RELATED live tests (other file types, other agents, other scenarios)
10. LOG       — Record in log.md: "[LIVE-TEST-BUG] description → fix → commit"
```

**Anti-patterns to avoid:**
- Fixing for `.pptx` without checking `.xlsx`, `.docx`, `.mp3`, `.m4a`, etc. — think ALL types
- Assuming the agent is broken when the parser dropped the output — check raw response first
- Changing config AND code simultaneously then declaring both necessary — isolate variables
- Reporting a diagnosis without verifying it independently — "missing tools" that weren't actually missing

### 5.6 Playwright E2E Patterns

For web-based verification (Telegram Web, Discord, etc.):

```
1. Load saved browser session (see 5.7 below)
2. Navigate to the web interface
3. Take a snapshot (accessibility tree, not screenshot)
4. Type a test message
5. Wait for response (with timeout)
6. Verify response content:
   - Correct agent responded
   - No identity confusion
   - No internal content leaked
   - Formatting correct
7. Take a post-response snapshot for evidence
```

### 5.7 Browser Session Injection for Automated Login

Playwright E2E tests require authenticated browser sessions. Store session state files (cookies + localStorage) and inject them before navigating.

**Session state files** are Playwright `storageState` JSON containing `cookies` and `origins` (localStorage). Store them at a known path (e.g., `~/.claude/telegram-session/state.json`).

**Injection pattern for MCP Playwright** (which doesn't support `storageState` natively):

1. **Cookies:** MCP Playwright preserves cookies across navigations within a session. If cookies alone aren't enough (e.g., Telegram Web uses localStorage for auth), use step 2.

2. **localStorage injection:** Navigate to the target domain first, then inject via `browser_evaluate`:
```javascript
// Inject localStorage entries from saved state
() => {
  const entries = [["token", '"value"'], ["auth_key", '"value"']];
  for (const [k, v] of entries) localStorage.setItem(k, v);
}
```
Then reload the page — the app reads auth from localStorage on load.

3. **Discord iframe trick:** Discord blocks `localStorage` on some pages. Use an iframe workaround:
```javascript
() => {
  const iframe = document.createElement('iframe');
  iframe.style.display = 'none';
  document.body.appendChild(iframe);
  iframe.contentWindow.localStorage.setItem('token', '"value"');
  document.body.removeChild(iframe);
}
```

**Session file locations** (check `~/.claude/` for saved sessions):
- `~/.claude/telegram-session/state.json` — Telegram Web auth
- `~/.claude/discord-session/state.json` — Discord Web auth
- Other services: save via `playwright codegen --save-storage` after manual login

**Important:** Session files contain auth tokens. Never commit them. Add to `.gitignore`.

---

## Phase 6: LEARN

Track patterns to get smarter over time.

### 5.1 Pattern Tracking

`.self-evolve/patterns.json`:

```json
{
  "patterns": [
    {
      "action": "add-eslint",
      "techStack": "typescript+next.js",
      "outcome": "success",
      "duration": 180,
      "filesChanged": 5,
      "testsAdded": 0,
      "timestamp": "2026-03-02T14:30:00Z"
    }
  ],
  "insights": {
    "successRate": 0.85,
    "avgDuration": 240,
    "mostCommonFailure": "dependency conflict",
    "totalImprovements": 12
  }
}
```

### 5.2 Adaptive Behavior

After every 5 completed tasks, reassess:
- Re-run Phase 1 evaluation (scores should improve)
- Compare before/after scores
- Adjust plan priorities based on what worked
- Generate a progress report for the user

### 5.3 Progress Report

```markdown
# Self-Evolution Progress Report
**Period:** 2026-03-01 to 2026-03-07

## Score Changes
| Area | Before | After | Delta |
|---|---|---|---|
| Tests | 23% coverage | 61% coverage | +38% |
| Linting | none | enforced | new |
| CI/CD | none | basic | new |
| Dependencies | 12 outdated | 2 outdated | -10 |

## Completed (7 tasks)
1. ✓ Add ESLint + Prettier
2. ✓ Add test coverage for utils/
3. ✓ Set up GitHub Actions CI
4. ✓ Update 10 outdated dependencies
5. ✓ Add pre-commit hooks
6. ✓ Add README badges
7. ✓ Add CONTRIBUTING.md

## Failed (1 task)
1. ✗ Migrate to TypeScript strict mode — 14 type errors remain

## Next Up
1. Add API documentation (OpenAPI spec)
2. Add error monitoring (Sentry integration)
3. Add performance benchmarks
```

---

## Quick Start

When the user triggers this skill with a repo:

```
1. cd /path/to/repo
2. Run Phase 1: EVALUATE
3. Present evaluation report to user
4. Run Phase 2: NEEDS — show what's needed
5. Collect credentials (if user provides them now) or proceed with what's available
6. Run Phase 3: BOOTSTRAP — set up .self-evolve/
7. Run Phase 7: NON-STOP MODE — start improving autonomously for 1 hour
8. Every 5 tasks: Phase 6 LEARN — log progress (don't stop to report)
9. MANDATORY after code changes: Phase 5 LIVE TEST — test against real infrastructure
10. At end of run: generate end-of-run report + Phase 9 META-EVOLVE
```

### Invocation Syntax

```bash
# Default: 1 hour non-stop
"Self-evolve /path/to/repo"

# Custom duration
"Self-evolve /path/to/repo for 30 minutes"
"Self-evolve /path/to/repo for 3h"

# Forever (until all tasks done or 3+ consecutive failures)
"Self-evolve /path/to/repo forever"

# Resume a previous run
"Keep going"                    # 1 hour default
"Keep going for 2 hours"        # custom duration
"Keep going forever"            # indefinite
```

Claude should:
1. `cd` to the repo
2. Run all Phase 1 checks in parallel
3. Generate evaluation.md
4. Show the user the top 5 opportunities and what credentials are needed
5. If credentials are needed, ask once — then **immediately proceed** with whatever tasks are unblocked
6. Bootstrap and enter non-stop autonomous mode (default 1 hour)
7. Do NOT wait for user input during execution — self-answer questions, commit+push continuously

---

## Improvement Categories

### Tier 1: Zero-Risk (auto-execute)
- Add/update .gitignore
- Add .editorconfig
- Fix markdown formatting
- Add LICENSE file
- Update README badges
- Remove unused imports (if linter confirms)

### Tier 2: Low-Risk (auto-execute with tests)
- Add linter configuration
- Add formatter configuration
- Add pre-commit hooks
- Update non-breaking dependencies
- Add missing test files (for uncovered modules)
- Add JSDoc/docstrings to exported functions

### Tier 3: Medium-Risk (auto-execute, verify build+tests)
- Set up CI/CD pipelines
- Add TypeScript strict mode
- Refactor for code consistency
- Add error handling patterns
- Add logging infrastructure
- Database migration scripts

### Tier 4: High-Risk (flag for user, create PR)
- Major dependency upgrades (breaking changes)
- Architecture refactors
- New feature development
- Security hardening
- Performance optimization
- Infrastructure changes (Docker, cloud config)

---

## Tech Stack Recipes

### Node.js / TypeScript
```bash
# Quality bootstrap
pnpm add -D eslint prettier husky lint-staged jest @types/jest ts-jest
npx husky install
npx mrm lint-staged
```

### Python
```bash
# Quality bootstrap
pip install ruff pytest pytest-cov mypy pre-commit
pre-commit install
ruff check --fix .
```

### Rust
```bash
# Quality bootstrap
cargo install cargo-audit cargo-tarpaulin
rustup component add clippy rustfmt
cargo clippy --fix
cargo fmt
```

### Go
```bash
# Quality bootstrap
go install golang.org/x/tools/cmd/goimports@latest
go install github.com/golangci/golangci-lint/cmd/golangci-lint@latest
golangci-lint run --fix
```

---

## Integration with Other Skills

| Need | Skill to Use |
|---|---|
| Twitter/X cookies | `/bird` — `bird check` for cookie status |
| Google Workspace tokens | `/gogcli` — `gog auth login` |
| OpenClaw channels | `/openclaw-configure` — channel setup |
| Enconvo bot invocation | `/enconvo-agent-cli` — curl to bots |
| Telegram bot setup | `/openclaw-configure` — `openclaw channels add --channel telegram` |
| Git operations | Native git commands |
| CI/CD (GitHub) | `gh` CLI |
| Dependency scanning | `npm audit` / `pip audit` / `cargo audit` |

---

## Failure Handling

| Failure | Response |
|---|---|
| Tests fail after change | Revert changes, log failure, skip task, move to next |
| Build breaks | Revert, log, flag as needs-manual-review |
| Credential missing | Mark task as BLOCKED, continue with unblocked tasks |
| 3+ consecutive failures | STOP execution, generate failure report, ask user |
| Unknown tech stack | Run Phase 1 only, present findings, ask user for guidance |
| No internet | Skip tasks requiring network, continue with local-only tasks |
| Rate limited (API) | Pause, wait, retry with backoff |

---

## Security Rules

1. **Credentials in `.self-evolve/.env` ONLY** — never in code, commits, or logs
2. **`.self-evolve/.env` MUST be in `.gitignore`** — verify before every commit
3. **Never display credential values** — only confirm "collected" or "missing"
4. **Audit before push** — scan staged files for accidental secret commits
5. **Branch-only changes** — never push directly to main
6. **Revert on failure** — never leave broken code on any branch

---

## Phase 7: NON-STOP AUTONOMOUS MODE

The default execution mode. Once bootstrapped, the agent runs **continuously** without waiting for user input.

### 6.1 Runtime Duration

| Trigger | Duration | Example |
|---|---|---|
| `"Self-evolve /path/to/repo"` | **1 hour** (default) | Default non-stop run |
| `"Self-evolve /path/to/repo for 30m"` | 30 minutes | Short burst |
| `"Self-evolve /path/to/repo for 3 hours"` | 3 hours | Extended session |
| `"Self-evolve /path/to/repo forever"` | **No time limit** | Runs until all tasks done or 3+ failures |
| `"Keep going"` / `"Keep evolving"` | **1 hour** (default) | Resume from where it left off |
| `"Keep going for 2h"` | 2 hours | Resume with custom duration |
| `"Keep going forever"` | No time limit | Resume indefinitely |

Duration formats: `30m`, `1h`, `2h`, `90m`, `3 hours`, `forever`

### 6.2 Non-Stop Rules

**The agent MUST:**
- **Never wait for user input** — not for confirmations, not for approvals, not for anything
- **Self-answer all questions** — if a decision is needed, use best-effort reasoning and pick the most sensible option. Log the decision and reasoning in `log.md` so the user can review later
- **Commit after every completed task** — `git add` specific files, conventional commit, push immediately
- **Push after every commit** — do NOT batch commits. Each task = 1 commit + 1 push
- **Keep the clock running** — track elapsed time, stop when duration expires
- **Run full validation** (typecheck + lint + test) after every change
- **Auto-revert on failure** — if tests break, revert immediately, log it, move to next task

**The agent MUST NOT:**
- Wait for the user to press Enter, confirm, or respond
- Ask "should I continue?" or "does this look good?" — just keep going
- Pause between tasks (move to next task immediately after commit+push)
- Stop for Tier 1-3 tasks (only flag Tier 4 in the log, then skip and continue)
- Push to main/master directly (use feature branches, auto-merge if tests pass)
- **STOP AND SUMMARIZE** — if you catch yourself writing a status report, session summary, or "here's what we did" message, you stopped too early. Go find the next thing to test or fix instead. Summaries happen ONLY when the timer expires.
- **END A RESPONSE WITH WORK, NOT WORDS** — every response must end with a tool call (Bash, Edit, Write, etc.), not with text. If your last output is prose, you paused. Chain your next action immediately. The user should see continuous tool calls, not status updates between them.

### 6.3 Self-Answering Protocol

When the agent encounters a question or ambiguity during execution:

```
1. REASON  — Think through the options using available context (code, docs, patterns)
2. DECIDE  — Pick the most sensible option (prefer conservative/safe choices)
3. LOG     — Record in log.md: "SELF-DECIDED: [question] → [answer] — [reasoning]"
4. EXECUTE — Proceed with the decision
5. TAG     — Add `[self-decided]` tag to the commit message
```

Example log entry:
```markdown
## [2026-03-02 15:45] SELF-DECIDED: ESLint config style
- **Question:** Use flat config or legacy .eslintrc?
- **Decision:** Flat config (eslint.config.js)
- **Reasoning:** Project uses ESLint 9+, flat config is default. Legacy is deprecated.
- **Tag:** [self-decided]
```

### 6.4 Round Structure

Each autonomous round:
1. Check elapsed time — stop if duration exceeded
2. Check plan.md for next READY task (or identify new improvement)
3. Create feature branch: `self-evolve/<task-slug>`
4. Implement the change
5. Run validation: `typecheck → lint → test`
6. If validation passes: commit + push + merge to main (if tests green)
7. If validation fails: attempt fix (1 retry), then revert if still broken
8. Update log.md with outcome
9. Move to next task immediately (no pause)

### 6.5 Priority Heuristics (when no plan item specified)
1. Fix failing tests/builds (blocking)
2. Fix bugs discovered during testing (Round 1 almost always discovers bugs)
3. Add test framework + initial test coverage (correctness first)
4. Reduce code duplication (refactor shared utilities)
5. Add new features / parity commands (interleave with quality tasks)
6. Add linting + formatting (style enforcement AFTER tests exist)
7. Add CI/CD pipeline (automate what's already validated locally)
8. Update documentation

### 6.6 End-of-Run Report

When the timer expires or all tasks are done, the agent MUST:
1. Generate a summary (below)
2. **Run Phase 9: META-EVOLUTION** — update this SKILL.md with lessons learned

```markdown
## Non-Stop Run Complete
**Duration:** 1h 00m (of 1h requested)
**Tasks completed:** 7
**Tasks failed:** 1
**Tasks skipped:** 2 (Tier 4, flagged for user)
**Self-decisions made:** 3
**Commits pushed:** 7

### Self-Decisions Made (review these)
1. [ESLint config] Used flat config over legacy — ESLint 9+ default
2. [Test framework] Chose vitest over jest — native ESM support
3. [Branch strategy] Merged directly after green CI — no PR needed for Tier 1

### Failed Tasks (review these)
1. TypeScript strict mode — 14 type errors, reverted

### Flagged for User (Tier 4)
1. Major dep upgrade: React 18 → 19 (breaking changes)
2. Architecture: Move to monorepo structure
```

---

## Phase 8: PARITY ANALYSIS (Optional)

When the project aims to mirror another CLI/tool's interface:

### 7.1 Research Phase
- Use an Agent subagent to study the target CLI's command structure
- Document all commands, subcommands, flags, and config patterns
- Save to `.self-evolve/<target>-parity.md`

### 7.2 Gap Analysis
Create a mapping table:
```markdown
| Target Command | Our Equivalent | Status |
|---|---|---|
| target cmd1 | our cmd1 | done |
| target cmd2 | (none) | missing |
| target cmd3 | our cmd3 | partial |
```

### 7.3 Not Applicable Section
**Always include a "Not Applicable" section** — explicitly list features that WON'T be implemented and why. This prevents wasted effort on irrelevant parity targets:
```markdown
### Not Applicable (architectural differences)
- `target cmd-x` — Our system handles this differently via [mechanism]
- `target cmd-y` — Not relevant for our use case because [reason]
```

### 7.4 Prioritized Implementation
- Priority 1: Core commands (config, status, health, doctor)
- Priority 2: Feature commands (agents, channels, messaging)
- Priority 3: Advanced features (cron, hooks, plugins, memory)
- Priority 4: Infrastructure (gateway, nodes, sandbox)

### 7.5 Round-by-Round Delivery Tracking
Track velocity and test growth per round in the parity doc:
```markdown
| Round | Commands Added | Cumulative Tests |
|---|---|---|
| Round 1 | channels add/remove/list | 38 |
| Round 2 | config get/set, status, doctor | 72 |
| Round 3 | agents bind/unbind, message send | 91 |
```
This makes progress tangible and shows the compounding effect of each round.

---

## Phase 9: META-EVOLUTION (Skill Self-Improvement)

**This skill improves itself.** Every time it's used to evolve a project, it MUST update its own `SKILL.md` with lessons learned. Over time, this compounds — each run makes the next run smarter.

### 8.1 The Meta-Evolution Loop

```
USE SKILL TO EVOLVE REPO
        ↓
   Learn lessons (gotchas, patterns, failures, new recipes)
        ↓
   UPDATE THIS SKILL.MD
        ↓
   Next user gets a smarter skill
        ↓
   REPEAT
```

### 8.2 What to Capture (MANDATORY after every run)

After every self-evolve session (when the timer expires or all tasks complete), the agent MUST:

1. **Review the run log** — scan `.self-evolve/log.md` for:
   - Failures that required novel solutions
   - Self-decisions that worked (or didn't)
   - Unexpected gotchas with specific tech stacks
   - New validation patterns discovered
   - Time sinks (tasks that took >10 min)

2. **Update SKILL.md** — append to the "Learned Patterns" section:
   - New gotchas under appropriate sub-headers
   - New tech stack recipes if a new stack was encountered
   - New failure handling patterns
   - Refined priority heuristics based on what actually worked
   - New tool/command patterns discovered

3. **Update config defaults** — if a runtime setting consistently needed overriding, change the default in the config template

4. **Update tier classifications** — if a "Tier 2" task consistently broke builds, promote it to Tier 3

### 8.3 Self-Evolution Protocol

```
At the END of every self-evolve run:

1. REFLECT  — What worked? What failed? What was surprising?
2. EXTRACT  — Pull out reusable patterns (not project-specific details)
3. WRITE    — Append to "Learned Patterns" section in THIS file:
             ~/.claude/skills/general-self-evolve/SKILL.md
4. DEDUPE   — Check if the pattern already exists; update rather than duplicate
5. VERIFY   — Ensure the SKILL.md is still valid markdown, no broken formatting
```

### 8.4 What NOT to Capture

- Project-specific details (repo paths, API keys, user names)
- One-off edge cases that won't recur
- Patterns already well-documented in the skill
- Speculative ideas not validated by actual execution

### 8.5 Evolution Categories

Each learned pattern should be tagged with a category:

| Tag | Meaning | Example |
|---|---|---|
| `[gotcha]` | Unexpected failure or trap | "pnpm workspace requires --filter for test" |
| `[recipe]` | New tech stack setup pattern | "SvelteKit + Vitest bootstrap steps" |
| `[heuristic]` | Better priority/decision rule | "Always fix lockfile before dep updates" |
| `[tool]` | New CLI tool or command discovered | "biome replaces eslint+prettier in 1 tool" |
| `[validation]` | Better validation sequence | "Run typecheck BEFORE lint to catch real errors" |
| `[perf]` | Faster way to do something | "Use --changed flag to only test affected files" |
| `[revert]` | Pattern that caused reverts | "Don't auto-upgrade major versions of type-only deps" |

### 8.6 Compounding Intelligence

Over time, this skill accumulates:

```
Run 1:   Base skill (manual patterns)
Run 5:   +10 gotchas, +3 recipes, +2 heuristics
Run 20:  +40 gotchas, +12 recipes, +8 heuristics, refined tier classifications
Run 100: Near-AGI for repo improvement — handles most stacks, knows most traps
```

The "Learned Patterns" section below is the living knowledge base. It grows with every use.

### 8.7 Skill Health Check

Every 10 runs (or when the Learned Patterns section exceeds 200 lines), the agent should:

1. **Consolidate** — merge redundant patterns
2. **Promote** — move battle-tested patterns into the main phases (e.g., a gotcha that happens every time should become an execution rule)
3. **Archive** — move outdated patterns (deprecated tools, old library versions) to an `archived-patterns.md` file
4. **Reorganize** — keep the section scannable and well-categorized

---

## Learned Patterns (v1.3.0)

Patterns discovered from real-world self-evolve sessions. **This section grows automatically with every use.**

### Git Push Gotchas
- **GitHub Actions CI requires `workflow` scope** on OAuth tokens — if push fails with
  "refusing to allow an OAuth App to create or update workflow", gitignore the workflow file
  and commit without it until the user upgrades their token
- **Always `git add` specific files**, never `git add -A` (prevents accidental .env commits)

### Testing Best Practices
- **vitest over jest** for TypeScript projects — faster, native ESM, no config needed
- **Mock at module boundary** (vi.mock) not at function level for cleaner tests
- **Test file location**: `src/module/__tests__/module.test.ts` colocated with source

### Code Dedup Pattern
When two files differ only by a constant (e.g., MAX_LENGTH 4096 vs 2000):
1. Extract shared logic to `src/utils/shared-module.ts` with parameterized function
2. Replace originals with thin wrappers that call shared function with their constant
3. Keep originals' export signatures unchanged (no import path changes needed)

### Execution Ordering [heuristic]
- **Tests BEFORE linting** — Add test framework and initial test coverage BEFORE configuring ESLint/Prettier. Tests catch real bugs; linting catches style. Validate correctness first, then enforce style.
- **Interleave features with quality** — Don't do all quality tasks first then all features. Mix feature work (parity commands) with quality (tests, linting) to keep momentum and validate features immediately.
- **Bug discovery during testing drives Round 1** — The first self-evolve round after evaluation often discovers bugs through testing that weren't visible in the evaluation phase. Prioritize fixing discovered bugs before adding new features.

### Cumulative Metrics [heuristic]
- **Always track cumulative test count** in log entries, not just per-task. Creates a trajectory (`0 → 38 → 50 → 72 → 91 → 125`) that shows project health growth.
- **Track insertion count** per round (e.g., `+326 insertions`) as a scope indicator beyond just "files changed."
- **Track cumulative LOC** in evaluation header for quick project size reference.

### Python Project Bootstrap [recipe]
For Python repos with no package structure:
1. Add `__init__.py` files FIRST (enables imports for tests)
2. Do NOT modify existing `sys.path.append` hacks until test coverage exists
3. Add `pyproject.toml` with both `[tool.ruff]` and `[tool.pytest.ini_options]`
4. Use lenient ruff config for legacy codebases — ignore style violations in working scripts, catch only real bugs
5. Order: requirements.txt → README → __init__.py → tests → ruff → editorconfig → pre-commit

### numpy Boolean Identity [gotcha]
`np.True_ is not True` in Python — numpy booleans are a different type. When testing functions that return numpy bools (pandas operations, comparisons), always use `== True/False` not `is True/False` in assertions.

### GitHub Actions Workflow Push [gotcha]
When push fails with "refusing to allow an OAuth App to create or update workflow", **revert the commit immediately** rather than leaving a diverged local/remote state. The revert pushes cleanly since it removes the workflow file. Log as BLOCKED and move on.

### Ruff Config Strategy [heuristic]
For repos with 100+ existing files and 500+ violations:
1. Start with `select = ["E", "F", "W"]` (basic rules only)
2. Add every high-count violation to `ignore` list with comments explaining why
3. Auto-fix whitespace issues (`W291`, `W293`) — zero-risk
4. Goal: clean `ruff check` immediately, tighten rules over subsequent runs

### CLI Command Pattern (Commander.js)
```
src/commands/{group}/index.ts  → registerXCommands(program)
src/commands/{group}/{cmd}.ts  → registerCmd(parent)
src/commands/{standalone}.ts   → registerXCommand(program)
```
- Group commands under `program.command('group')` for related features
- Top-level commands for single-purpose utilities (status, health, doctor)
- Always add `--json` flag for machine-readable output

### Dead Dependency Detection [heuristic]
After evaluation, grep the source tree for every package.json dependency. If a dependency is never imported/required anywhere in `src/`, it's dead weight — remove it. Example: `dotenv` left over from an earlier `.env`-based config was never imported after migration to JSON config store. `grep -r "dotenv" src/` → zero hits → safe to remove.

### DRY Across Command Files [heuristic]
Standalone command files (e.g., `version.ts`) often accumulate private helper functions that duplicate exports from shared utility modules (e.g., `info.ts`). After building shared modules, audit all command files for private functions whose names match exported utilities. Replace with imports — saves 20+ lines per file.

### Maturity Plateau Recognition [heuristic] [UPDATED]
When test-to-source ratio exceeds 100%, ESLint reports zero warnings, comprehensive audit finds zero TODOs/dead exports/type assertions, the codebase has reached **code-level** maturity plateau. BUT THIS DOES NOT MEAN IT WORKS. At this point:
- **MANDATORY: Run Phase 5 LIVE TEST before declaring plateau** — code-level clean doesn't mean functionally correct
- Shift focus to: live/integration testing, deployment, user-facing features
- Only declare true maturity after live tests pass
- Track plateau state in evaluation.md but mark as "code-level only" until live-tested

### Explore Agent Verification [gotcha]
Subagent research (Explore agents) can report false positives — e.g., claiming a function is duplicated when it's actually correctly imported. **Always verify subagent findings manually** (read the actual file) before acting on them. Cost of verification: 1 Read call. Cost of acting on false positive: wasted commit + revert.

### ESLint as Final Sweep [validation]
After all code changes in a round, run `npx eslint src/` as a final sweep. Catches subtle issues like unused `catch` variables (`catch (e)` → `catch`) that slip through during refactoring. Do this as the last step before committing, not interleaved with changes.

### Unit Tests Are Necessary But Not Sufficient [heuristic] [CRITICAL]
Mocks test your assumptions. Live tests test reality. Mocks can't reveal shared state bugs, silent UX failures, or response content types you didn't know the API returns. After every batch of code improvements, run Phase 5 LIVE TEST. See `case-studies.md` (Case Study 1).

### Live Testing Is a Non-Stop Loop [heuristic] [CRITICAL]
```
TEST → bug found → FIX → RETEST → new bug found → FIX → RETEST → ...repeat until clean
```
Never stop after one pass. The first round ALWAYS finds bugs. The second round finds bugs in your fixes. Keep going until a full pass is clean. See `case-studies.md` (Case Study 3).

### Misdiagnosis Is Worse Than No Diagnosis [heuristic] [CRITICAL]
When you change two things and the bug goes away, you don't know which fixed it. Change one thing at a time. Verify your diagnosis independently. A fix that works doesn't prove your diagnosis was correct. See `case-studies.md` (Case Study 2).

### Think Bigger — Generalize, Don't Patch [heuristic] [CRITICAL]
When you fix a bug for one type/scenario, ask: "What are ALL the types this applies to?"
- **Whitelists → Exclude-lists:** Don't enumerate allowed types. Exclude the known-bad ones. Covers all future types.
- **One content type → All:** If you handle `image_url`, also handle `text`, `file`, etc. from the same structure.
- **`existsSync` → `isFile()`:** Filesystem checks that pass for directories will crash file operations. Validate specifically.

See `case-studies.md` (Case Study 3).

### Stale Sessions Cause Ghost Bugs [gotcha]
LLM agents cache conversation context in sessions. Config changes don't propagate to running sessions. After any config/KB change: force new sessions, tell agents to re-read files, and retest the broken scenario. See `case-studies.md` (Case Study 4).

### Check Your Pipeline Before Blaming the Agent [heuristic]
When an agent "can't" produce something, `curl` the API directly and read the raw response. The agent almost certainly produced it — your parsing/delivery code dropped it. See `case-studies.md` (Case Study 5).

### "All Good" Is Never True on the First Pass [heuristic] [CRITICAL]
The natural tendency after fixing code and seeing tests pass is to summarize results and stop. Resist this. In practice, every "all good" report in this skill's history was followed by the user finding more bugs through harder testing. The pattern:
- Agent reports "fixed, tests pass" → user tests manually → bugs found → repeat 3-5 times
- The agent's definition of "done" is always premature

**Rules for autonomous mode:**
- After fixing a batch of bugs, don't report — immediately run the next tier of live tests
- After live tests pass on one channel, test the other channels without being asked
- After testing one file type, test ALL file types without being asked
- After testing happy path, test error paths and edge cases
- Keep going until you've exhausted every testable scenario, not just the ones in the plan
- If you find yourself writing a summary, you stopped too early — go test something else first

### Commit and Push Per Fix, Not Per Batch [heuristic] [CRITICAL]
The workflow for every bug: find → reason → fix → review → retest → commit → **push**. Each verified fix is one commit, pushed immediately. Don't accumulate unpushed commits — if something breaks between fixes, you can't isolate which commit caused it. Pushing per fix also means the remote always reflects reality. Batching commits then pushing 6 at once defeats the purpose of incremental verification.

### Deploy = Code + Mirror + Services [gotcha]
When code runs from a synced mirror (rsync, Docker copy, CI artifact), changing source code doesn't change running services. A "fix" that passes local tests but isn't deployed to running services is not a fix. Always redeploy after code changes and verify the deployed code matches source. Build the sync step into the deploy command so it can't be forgotten.

### Long-Running Self-Evolve Sessions [meta]
After 80+ rounds on a single codebase:
- The codebase reaches diminishing returns — each round's improvement is smaller
- Shift from "find bugs and add tests" to "architectural hardening and cross-cutting concerns"
- Update MEMORY.md and SKILL.md after every session (Phase 8 META-EVOLVE mandate)
- Track cumulative round count across sessions to avoid re-doing work

---

## Appendix: Self-Evolving Agent Architecture Reference

Distilled from OpenClaw's architecture. Use these patterns when designing autonomous agent systems beyond repo improvement.

### The Core Insight

**Knowledge (text in prompts) costs tokens every call and can be forgotten. Behavior (self-written code) runs automatically, zero tokens.**

### 4 Pillars of Self-Evolving Agents

| Pillar | What It Does | Implementation |
|---|---|---|
| **Always-On Daemon** | Runs continuously, checks for work on schedule | Heartbeat (batched checks) or Cron (exact timing) |
| **Autonomous Execution Loop** | Persistent agent cycle without user input | Ralph Loop: Receive → Plan → Execute → Evaluate → Iterate |
| **Self-Writing Code** | Agent writes tools/skills into itself | Foundry: Observe → Research → Learn → Write → Deploy |
| **Pattern Crystallization** | Repeated workflows become single commands | Auto-triggers at 5+ repeats with 70%+ success rate |

### Heartbeat vs Cron Decision Tree

1. Exact timing required? → **Cron**
2. Needs isolation from main session? → **Cron** (isolated)
3. Can batch with other checks? → **Heartbeat**
4. One-shot reminder? → **Cron** with `--at`
5. Requires different model/thinking? → **Cron** (isolated)
6. Otherwise → **Heartbeat**

### Ralph Loop Guard Rails

```json5
{
  "maxIterations": 50,       // cap loop cycles
  "maxRuntime": 120,         // time limit in minutes
  "pauseInterval": 5,        // delay between iterations (seconds)
  "progressReports": true,   // periodic updates
  "reportInterval": 5        // update every N iterations
}
```

Key properties: quality-based iteration (self-evaluates outputs), explicit stopping conditions, cost-awareness (token consumption tracking), multi-hour capable.

### Pattern Crystallization

The system observes every workflow: `{ goal, tool_sequence, outcome, duration, success }`.

**Crystallization triggers when:** a workflow repeats **5+ times** with **70%+ success rate**.

**Result:** Multi-step workflows compress into single commands. Example: `git → build → test → deploy` becomes one `deploy_staging` tool. 8 tool calls → 1. Token cost → zero (compiled behavior).

**This is recursive self-improvement**: the system that writes the code IS the code being written. Each capability makes acquiring the next capability easier. Research shows 17-53% improvement through "non-gradient learning via LLM reflection and code updates."

### Foundry Security Layers

Self-generated code must pass:
1. **Static Scanning** — Blocks: `child_process`, `eval`, `Function`, credential access, arbitrary file ops
2. **Flagged Patterns** — Warnings for risky operations requiring explicit approval
3. **Runtime Validation** — Isolated Node process execution before production deployment

### Cost Optimization

- Keep task checklists minimal to reduce token overhead
- Batch similar checks into one heartbeat rather than multiple cron jobs
- Use isolated cron with cheaper models for routine tasks
- Crystallize patterns to eliminate repeated token costs
- Use `target: "none"` on heartbeat for internal processing only

### Sources

- [OpenClaw GitHub](https://github.com/openclaw/openclaw) — 68k+ stars
- [Foundry GitHub](https://github.com/lekt9/openclaw-foundry) — Self-writing meta-extension
- [Ralph Loop Guide](https://clawtank.dev/blog/openclaw-ralph-loop-guide)
