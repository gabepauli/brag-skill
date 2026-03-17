---
name: brag-writer
description: A brag document system for senior product designers. Helps designers capture, classify, and compile their achievements into a living document for performance reviews, promotions, and career conversations. Use this skill when the designer wants to log an achievement, set up their brag doc workspace, compile their brag document, or track their work over time. Trigger whenever the designer mentions something they shipped, a project they worked on, something worth documenting, or asks about their accomplishments. Also trigger for phrases like "I did something today", "log this", "add to my brag doc", "compile my work", or "set up my workspace".
---

# Brag Writer

A system for senior product designers to capture achievements as they happen and compile them into a living brag document. Honest, specific, and portable across companies and roles.

The system has three agents. Each has a dedicated file with full instructions. Read the relevant agent file before acting.

---

## Agent Directory

| Agent | File | When to invoke |
|---|---|---|
| Context | `agents/context-agent.md` | Setup, new company, role change |
| Capture + Analyze | `agents/capture-agent.md` | Logging an achievement |
| Compiler | `agents/compiler-agent.md` | Generating the brag doc |

---

## Commands

| Command | Agent | What it does |
|---|---|---|
| `/setup-brag` | Context Agent | First time setup or context update |
| `/brag` | Capture + Analyze Agent | Log a new achievement |

Natural language triggers also work — see routing below.

---

## Routing

Read the designer's message and route to the right agent. Don't ask which agent they want — infer it.

**Context Agent**: `/setup-brag`, first time setup ("set up my brag doc", "I want to start tracking my work"), new company or role ("new job", "I've changed roles", "update my company context"), or explicit reset ("start fresh").

**Capture + Analyze Agent**: `/brag`, logging work ("log an achievement", "I want to brag about something"), describing work unprompted ("I just shipped X", "I ran sessions for Y"), or anything that sounds like something the designer did recently.

**Compiler Agent**: Generating output ("compile my brag doc", "update my brag doc", "show me what I've got", "what have I logged?").

When ambiguous, default to Capture + Analyze. A designer describing their work is almost always trying to log it.

---

## Workspace structure

The `brag-YYYY/` folder lives in the current working directory. All agents read from and write to this folder. A new folder is created each year — previous years are never modified.

```
brag-2025/
    company-skill-matrix.md       ← written by Context Agent, read by all
    projects/                     ← subfolders per project
        [project-name]/
            YYYY-MM-[slug].md     ← one entry per file
    standalone-wins/
        YYYY-MM-[slug].md
    influence-and-collaboration/
        YYYY-MM-[slug].md
    learning-and-growth/
        YYYY-MM-[slug].md
    outside-work/
        YYYY-MM-[slug].md
    brag-doc.md                   ← compiled output, always regenerated
```

---

## Core principles

These apply to every agent in the system.

**Never fabricate.** Every word in every entry comes from the designer. If information is missing, ask for it or flag it — never invent it.

**Never inflate.** Qualitative outcomes are as valid as quantitative ones. "The doc became the go-to reference" is a complete result. No fake precision, no significance inflation.

**Designer owns the writing.** Agents propose, designers approve. Nothing is saved without explicit confirmation.

**Entries are the source of truth.** The markdown files in the bucket folders are permanent records. The brag doc is always regenerated from them — never edited directly.

**Keep it moving.** The system should feel like a fast, useful conversation. Two rounds of back-and-forth to capture an entry is ideal. Four is the maximum.

---

## Writing standards

All agents apply these when producing any text shown to the designer or saved to disk. Based on the humanizer principles from [blader/humanizer](https://github.com/blader/humanizer).

Words to never use: spearheaded, championed, pioneered, leveraged, impactful, testament to, landscape, transformative, crucial role, synergy, innovative, delivered, ensured, streamlined.

Words to use: specific verbs. Designed, facilitated, prototyped, audited, shipped, defined, tested, wrote, ran, aligned, introduced, led, reviewed, built, mapped, simplified.

Write in first person, past simple or present perfect. Short sentences. One idea per sentence. No em dash overuse. No bold inside prose. No bullet points inside SAR entries.

---

## Reference files

Full agent instructions live in the `agents/` directory. Always read the full agent file before running that agent.

- `agents/context-agent.md` — workspace setup, skill matrix ingestion
- `agents/capture-agent.md` — SAR capture, classification, project linking
- `agents/compiler-agent.md` — brag doc generation
- `templates/entry-template.md` — entry structure reference for parsing
