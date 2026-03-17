# Brag Writer

A Claude Code skill for senior product designers who want to document their work as it happens — and turn it into something useful when it counts.

Built around a simple idea: the best time to capture an achievement is right after it happened, not three weeks before your performance review.

---

## What it does

Brag Writer is an agent system with three parts that work together.

**Context Agent** sets up your workspace once. You give it your company's skill matrix — or describe what good performance looks like at your level and what your target role requires. It builds the lens every other agent uses to evaluate and classify your work.

**Capture Agent** is the one you talk to most. Tell it what you did. It opens with the SAR framework (Situation, Action, Result) so you know what to share, then asks follow-up questions about anything missing. It never invents details — everything in the final entry comes from you. Once you approve the draft, it saves the entry and asks what project it belongs to if relevant.

**Compiler Agent** reads all your saved entries across all buckets and produces a clean, readable brag document grouped by project and category. Run it any time you want to see where you stand.

---

## What the output looks like

### Without the skill

Most designers reconstruct their work from memory at review time. The result is vague, undersells the real impact, and misses things entirely.

> *"I worked on the map feature and helped with some research. I also wrote some docs for the design system."*

### With the skill

Each achievement is captured at the time it happened, in your own words, with real context.

```markdown
# Brag Document
**Senior Product Designer → Staff Product Designer**
**Verizon Connect** · Analytics Team
**Last updated:** March 2025

## Projects

### Map Clustering Initiative
*March 2025 – ongoing*

#### Ran usability sessions to validate the clustering approach
**Competency:** Craft & Methods

**Situation**
The team was split on whether to cluster map pins by proximity or by job
type. No user data existed to support either direction.

**Action**
I designed and ran 6 usability sessions with fleet managers across two
customer segments. I wrote the research plan, recruited participants
through the CS team, and synthesised findings into a decision brief.

**Result**
The brief aligned the team on job-type clustering within a week. It also
surfaced a secondary finding about label density that fed into the next sprint.
```

That's something you can hand to your manager, drop into a self-assessment, or use to prep for a promotion conversation.

---

## How to use it

Once installed, open Claude Code in your brag doc directory.

### Commands

| Command | What it does |
|---|---|
| `/setup-brag` | First time setup — initializes your workspace and ingests your skill matrix |
| `/brag` | Log a new achievement — opens the SAR framework and captures the entry |

### Or use natural language

**First time setup:**
```
/setup-brag
```

**Log an achievement:**
```
/brag
```
Or just describe what you did — the skill picks it up.

**Generate your brag doc:**
```
compile my brag doc
```

---

## Installation

### Recommended — clone from GitHub

Pick a stable directory for the skill and run:

```bash
mkdir -p ~/.claude/skills/brag-writer
git clone https://github.com/[your-username]/brag-writer.git ~/.claude/skills/brag-writer
```

*GitHub URL will be updated once the repo is live.*

### Manual install

Download the skill files and copy them into your Claude Code skills directory:

```bash
# Create the skill directories
mkdir -p ~/.claude/skills/brag-writer/agents
mkdir -p ~/.claude/skills/brag-writer/templates

# Copy files into place
cp SKILL.md ~/.claude/skills/brag-writer/
cp agents/context-agent.md ~/.claude/skills/brag-writer/agents/
cp agents/capture-agent.md ~/.claude/skills/brag-writer/agents/
cp agents/compiler-agent.md ~/.claude/skills/brag-writer/agents/
cp templates/entry-template.md ~/.claude/skills/brag-writer/templates/
```

### Where to run it

The skill creates a `brag-YYYY/` folder in whatever directory Claude Code is running from. Pick a stable directory so your entries persist across sessions:

```bash
# Navigate to your preferred home for the brag doc
cd ~/Documents/career   # or wherever makes sense for you
claude                  # open Claude Code here
```

Everything — entries, your skill matrix, and your compiled brag doc — will live inside `~/Documents/career/brag-2025/`.

A new year folder is created automatically when you run setup in a new year. Previous years are never touched.

---

## Pairs well with

[humanizer](https://github.com/blader/humanizer) — run a humanizer pass on your compiled brag doc to catch any lingering AI writing patterns before sharing it.

```bash
git clone https://github.com/blader/humanizer.git ~/.claude/skills/humanizer
```

---

## File structure

```
~/.claude/skills/brag-writer/
    SKILL.md
    agents/
        context-agent.md
        capture-agent.md
        compiler-agent.md
    templates/
        entry-template.md

[your working directory]/
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

## Design principles

**Never fabricate.** Every word in every entry comes from you. The agent asks questions, proposes drafts, and waits for your approval. Nothing is saved without your sign-off.

**Qualitative results count.** Not every achievement has a metric. "The doc became the go-to reference" is a complete result. The skill never pushes you to invent a number.

**Current role and target role.** The skill matrix captures where you are and where you're headed. Your achievements get classified against both — so the brag doc works as a career conversation artifact, not just a log.

**Entries are the source of truth.** The brag doc is always regenerated from your markdown entry files. You never edit the doc directly — you add entries and recompile.

**Your work lives in buckets.** Not everything is a project. Standalone wins, influence, learning, and outside work all have their own space.

---

## V1 scope

This is V1. The system captures, classifies, and compiles. A few things are intentionally left for later:

- Performance review narrative (too company-specific to get right generically)
- Updating pending results (needs its own interaction pattern)
- Resume export format

---

Built with Claude Code. Inspired by [Julia Evans' brag document](https://jvns.ca/blog/brag-documents/) and [Jeff Humble's designer-specific take](https://www.thefountaininstitute.com/blog/brag-documents).
