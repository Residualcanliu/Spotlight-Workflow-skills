# Spotlight Workflow — A Personal Workflow Engine

> Not a prompt template. An operating system for how you think, execute, and learn — encoded into reusable skill files.

🌐 [中文](./README.md) · [English](./README_EN.md)

---

## How This System Works

```
User asks a question
    │
    ▼
┌──────────────────────────────────────────┐
│  Fast path check                          │
│  ≤ 20 chars or single file? → Just do it │
│  Multi-file / multi-step? → Full process  │
└──────────────────────┬───────────────────┘
                       │ (full process)
                       ▼
┌─────────────────┐                                         │
│  Review learn    │ ← Read last 3 summaries only,           │
│  (summary mode)  │    not full library. Auto-compress:     │
│                  │    >20 items → 5 core principles        │
└───────┬─────────┘                                         │
        ▼                                                   │
┌─────────────────┐                                         │
│  Decompose task  │ ← Reverse-engineer from the goal        │
│  (Spotlight way) │    Only deep-dive where attention goes  │
└───────┬─────────┘                                         │
        ▼                                                   │
┌─────────────────┐                                         │
│  Create TODOs    │ ← Default 3 items, 4+ for complex tasks │
│  (pick a template)│   Bug / Feature / Research / Doc / Review│
└───────┬─────────┘                                         │
        ▼                                                   │
┌─────────────────┐                                         │
│  Execute + Iterate│ ← Writing rules & pitfalls auto-apply  │
│  (build & refine)│    Present draft, leave room for iteration│
└───────┬─────────┘                                         │
        ▼                                                   │
┌─────────────────┐                                         │
│  Retrospective   │ ← Errors→Fixes, optimizations, insights │
│  (write to learn) │    ≤50 chars each, auto-compress at 20  │
└───────┬─────────┘                                         │
        │                                                   │
        └────────────────────────────────────────────────→ Retrieved on next task
```

> Fast path prevents noise. Summary mode prevents bloat. The learn directory is this system's long-term memory — you never pay tuition for the same mistake twice.

---

## Why "Spotlight"?

Most workflows tell you to break everything down before you start. Spotlight doesn't.

**A spotlight only illuminates where it's pointed.** When you get a task, start from the overall goal and work backwards to identify the major modules — but only deep-dive into the module the user is currently focused on. Modules they haven't asked about stay at a coarse-grained outline. Don't over-decompose prematurely.

This isn't laziness. It's respect for attention. Until the user sees a first draft, you don't know which details actually matter. Instead of guessing, build a draft and let the user's attention show you where to go next.

```
User's attention (the spotlight beam)
      │
      ▼
┌──────────────────┐
│  Deep dive here  │  ← The module they're looking at — decompose fully
└──────────────────┘
      │
      ▼
┌──────────────────┐
│  Coarse-grained  │  ← Everything else — stay at outline level
└──────────────────┘
```

---

## System Overview

```
/spotlight (single entry point)
      │
      ├─ Short / single-file? → Fast path: just do it
      │
      ├─ Complex task? → Review learn → Decompose → TODO → Execute → Retro
      │
      └─ No task? → Check installation status
                      │
                 ┌────┴────┐
           Installed    Not installed → guided setup → learn + claudework
                 │                        │
          Load full config           Or lightweight mode
                 │                  (thinking only)
                 ▼
    ┌─────────────────────────────────────┐
    │          Spotlight Engine            │
    │                                     │
    │  🔦 Attention-driven decomposition  │
    │  ⚡ Fast path: skip ceremony for     │
    │     short/single-file requests       │
    │  📋 TODO-driven execution            │
    │  ✍️  Writing rules + style framework │
    │  🧠 Thinking pattern matching        │
    │  🕳️ Automatic pitfall prevention     │
    │  📝 Retrospective + auto-compression │
    │  🔗 Skill discovery + recommendations│
    └─────────────────────────────────────┘
```

---

## Commands

**You only need to remember one: `/spotlight`.** The system auto-detects your intent and routes accordingly.

| You say | System does |
|---------|-------------|
| `/spotlight write my report` | Execute task (fast path check → full process or quick action) |
| `/spotlight init` | Guided setup of learn + claudework |
| `/spotlight check` | Installation diagnostic report |
| `/spotlight toggle style` | Flip blended ↔ learn-only mode |
| `/spotlight` (no input) | Check status, suggest next steps |

Sub-commands (`/spotlight-init`, `/spotlight-work`, etc.) still exist but are optional.

---

## Thinking Model

### Top-Down Reverse Decomposition

Traditional approach: list all required components → refine each one → assemble. Spotlight reverses this: start from the overall goal → work backwards to identify major modules → only decompose the module under the user's current attention.

```
User says "build gesture recognition for smart glasses"
        │
        ▼
  Reverse-decompose from the goal
  ├── Hardware (camera + compute module)
  ├── Algorithm (gesture recognition model)
  └── System (capture → inference → output)
        │
        ▼
  User asks "what lightweight models are available?"
        │
        ▼
  Only deep-dive into the Algorithm layer
  Hardware and System stay at outline level
```

### TODO-Driven Execution (default: 3 items)

Every task analysis ends with a TODO list. Three items covers most cases — pick the template that matches your task type:

| Task type | TODO structure |
|-----------|---------------|
| Bug investigation | ①Locate the issue ②Trace the full chain ③Fix + verify |
| Feature development | ①Clarify scope ②Design implementation ③Define acceptance criteria |
| Research / evaluation | ①Define research question ②Compare candidates ③Recommend with rationale |
| Document writing | ①Define structure + scope ②Fill core content ③Review + tighten |
| Code review | ①Set review dimensions ②Audit item by item ③Rank by severity |

**Complex tasks can have 4+.** Multiple independent sub-systems, parallel workstreams, or extra verification phases all justify going beyond three. The rule: each TODO must earn its place — don't split to pad the list, don't merge to hit a number.

### Three-Level Drill-Down for Complex TODOs

```
Trunk (TODO)
  └── Branch (sub-steps)
        └── Leaf (concrete actions)
```

---

## Writing Style System

This is one of Spotlight's most distinctive features. Writing and expression are deeply personal — someone else's "good" isn't necessarily yours.

### Dual-Mode Design

| Mode | Style source | Best for |
|------|-------------|----------|
| **Blended** (default) | Spotlight built-in rules 50% + your personal style 50% | Daily use — structured but flexible |
| **Learn-Only** | Your personal style 100% | When you've accumulated enough style samples in learn |

Toggle with `/spotlight-style`.

### Three Iron Rules

1. **No parentheses for parameters** — `Adam, learning rate 0.0008` not `Adam(lr=0.0008)`
2. **No reflections in procedure steps** — steps describe what was done, not what was learned
3. **Results in a single paragraph** — one summary, not a per-scenario breakdown

### Five-Dimensional Style Framework

Analyze any reference text across five dimensions: overall structure → paragraph flow → language features → deviation from genre norms → one-sentence essence.

---

## Pitfall Prevention: Errors as Knowledge

Every entry in this list comes from a real failure — symptom, root cause, and fix, all present:

| Pitfall | Symptom | Fix |
|---------|---------|-----|
| ASCII double-quotes in officecli batch JSON | Parse error: `'C' is invalid after a value` | Use square brackets for Chinese quotes |
| Position-index paragraph addressing | Offsets shift after insert/delete | Use stable paraId |
| Using Edit on mixed Chinese/English files | old_string match fails | Use Write for full overwrite |
| Using `python3` on Windows | Exit code 49 | Always use `python` |
| Editing paragraphs one-by-one | Hard to locate mid-batch errors | Build batch JSON, submit at once |
| Editing without checking image positions | Accidentally overwriting paragraphs with images | Always run `officecli query image` first |
| sed low→high replacement order | Chain-overwrite, values skip levels | Replace high values first, low values last |
| Side effects inside useMemo | Shader uniforms don't update | Use useEffect for side effects |

Full list: [SKILL.md §4](./SKILL.md).

---

## Retrospective System: Never Pay Tuition Twice

Every completed project gets a structured retrospective. Anti-bloat rules:

- **Each lesson ≤ 50 chars**: just enough to capture symptom → fix
- **Auto-compress at 20 items**: merge into 5 core principles
- **Only read last 3 summaries**: before next task — don't load the whole library

```
learn/
├── YYYY-MM-DD-project-name.md    ← structured retrospective
├── YYYY-MM-DD-project-name.md    ← auto-compressed at 20 items
├── ...
└── archive/                      ← old files archived at 30+
```

You don't fall into the same hole twice — and the library doesn't become a bloated black hole.

---

## Installation

```bash
# 1. Copy to Claude Code skills directory
cp -r spotlight/ spotlight-init/ spotlight-work/ spotlight-check/ spotlight-learn/ spotlight-style/ ~/.claude/skills/

# 2. Type /spotlight to begin
# First run will guide you through setting up learn (retrospective library)
# and claudework (project workspace) locations
```

---

## Skill Discovery

Spotlight automatically detects and invokes related installed skills during tasks:

| Scenario | Paired skill |
|----------|-------------|
| Word document editing | `officecli` |
| Presentation creation | `ppt-master` |
| Academic writing / polishing | `nature-writing`, `nature-polishing` |
| Code review | `code-review` |
| Project initialization | `init` |

After each task, Spotlight checks if any uninstalled skills could have helped — and recommends them.

---

## License

Personal use. This isn't an open-source project — it's an operating system for a way of working.

---

> **Last updated:** 2026-06-28 · **Version:** v2.6
>
> Fast path · Single entry · Learn compression. Grown from real failures and iterations. Not designed — evolved.
