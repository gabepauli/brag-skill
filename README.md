# Brag

A Claude Code skill for individual contributors who want to document their work as it happens.

The best time to capture an achievement is right after it happened, not three weeks before your performance review.

---

## What it does

Brag has three agents.

**Context Agent** sets up your workspace once. You give it your company's skill matrix, or describe what good performance looks like at your level and what your target role requires. It saves that as the lens every other agent uses to classify your work.

**Capture Agent** is the one you talk to most. Tell it what you did. It shows you the SAR framework (Situation, Action, Result), asks follow-up questions about anything missing, and writes a draft for you to approve. Nothing gets saved until you confirm it.

**Compiler Agent** reads all your entries and produces a brag document grouped by project and category. Run it any time.

---

## Getting started with context

The first time you run Brag, it asks for your company's skill matrix — the competency framework used to evaluate performance at your level. That becomes the classification lens for every achievement you log.

If your company doesn't have a formal document, the agent asks you to describe what good performance looks like at your current level and what your target role requires. It builds the matrix from that.

The skill matrix records two things: your current role and your target role. Achievements get classified against both.

---

## What the output looks like

Most contributors reconstruct their work from memory at review time. The result undersells the real impact and misses things entirely.

> *"I worked on the checkout flow and helped the team ship some improvements. Also fixed some issues that came up in testing."*

With Brag, each achievement is logged at the time it happened.

```markdown
# Brag Document
**Senior Product Designer → Staff Product Designer**
**Company** · Growth Team
**Last updated:** April 2025

## Projects

### Checkout Flow Redesign
*February 2025 – April 2025*

#### Redesigned the guest checkout flow to reduce drop-off
**Competency:** Craft & Execution

**Situation**
Analytics showed a 34% drop-off at the account creation step in the
checkout flow. The team suspected the forced sign-up was the main cause
but had no qualitative data to back it up.

**Action**
I ran usability sessions with recent customers, mapped the friction
points, and proposed a guest checkout path as an alternative. I designed
the end-to-end flow, scoped it with the engineer to a two-week build,
and wrote the acceptance criteria.

**Result**
Guest checkout shipped in March. Drop-off at that step fell by 12%. The
usability findings also fed into a broader audit of the account creation
experience.
```

---

## How to use it

Open Claude Code in your brag doc directory and run `/brag`. If no workspace exists yet, the skill walks you through setup first.

**Log an achievement:**
```
/brag
```

**Generate your brag doc:**
```
compile my brag doc
```

---

## Installation

### Recommended — clone from GitHub

```bash
mkdir -p ~/.claude/skills/brag
git clone https://github.com/gabepauli/brag-skill.git ~/.claude/skills/brag
```

### Manual install

```bash
mkdir -p ~/.claude/skills/brag/agents
mkdir -p ~/.claude/skills/brag/templates

cp SKILL.md ~/.claude/skills/brag/
cp agents/context-agent.md ~/.claude/skills/brag/agents/
cp agents/capture-agent.md ~/.claude/skills/brag/agents/
cp agents/compiler-agent.md ~/.claude/skills/brag/agents/
cp templates/entry-template.md ~/.claude/skills/brag/templates/
```

### Where to run it

Navigate to a stable directory before opening Claude Code — that's where your brag folder will be created.

```bash
cd ~/Documents/career
claude
```

---

## How your work is stored

Brag creates a folder per year: `brag-2025/`, `brag-2026/`. Each year is separate and previous years are never touched. Inside, achievements sit in bucket folders by type. Each achievement is one markdown file, named by date. You can browse them in any file manager or open individual entries in any editor.

```
brag-2025/
    company-skill-matrix.md
    projects/
        [project-name]/
            YYYY-MM-[slug].md
    standalone-wins/
        YYYY-MM-[slug].md
    influence-and-collaboration/
        YYYY-MM-[slug].md
    learning-and-growth/
        YYYY-MM-[slug].md
    outside-work/
        YYYY-MM-[slug].md
    brag-doc.md
```

---

## Pairs well with

[humanizer](https://github.com/blader/humanizer) — catches lingering AI writing patterns in your compiled brag doc before you share it.

```bash
git clone https://github.com/blader/humanizer.git ~/.claude/skills/humanizer
```

---

Built with Claude Code. Inspired by [Julia Evans' brag document](https://jvns.ca/blog/brag-documents/) and [Jeff Humble's take on brag docs for designers](https://www.thefountaininstitute.com/blog/brag-documents).
