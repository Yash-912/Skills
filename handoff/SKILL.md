---
name: handoff
description: Create or refresh handoff.md so a fresh coding agent can continue the current engineering task from the repository and a compact, evidence-based handoff. Use when the user invokes /handoff, $handoff, handoff-doc, or asks to hand off the current coding session to a fresh agent.
---

# Handoff

Write a compact but comprehensive engineering handoff for a fresh coding agent. Assume the current conversation will disappear immediately after writing the file. The next agent must be able to continue using only `handoff.md` and the repository.

## Scope and destination

- Interpret invocation as a request to document the current task and end this working turn after the handoff is written. Do not continue implementation afterward or claim to reset the context or start another session.
- Write `handoff.md` at the active repository root unless the user specifies another location. Without a repository, use the active project/workspace directory. If multiple repositories are relevant, identify their paths and the primary handoff location.
- This operation is observational and documentational. Do not change application code, install dependencies, start or stop services, commit, stage, push, or modify external systems unless separately instructed.
- Skill creation or editing is not itself an invocation of this workflow.

## Reconstruct the engineering state

1. Review the entire available session: user intent, accepted constraints, messages, tool outputs, commands and their results, changes, errors, attempts, decisions, and unfinished work. Include relevant prior context available through summaries or existing handoffs. Do not imply access to unavailable or truncated history; state any material gaps.
2. Read an existing `handoff.md` before replacing it. Treat it as prior context whose claims may be stale, and verify consequential claims against current evidence when possible.
3. Inspect applicable repository instructions and useful repository state. Typical read-only checks are:

   ```text
   git rev-parse --show-toplevel
   git status --short --branch
   git diff --stat
   git diff
   git diff --cached --stat
   git diff --cached
   git log -5 --oneline
   ```

   Scope large diffs to relevant files; inspect important untracked files separately because ordinary diffs omit them. Use `rg` and targeted file reads to confirm key symbols, configuration, and implementation details. If Git is unavailable, record that and continue with available evidence.
4. Distinguish changes attributable to this session from pre-existing user changes, generated artifacts, and changes of unknown origin. Repository status alone does not establish who made a change. Preserve unrelated work.
5. Separate observed code state, observed runtime/test results, intentions, and hypotheses. Record verification freshness: a test run before later edits does not verify the final code. Include relevant command results already observed; do not claim checks were run when they were not. Run additional non-mutating checks only when useful and within scope. Do not rerun expensive or externally mutating workflows merely to write the handoff.
6. Synthesize the result by engineering topic rather than conversation chronology. Prioritize current state, decisions, failed attempts, changed files, known issues, and next actions.

Never put passwords, tokens, API keys, private keys, connection-string credentials, or other secrets in the handoff. Redact secrets in commands, URLs, logs, diffs, and error messages too. Record configuration names and requirements, such as `OPENAI_API_KEY must be configured`, without values. Avoid reading credential stores or dumping environment variables to collect context.

## Required output structure

Use the title and all 16 numbered headings below. Keep inapplicable sections short: use `Not applicable`, `None known`, `Not verified`, or `Unknown` as appropriate, without implying absence when evidence is missing. Add useful subheadings where needed. Include concrete repository-relative paths, symbols, commands, endpoints, errors, and results; include line numbers only when verified and useful.

# Project Handoff

## 1. Objective

State the user's intended outcome, feature or problem, motivation, definition of done, constraints, and acceptance criteria. Describe the active objective accurately, including later steering. Separate requested work from optional follow-ups.

## 2. Project / System Context

Include only continuation-relevant application purpose, languages, frameworks, runtime, package manager, important libraries, architecture, services, databases, APIs, external dependencies, deployment context, and repository layout.

## 3. Current State

Explicitly distinguish working functionality, partial implementation, missing functionality, known broken behavior, temporary workarounds, and incomplete refactors. Summarize the current test/build state with freshness and limits. Describe what exists now, not just what was planned.

## 4. Changes Made During This Session

For each meaningful change, give its file path, what changed, why, and the primary functions, classes, or components affected. Cover deletions and renames where relevant. Attribute only changes supported by session evidence; label uncertain attribution. Do not paste entire files.

## 5. Files Touched

Provide a concise inventory grouped into created, modified, deleted, renamed, and investigated but unchanged. Identify pre-existing or unattributed changes separately when relevant. Use old and new paths for renames. This inventory must reflect actual work, not planned edits.

## 6. Important Code Locations

List the implementation entry points that reduce exploration time: functions, classes, components, routes, API handlers, database models, configuration, tests, and scripts. Prefer `path::symbol — role`, for example `src/agent/executor.ts::executeTask() — main execution loop`.

## 7. Decisions and Reasoning

Capture each consequential engineering or product decision, its rationale, alternatives actually considered, and tradeoffs. Preserve intentional architecture, user preferences, and constraints the next agent could otherwise reopen unnecessarily. Distinguish accepted decisions from proposals.

## 8. What We Tried

### Worked

For significant successful approaches, record the approach, result, and evidence. Bound conclusions to what was demonstrated.

### Failed / Rejected

Record the approach, observed error or symptom, suspected cause, and whether or under what changed conditions retrying makes sense. Distinguish observed failure, inconclusive experiment, and rejected proposal. Include enough detail to prevent repeating failed experiments without a reason.

## 9. Commands Run

Record important commands exactly enough to reproduce them, with working directory or shell when necessary. Include outcome, warnings, relevant environment variable names, and prerequisites. Separate commands actually run from suggested future commands. Omit trivial exploration unless it exposed meaningful state; sanitize sensitive arguments.

## 10. Tests and Verification

Record tests, lint, typecheck, builds, manual checks, endpoints, and scenarios actually verified. Give pass/fail/skip counts and failing test names when known. State whether verification occurred before or after the latest relevant changes. Clearly list what remains unverified and whether failures are new, pre-existing, or unattributed.

## 11. Errors / Bugs / Blockers

Classify issues as confirmed bugs, suspected bugs, external blockers, or unanswered questions. For each, provide symptom, exact or abbreviated sanitized error, affected code, suspected root cause, severity/impact, and next investigation when known. Remove resolved blockers from this section; retain their useful lessons under attempts or decisions.

## 12. Environment / Configuration

Record required environment variable names, ports, feature flags, service dependencies, database setup, Docker requirements, local assumptions, and necessary tools/versions when known. Include relevant running process or temporary worktree state needed to resume safely. Never include secret values; do not invent configuration or version information.

## 13. Git / Repository State

Record the observed branch, relevant commits, staged and unstaged changes, untracked files, merge/rebase state, and important diff implications. Distinguish local evidence from remote status that was not checked. Identify generated files and whether they should be committed only if known. Do not commit as part of the handoff.

## 14. Open Questions

List unresolved questions that affect implementation, noting relevant options or the decision owner if known. Do not silently resolve questions that were left open. Keep optional product ideas separate from actual blockers.

## 15. Next Steps

Give an ordered, concrete continuation plan using paths, symbols, tests, or commands. Item 1 must be the exact next action you would take if this context were continuing. Explain essential dependencies and authorization requirements already known. Avoid generic instructions such as “continue implementing.” If the task is complete, say so and give the appropriate review or verification action without inventing more implementation work.

## 16. Recommended First Action for the Next Agent

Finish with a short explicit instruction identifying the first file(s), symbol(s), test(s), or command to inspect/run and the issue to resolve. Make it agree with Next Steps item 1. Include any essential intentional decision or failed approach the next agent must respect.

## Rewrite, compress, and verify

- Rewrite an existing handoff into the latest canonical project state; do not append another session dump. Preserve still-relevant context, decisions, and failed experiments. Update completed tasks, test status, changed files, open questions, and next steps; remove obsolete plans and resolved blockers.
- Prefer facts and compact bullets over narrative. Avoid duplicate detail, conversational material, generic explanations, excessive code dumps, and obvious repository facts that do not help continuation. Cross-reference sections for details that serve multiple purposes.
- Aggressively compress low-value history in long sessions while preserving evidence that prevents duplicated work, incorrect assumptions, or reversals of intentional decisions. Do not impose a word limit that discards critical continuation information.
- Write the file using the environment's supported file-editing mechanism. Read it back and check the required headings, accuracy, secret redaction, latest state, uncertainty labels, and consistency of the first action. Confirm that only the intended documentation changed during this operation.
- Ask yourself: “Could a capable agent with only this file and the repository resume without wasting time, repeating mistakes, or misunderstanding the goal?” Add missing actionable context before finishing.
- End with a brief report that the handoff was written, including its path. Do not resume coding after producing it.
