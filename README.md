# Brag Writer

A Claude Code skill for senior product designers who want to document their work as it happens — and turn it into something useful when it counts.

Built around a simple idea: the best time to capture an achievement is right after it happens, not three weeks before your performance review.

---

## What it does

Brag Writer is an agent system with three parts that work together:

**Context Agent** sets up your workspace once. You give it your company's skill matrix (or describe what good performance looks like at your level) and it builds the lens every other agent uses to evaluate your work.

**Capture Agent** is the one you talk to most. Tell it what you did. It asks a few follow-up questions to pull out the situation, what you did, and what the result was. It never invents details — everything in the final entry comes from you. Once you approve the draft, it saves the entry and asks if it belongs to a project.

**Compiler Agent** reads all your saved entries and produces a clean, readable brag document grouped by project, ordered chronologically. Run it any time you want to see where you stand.

---

## What the output looks like

### Without the skill

Most designers reconstruct their work from memory at review time. The result is vague, undersells the real impact, and misses things entirely.

> *"I worked on the map feature and helped with some research. I also wrote some docs for the design system."*

### With the skill

Each achievement is captured at the time it happened, in your own words, with real context.

```markdown
## Map Clustering Initiative
*March 2025 – ongoing*

### Ran usability sessions to validate the clustering approach
**Competency:** Craft & Methods

**Situation:** The team was split on whether to cluster map pins by proximity
or by job type. No user data existed to support either direction.

**Action:** I designed and ran 6 usability sessions with fleet managers across
two customer segments. I wrote the research plan, recruited participants through
the CS team, and synthesised findings into a decision brief.

**Result:** The brief aligned the team on job-type clustering within a week.
It also surfaced a secondary finding about label density that fed directly
into the next sprint.
```

That's something you can hand to your manager, drop into a self-assessment, or use to prep for a promotion conversation.

---

## How to use it

Once installed, open Claude Code in any directory and start with one of these:

**First time setup:**
```
set up my brag doc
```

**Log an achievement:**
```
I want to brag about something
```
Or just describe what you did — the skill picks it up from context.

**Generate your brag doc:**
```
compile my brag doc
```

---

## Installation

### Recommended — clone from GitHub

Choose a directory where you want your skill to live and run:

```bash
mkdir -p ~/.claude/skills/brag-writer
git clone https://github.com/[your-username]/brag-writer.git ~/.claude/skills/brag-writer
```

*GitHub URL will be updated once the repo is live.*

### Manual install

Download or copy the skill files and place them in your Claude Code skills directory:

```bash
# Create the skill directory
mkdir -p ~/.claude/skills/brag-writer/agents

# Copy files into place
cp SKILL.md ~/.claude/skills/brag-writer/
cp agents/context-agent.md ~/.claude/skills/brag-writer/agents/
cp agents/capture-agent.md ~/.claude/skills/brag-writer/agents/
cp agents/compiler-agent.md ~/.claude/skills/brag-writer/agents/
```

### Where to run it

The skill creates a `.brag/` folder in whatever directory Claude Code is running from. Pick a stable home directory so your entries persist across sessions:

```bash
# Navigate to your preferred home for the brag doc
cd ~/Documents/career   # or wherever makes sense for you
claude                  # open Claude Code here
```

All your entries, your skill matrix, and your compiled brag doc will live in `~/Documents/career/.brag/`.

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
    SKILL.md                        ← orchestrator, routing, principles
    agents/
        context-agent.md            ← workspace setup, skill matrix
        capture-agent.md            ← SAR capture, classification
        compiler-agent.md           ← brag doc generation

[your working directory]/
    .brag/
        company-skill-matrix.md     ← your company's competency lens
        projects.md                 ← project index, grows over time
        entries/                    ← one YAML file per achievement
        brag-doc.md                 ← compiled output
```

---

## Design principles

**Never fabricate.** Every word in every entry comes from you. The agent asks questions, proposes drafts, and waits for your approval. Nothing is saved without your sign-off.

**Qualitative results count.** Not every achievement has a metric. "The doc became the go-to reference" is a complete result. The skill never pushes you to invent a number.

**The skill matrix is yours.** Every company measures performance differently. You bring your company's framework — the skill uses it as the lens to classify your work. No generic categories imposed on top.

**Entries are the source of truth.** The brag doc is always regenerated from your YAML entries. You never edit the doc directly — you add entries and recompile.

---

## V1 scope

This is V1. The system captures, classifies, and compiles. A few things are intentionally left for later:

- Performance review narrative (too company-specific to get right generically)
- Updating pending results (needs its own interaction pattern)
- Resume export format

---

Built with Claude Code. Inspired by [Julia Evans' brag document](https://jvns.ca/blog/brag-documents/) and [Jeff Humble's designer-specific take](https://www.thefountaininstitute.com/blog/brag-documents).
