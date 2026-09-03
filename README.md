# OpenClaw Workspace Template

A lightweight workspace template for a persistent personal AI assistant. It gives an agent a home base: identity, operating rules, memory, local tool notes, skill-design conventions, and optional heartbeat tasks.

The template is meant to be copied, personalized, and evolved over time. Most files are plain Markdown so the assistant can read and update them directly during normal work.

## What's Included

| File | Purpose |
| --- | --- |
| `AGENTS.md` | Core operating instructions, safety rules, memory guidance, and proactive behavior. |
| `IDENTITY.md` | The assistant's name and short identity marker. |
| `SOUL.md` | Personality, boundaries, tone, and continuity guidance. |
| `USER.md` | A private profile for the person the assistant helps. |
| `MEMORY.md` | Curated long-term memory for direct, private sessions. |
| `HEARTBEAT.md` | Optional periodic checks or background reminders. Leave empty to skip heartbeat work. |
| `TOOLS.md` | Local environment notes such as tool slugs, device names, accounts, and conventions. |
| `SKILLS_DESIGN.md` | Standards for writing reusable skills under `skills/<skill-name>/SKILL.md`. |
| `4Geeks_assistant/` | Example project-specific assistant notes. |

## How It Works

The workspace separates agent context into focused files:

1. **Startup context** lives in files such as `AGENTS.md`, `SOUL.md`, `IDENTITY.md`, and `USER.md`.
2. **Memory** is split between raw daily notes in `memory/YYYY-MM-DD.md` and curated long-term notes in `MEMORY.md`.
3. **Tooling notes** stay in `TOOLS.md`, keeping local setup separate from reusable skills.
4. **Skills** are designed as self-contained procedures with clear inputs, outputs, and success criteria.
5. **Heartbeat tasks** can be added to `HEARTBEAT.md` when the assistant should periodically check or maintain something.

## Getting Started

1. Copy this repository or use it as a template for a new assistant workspace.
2. Fill in `IDENTITY.md` with the assistant's name.
3. Update `USER.md` with only the personal context the assistant truly needs.
4. Add local tool notes to `TOOLS.md` as integrations become available.
5. Keep `HEARTBEAT.md` empty unless you want periodic background checks.
6. Create skills under `skills/<skill-name>/SKILL.md` using the template in `SKILLS_DESIGN.md`.

## Memory Model

Use two memory layers:

- `memory/YYYY-MM-DD.md` for raw chronological notes.
- `MEMORY.md` for distilled facts, preferences, lessons, and durable context.

Avoid storing secrets in either layer. If a workflow needs credentials, keep them in an appropriate secret manager or local environment outside version control.

## Skill Authoring

New skills should follow the standard in `SKILLS_DESIGN.md`. Each skill should clearly define:

- What outcome it produces.
- What context it gets from bootstrap files.
- What it must gather at runtime.
- Where output goes and how success is verified.

Suggested location:

```text
skills/
  example-skill/
    SKILL.md
```

## Privacy And Safety

This workspace may contain personal notes, account references, and local integration details. Before sharing or publishing a customized copy:

- Review `USER.md`, `MEMORY.md`, `TOOLS.md`, `memory/`, and any project-specific folders.
- Remove tokens, credentials, private contacts, and sensitive logs.
- Keep reusable skill instructions separate from local account details.
- Treat external actions such as sending messages, posting publicly, or emailing as confirmation-required workflows.

## Repository Status

This repository is a template, not a conventional application package. There are no build, test, or install commands required by default.

## Suggested Next Steps

- Add a `skills/` directory once you have reusable procedures to store.
- Add a `.gitignore` if local memory, generated logs, or credentials should stay out of version control.
- Periodically review daily memory files and fold durable lessons into `MEMORY.md`.