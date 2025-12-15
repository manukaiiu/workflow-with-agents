# Workflow System for AI Agents

**Purpose**: Structured system for managing development work (features, maintenance, bugs, concepts) with AI agents. Designed for minimal context usage while maintaining clear protocols.

## Architecture

The system uses a **hierarchical loading** approach to minimize context consumption:

```
meta/
├── CORE.md                ← Agent reads EVERY session (~165 lines)
├── protocols/             ← Agent reads ON-DEMAND when executing commands
│   ├── start.md
│   ├── continue.md
│   ├── wrap.md
│   ├── pause.md           ← NEW: Mid-task interruption
│   ├── checkpoint.md
│   ├── recovery.md        ← NEW: Context recovery
│   ├── test.md
│   ├── archive.md
│   ├── bug.md
│   ├── status.md
│   ├── init-knowledge.md
│   ├── scan-repo.md
│   └── concept/           ← Concept workflow protocols
│       ├── overview.md
│       ├── start-concept.md
│       ├── add-input.md
│       ├── extract.md
│       ├── conceptualize.md
│       ├── plan.md
│       ├── roadmap.md
│       ├── refine.md
│       ├── finalize.md
│       └── new-version.md
├── reference/             ← Agent consults AS NEEDED
│   ├── GLOSSARY.md
│   ├── FILE-CONVENTIONS.md
│   ├── WORK-TYPES.md
│   └── ANTI-PATTERNS.md
├── templates/             ← Agent copies for new work
│   ├── features/
│   ├── maintenance/
│   ├── concept/
│   └── knowledge/
├── FOR-HUMANS.md          ← Human guide
└── README.md              ← This file
```

### Loading Strategy

| Layer | When to Read | Size |
|-------|--------------|------|
| CORE.md | Every session | ~165 lines |
| protocols/*.md | When executing that command | ~50-100 lines each |
| reference/*.md | When clarification needed | Consult as needed |
| 00-OVERVIEW.md (work item) | When working on that item | ~50-80 lines |

**Typical session**: ~300 lines read vs. previous ~1700+ lines

---

## Quick Start

### For Humans
→ Read [FOR-HUMANS.md](FOR-HUMANS.md)

**First session**: Tell agent to read `ai-agent/meta/CORE.md`
**Commands**: `>>start`, `>>continue`, `>>wrap`, `>>pause`, `>>test`

### For AI Agents
→ Read [CORE.md](CORE.md) every session

Parse `>>` commands and read the corresponding protocol file.

---

## Project Structure (When Using This System)

```
project-root/ai-agent/
├── meta/                    ← System docs (this directory)
├── work/                    ← Active work items
│   ├── 001-feat-auth/
│   ├── 002-maint-deps/
│   └── 003-concept-platform/
├── concepts/                ← Finalized concepts
│   └── [name]/v1/
├── workplans/               ← Finalized work plans
│   └── [name]/v1/
└── knowledge/               ← Project knowledge base
    ├── SYSTEM-OVERVIEW.md
    ├── REPOSITORY-MAP.md
    ├── CONCEPTS-INDEX.md
    └── subsystems/
```

---

## Work Types

| Type | Prefix | Use For |
|------|--------|---------|
| Feature | `feat` | New functionality, enhancements |
| Maintenance | `maint` | Dependency updates, refactoring, security |
| Bug | `bug` | Bug fixes |
| Concept | `concept` | Complex planning, work plans, roadmaps |

---

## Commands Quick Reference

**Setup**:
- `>>init-knowledge` - Initialize project knowledge
- `>>scan-repo` - Map repository structure

**Work**:
- `>>start [TYPE] name` - Start new work
- `>>continue` - Resume work
- `>>wrap` - End session with handoff
- `>>pause [reason]` - Pause mid-task with context
- `>>status` - Quick status check
- `>>test` - Create test checklist
- `>>bug <description>` - Report and fix bug
- `>>archive` - Complete and archive work
- `>>checkpoint` - Mid-session knowledge capture

**Concept Workflow**:
- `>>start concept name` - Start concept work
- `>>add-input [path]` - Add input sources
- `>>extract` - Process inputs
- `>>conceptualize` - Build concept
- `>>plan` - Generate work plan
- `>>roadmap` - Create roadmap
- `>>refine [phase]` - Refinement cycle
- `>>finalize` - Promote to final folders

---

## Key Features

- **Hierarchical loading**: ~80% reduction in context usage
- **Self-sufficient work items**: OVERVIEW contains recovery context
- **Pause/Resume**: Full context capture for interruptions
- **Context recovery**: Explicit handling after summarization
- **Knowledge accumulation**: Insights persist across sessions
- **Concept workflow**: Full planning lifecycle with traceability
- **On-demand protocols**: Read only what you need

---

## Philosophy

1. **Load what you need**: Don't read everything every session
2. **SSOT per work item**: 00-OVERVIEW.md is the source of truth
3. **Append, don't recreate**: Progress log is append-only
4. **Self-sufficient documents**: Work items contain their own recovery context
5. **Explicit context recovery**: Handle summarization gracefully
6. **Knowledge accumulation**: Insights help future work

---

## Getting Started

1. Copy `meta/` folder to your project's `ai-agent/` directory
2. Tell agent: "Please read ai-agent/meta/CORE.md"
3. Start work: `>>start feat my-first-feature`

The agent creates `work/`, `knowledge/`, `concepts/`, and `workplans/` folders automatically.

---

## Success Metrics

- `>>continue` gets you working in < 2 minutes
- Agent reads ~300 lines per session (not 1700+)
- Work items are numbered: `NNN-TYPE-name`
- Progress logs show clear progression
- Knowledge docs stay updated

---

That's it. Simple, focused, scalable.
