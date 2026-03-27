---
name: web3-feature
description: Use this skill when building any new feature for the WalletRep, wlltresume, or Wallet Passport products. Generates a structured, self-contained Claude Code prompt ready to paste. Assumes AGENTS.md is loaded — does not repeat standing rules.
---

# Web3 Feature Prompt Builder

Generate a ready-to-paste Claude Code prompt for a new feature. AGENTS.md covers standing rules — this skill only handles prompt structure and product thinking.

---

## Step 1 — Product Thinking Check (always do this first)

Before generating the prompt, answer these out loud:
- Is there a simpler version to build first?
- Does this touch more than one product in the suite? If so, flag the integration point.
- Is there an open GitHub issue for this? Reference it.
- Is this small enough for one Claude Code session? If not, propose phases.

---

## Step 2 — Phase if Needed

If the request is too large, split it before writing the prompt:
- **Phase 1** — Core functionality only
- **Phase 2** — Edge cases, empty states, mobile
- **Phase 3** — Cross-product integration

One prompt per phase.

---

## Step 3 — Generate the Prompt

```
## Context
[Product name. What currently exists. Relevant file paths.]

## Task
[Single scoped feature. One phase only.]

## Files to Create / Edit
[Exact file paths — never vague.]

## Acceptance Criteria
- [ ] [Specific, testable outcome]
- [ ] Mobile responsive
- [ ] Empty states handled — no blank sections on failed API calls
- [ ] Errors handled gracefully — UI never crashes

## Git
- Commit: `feat: [description] (closes #[issue])`
- Push to main → verify Vercel deployment
```

---

## Step 4 — After the Prompt Runs

Remind me to:
1. Update `CHANGELOG.md` under `[Unreleased]`
2. Close the GitHub issue if done
3. Confirm Vercel deployment is live
4. Note any follow-up phases or new issues to open
