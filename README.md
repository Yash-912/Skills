# Agent Skills

Reusable skills for coding agents. Each skill lives in its own folder with a `SKILL.md` instruction file.

## Handoff

[`handoff`](handoff/SKILL.md) turns the current coding session into a compact engineering handoff for a fresh agent. Use it when a long session has accumulated too much context or when you want to pause and resume in a new session.

The skill reviews the available conversation, relevant code, command results, changes, errors, decisions, and Git state, then creates or rewrites `handoff.md` in the active project root. The next agent can use that file and the repository to continue the task.

### What it captures

The document has 16 sections:

1. Objective
2. Project / System Context
3. Current State
4. Changes Made During This Session
5. Files Touched
6. Important Code Locations
7. Decisions and Reasoning
8. What We Tried: worked and failed/rejected approaches
9. Commands Run
10. Tests and Verification
11. Errors / Bugs / Blockers
12. Environment / Configuration
13. Git / Repository State
14. Open Questions
15. Next Steps
16. Recommended First Action for the Next Agent

It emphasizes concrete paths, symbols, results, and actionable next steps. Unknowns are labeled, and failed experiments are retained so the next agent can avoid repeating them. An existing handoff is rewritten to represent the latest state rather than accumulating session dumps.

### Install

Clone this repository:

```sh
git clone https://github.com/Yash-912/Skills.git
```

Copy the entire `handoff` folder, including `agents/openai.yaml`, into one of these locations:

- Personal Codex skills: `$CODEX_HOME/skills/handoff`, or `~/.codex/skills/handoff` when `CODEX_HOME` is unset.
- Project-local skills: `<your-project>/.agents/skills/handoff`.

Choose one location to avoid duplicate entries. Preserve any existing customized version before replacing it. Open a fresh agent session if the installed skill is not yet listed.

### Use

In the coding session you want to hand off, invoke:

```text
$handoff
```

You can also request:

```text
Use the handoff skill to write handoff.md for the current task.
```

The instructions also recognize `/handoff` when the host supports that invocation syntax. Creating or installing the skill does not itself generate a project handoff.

After the file is written, open a fresh session in the same project and give the agent this prompt:

```text
Read handoff.md and the applicable repository instructions. Check the current
repository state, then continue from the recommended first action. Preserve
intentional decisions and do not repeat failed attempts without new evidence.
```

### Behavior and limits

- The handoff operation documents the project; it does not change application code or commit, push, install dependencies, or control services unless separately instructed.
- Secrets are excluded, including credentials embedded in commands, logs, URLs, and connection strings. Configuration variable names and setup requirements can be recorded.
- Only available session history and accessible repository evidence can be reconstructed. Missing history and stale verification are identified explicitly.
- Generating a handoff does not automatically reset the context or open another session. The current turn ends after reporting the written file.

## ASD-STE100 Writing

[`asd-ste100`](asd-ste100/SKILL.md) writes or revises English with up to 80 percent ASD-STE100-inspired Simplified Technical English. Use it for replies, explanations, documentation, and other prose when you want clear technical writing with room for natural phrasing.

The 80 percent target is a flexible style preference, not a measured compliance score. The skill favors short sentences, direct instructions, active voice, and consistent terms. It preserves meaning, qualifications, necessary detail, and exact technical text. It includes examples and a review checklist.

### Install

Copy the entire `asd-ste100` folder, including `agents/openai.yaml`, into one of these locations:

- Personal Codex skills: `$CODEX_HOME/skills/asd-ste100`, or `~/.codex/skills/asd-ste100` when `CODEX_HOME` is unset.
- Project-local skills: `<your-project>/.agents/skills/asd-ste100`.

Choose one location to avoid duplicate entries. Preserve an existing customized version before replacing it. Open a fresh agent session if the installed skill is not yet listed.

### Use

```text
$asd-ste100 Explain how this service works.
```

For a rewrite:

```text
Use $asd-ste100 to rewrite this README with up to 80 percent
ASD-STE100-inspired English. Preserve the technical details and commands.
```

The skill applies to the requested output and follow-up revisions of that deliverable. It can work with an artifact skill to guide prose in documents or presentations.

### Behavior and limits

- Code, commands, identifiers, paths, URLs, exact labels, data, and verbatim quotations retain their original text.
- Accuracy, requested format, and explicit user requirements take priority over the style target.
- The skill does not claim formal ASD-STE100 compliance or include the full approved dictionary. Its editing suggestions and examples are not certified STE text.
- It links to the [official ASD-STE100 guidance](https://asd-ste100.org/STE_faq.html) and [standard downloads](https://asd-ste100.org/STE_downloads.html) for authoritative checks.
- Creating the skill in this repository does not install it or change global writing preferences.

## Repository layout

```text
Skills/
├── README.md
├── handoff/
│   ├── SKILL.md
│   └── agents/
│       └── openai.yaml
└── asd-ste100/
    ├── SKILL.md
    └── agents/
        └── openai.yaml
```

`SKILL.md` contains the reusable workflow. `agents/openai.yaml` contains the skill's display name and suggested invocation prompt. The generated project `handoff.md` belongs in the project being handed off, rather than in this skill repository.
