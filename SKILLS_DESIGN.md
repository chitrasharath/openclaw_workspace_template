# SKILLS_DESIGN.md — How to Write a Skill

Every skill in this workspace lives under `skills/<skill-name>/SKILL.md`. Before you write or approve a skill, it must answer three questions clearly. If any answer is missing, the skill is not ready.

---

## The three required parts

### 1. What does this skill do?

**One sentence.** State the outcome, not the mechanism.

| Good | Bad |
|------|-----|
| "Fetches Pittsburgh weather and sends Chitra a formatted summary." | "Uses curl and wttr.in and maybe Composio." |
| "Summarizes unread Gmail and highlights action items." | "Helps with email." |

Put this sentence in the skill's YAML `description` frontmatter and repeat it as the opening line of the skill body.

---

### 2. What input does the agent need?

List what the agent must already know or gather before running the skill. Split inputs into two buckets.

#### A. Known from bootstrap files (do not duplicate — reference)

The agent loads these every session. A skill should say **which fields matter** and **where to look**, not copy whole files.

| File | What the agent knows from it | Skill should reference when… |
|------|------------------------------|------------------------------|
| **IDENTITY.md** | Name (Nova), vibe, emoji, role as Chitra's assistant | Tone, sign-off, or how to present results |
| **SOUL.md** | Voice, boundaries, Vedic lens, when to ask vs act | Any outbound message, advice, or judgment call |
| **AGENTS.md** | Memory rules, red lines (privacy, stop-and-ask), group-chat behavior, heartbeats | Before external actions, shared contexts, or proactive outreach |
| **USER.md** | Chitra's name, location (Pittsburgh), timezone, email, goals, preferences | Personalization, scheduling, recipient addresses |
| **TOOLS.md** | Composio tool slugs, CLI paths, local conventions, timezone | Which tool to call and how (Gmail, Calendar, etc.) |

**Example input block for a skill:**

```markdown
## Input

**From bootstrap (already in context):**
- USER.md → recipient: Chitra, location: Pittsburgh, email: chitrasharathchandra001@gmail.com
- TOOLS.md → `GMAIL_SEND_EMAIL`, `~/.composio/composio execute`, timezone America/New_York
- AGENTS.md → dry-run before send; stop and ask if recipient is ambiguous
- SOUL.md → concise, no corporate filler

**Must gather at runtime:**
- User's explicit request (e.g. "send weather to my email")
- Current weather data (wttr.in or web_fetch)
```

#### B. Must gather at runtime

Anything not in the bootstrap files: user message, live API data, file paths, dates, confirmation flags. Be explicit so the agent does not guess.

---

### 3. What does good output look like?

Define **format**, **destination**, and **how you know it worked**.

| Dimension | Define clearly |
|-----------|----------------|
| **Format** | Structure: bullets, subject line, emoji use, max length, markdown vs plain text per channel |
| **Destination** | Where the result goes: Telegram reply, Gmail to USER.md email, `memory/YYYY-MM-DD.md`, cron channel, file path |
| **Success** | Observable proof: API response ID, `memory_search` hit, user confirmation, exit code 0 on dry-run then live run |

**Example output block for a skill:**

```markdown
## Output

**Format:** Short Telegram message or email with location, temp, conditions, one-line outlook; emoji optional, no markdown tables on Telegram.

**Destination:**
- Default: reply in current Telegram chat
- If asked to email: send to address from USER.md via `GMAIL_SEND_EMAIL`

**Success criteria:**
- Weather data fetched (non-empty wttr.in response)
- If emailing: Composio dry-run passes, then send returns message ID
- Log summary in `memory/YYYY-MM-DD.md` when action was user-initiated and non-trivial
```

---

## Skill file template

Use this skeleton for every new `skills/<name>/SKILL.md`:

```markdown
---
name: skill-name
description: One sentence — what this skill does.
---

# Skill Name

> One sentence — what this skill does.

## Input

**From bootstrap:**
- IDENTITY.md → …
- SOUL.md → …
- AGENTS.md → …
- USER.md → …
- TOOLS.md → …

**Gather at runtime:**
- …

## Output

**Format:** …

**Destination:** …

**Success criteria:** …

## Procedure

1. …
2. …
```

---

## Checklist before merging a skill

- [ ] **One-sentence purpose** in `description` and body opening
- [ ] **Input** lists bootstrap references (by file + field) and runtime gathers
- [ ] **Output** specifies format, destination, and success criteria
- [ ] Skill does not contradict AGENTS.md red lines (privacy, stop-and-ask)
- [ ] Skill does not duplicate TOOLS.md — it points to the right tool slugs/commands
- [ ] Tested once: dry-run where applicable, then verify success criteria

---

## Related

- Workspace skills directory: `skills/`
- Local tool notes: [TOOLS.md](./TOOLS.md)
- Operating rules: [AGENTS.md](./AGENTS.md)
