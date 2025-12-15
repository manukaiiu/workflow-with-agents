# Workflow System Core

**Read this file every session.** It's your mental model and navigation guide.

---

## Mental Model

You're working with a structured documentation system for human-AI collaboration.
- **Work** happens in numbered folders (`ai-agent/work/NNN-type-name/`)
- **Documents** track state (00-OVERVIEW.md is always the source of truth)
- **Commands** (`>>command`) trigger protocols in `protocols/` folder
- **Knowledge** accumulates in `ai-agent/knowledge/`

---

## Work Types

| Type | Prefix | When to Use |
|------|--------|-------------|
| feature | `feat` | New functionality, enhancements |
| maintenance | `maint` | Updates, refactoring, security audits |
| bug | `bug` | Fixing defects |
| concept | `concept` | Complex planning, analysis, roadmaps |

Folder naming: `NNN-TYPE-name` (e.g., `001-feat-user-auth`, `002-concept-platform`)

---

## Commands → Protocols

When you see these commands, read the linked protocol file:

### Core Commands
| Command | Protocol | Purpose |
|---------|----------|---------|
| `>>start [type] name` | [protocols/start.md](protocols/start.md) | Begin new work |
| `>>continue` | [protocols/continue.md](protocols/continue.md) | Resume work |
| `>>wrap` | [protocols/wrap.md](protocols/wrap.md) | End session |
| `>>checkpoint` | [protocols/checkpoint.md](protocols/checkpoint.md) | Mid-session knowledge save |
| `>>pause` | [protocols/pause.md](protocols/pause.md) | Interrupt work with context |
| `>>status` | (inline below) | Quick status check |
| `>>test` | [protocols/test.md](protocols/test.md) | Create test checklist |
| `>>archive` | [protocols/archive.md](protocols/archive.md) | Complete and archive work |

### Concept Commands
Read [protocols/concept/overview.md](protocols/concept/overview.md) first, then specific phase:

| Command | Protocol | Phase |
|---------|----------|-------|
| `>>start concept name` | [protocols/concept/gather.md](protocols/concept/gather.md) | Gather inputs |
| `>>add-input` | [protocols/concept/gather.md](protocols/concept/gather.md) | Add input source |
| `>>extract` | [protocols/concept/extract.md](protocols/concept/extract.md) | Process inputs |
| `>>conceptualize` | [protocols/concept/conceptualize.md](protocols/concept/conceptualize.md) | Build concept |
| `>>plan` | [protocols/concept/plan.md](protocols/concept/plan.md) | Generate work plan |
| `>>roadmap` | [protocols/concept/roadmap.md](protocols/concept/roadmap.md) | Create roadmap |
| `>>refine` | [protocols/concept/refine.md](protocols/concept/refine.md) | Refinement cycle |
| `>>finalize` | [protocols/concept/finalize.md](protocols/concept/finalize.md) | Promote to top-level |

### Knowledge Commands
| Command | Protocol | Purpose |
|---------|----------|---------|
| `>>init-knowledge` | [protocols/init-knowledge.md](protocols/init-knowledge.md) | Setup knowledge base |
| `>>scan-repo` | [protocols/scan-repo.md](protocols/scan-repo.md) | Map codebase |

---

## Session Start Protocol

**Every session, do this:**

1. **Check work index** (if exists): Read `ai-agent/work/WORK-INDEX.md` for overview
2. **Or list work folders**: `ls ai-agent/work/`
3. **If active work exists**: Read that work item's `00-OVERVIEW.md`
4. **The OVERVIEW tells you**:
   - Current phase and status
   - What to do next
   - Which protocol file to read

**No active work?** Wait for human to specify what to do.

---

## Context Recovery

**If your context was summarized/compressed, or you're a new agent continuing work:**

1. Check `git status` (uncommitted changes?)
2. List work folders: `ls ai-agent/work/`
3. Read active work item's `00-OVERVIEW.md`
4. Read last entry in progress log (03-PROGRESS-LOG.md or 06-PROGRESS-LOG.md)
5. If OVERVIEW has "Pause Context" section → follow its resume steps
6. **Confirm with human** before proceeding

For detailed recovery: [protocols/recovery.md](protocols/recovery.md)

---

## Quick Reference

### Status Codes
| Symbol | Meaning |
|--------|---------|
| `[ ]` | Not started / Pending |
| `[~]` | In progress |
| `[x]` | Complete |
| `[P]` | Paused |

### Extraction IDs (Concept Work)
| ID | Meaning |
|----|---------|
| T | Theme |
| R | Requirement |
| C | Constraint |
| S | Stakeholder |
| D | Decision |
| A | Ambiguity |

Full details: [reference/GLOSSARY.md](reference/GLOSSARY.md)

### File Numbers
| Range | Purpose |
|-------|---------|
| 00-09 | Core template documents |
| 10-89 | Work-item specific |
| 90-99 | Outputs, deliverables |

---

## >>status (Inline Protocol)

Quick status check - no file changes:

1. Read `00-OVERVIEW.md`
2. Read `02-IMPLEMENTATION-PLAN.md` (count completed phases)
3. Report:
   ```
   Work: [Name] ([type])
   Progress: [X]% ([Y] of [Z] phases)
   Current Phase: [Name]
   Next: [task from progress log]
   ```

---

## Core Principles

1. **SSOT**: `00-OVERVIEW.md` is truth for each work item
2. **Append-only**: Progress logs grow, never rewrite history
3. **Self-sufficient**: Work items contain their own resume context
4. **On-demand loading**: Read protocol files only when executing that command
5. **Checkpoint often**: Capture knowledge before context loss
6. **Confirm major changes**: Ask before refactoring or large changes
7. **Work in work items**: Create/edit outputs in `work/` folder, promote via `>>finalize`

## Output Location Rules

**Where do I create/edit files?**

| Situation | Location | Why |
|-----------|----------|-----|
| Active work on a work item | `work/NNN-TYPE-name/` | Keep work contained |
| Deliverables from work item | `work/NNN-TYPE-name/90-OUTPUTS/` | Track with work item |
| Finalizing concept/workplan | Use `>>finalize` protocol | Controlled promotion |
| User asks to edit finalized output | **Ask first**: "Edit in place, or create new version?" | Protect finalized work |
| User asks to create file outside work item | **Confirm location** with user | Avoid accidental bypass |

**Key rule**: If there's an active work item, outputs belong there until finalized.

---

## Natural Language → Commands

When human says these phrases, treat as the corresponding command:

| Human Says | Treat As |
|------------|----------|
| "let's start...", "create a new..." | `>>start` |
| "continue", "resume", "keep going" | `>>continue` |
| "wrap up", "end session", "that's it for now" | `>>wrap` |
| "pause", "stop here", "need to interrupt" | `>>pause` |
| "what's the status" | `>>status` |
| "we're done", "finalize", "complete this" | `>>finalize` (concept) or `>>archive` (other) |

---

## Need More Detail?

| Topic | Read |
|-------|------|
| Starting any work | [protocols/start.md](protocols/start.md) |
| Concept workflow overview | [protocols/concept/overview.md](protocols/concept/overview.md) |
| File naming conventions | [reference/FILE-CONVENTIONS.md](reference/FILE-CONVENTIONS.md) |
| Where to create/edit files | [reference/OUTPUT-LOCATIONS.md](reference/OUTPUT-LOCATIONS.md) |
| Jira ticket structure | [reference/TICKET-TEMPLATES.md](reference/TICKET-TEMPLATES.md) |
| All extraction ID meanings | [reference/GLOSSARY.md](reference/GLOSSARY.md) |
| Work type comparison | [reference/WORK-TYPES.md](reference/WORK-TYPES.md) |

---

## Folder Structure

```
ai-agent/
├── meta/                    ← You are here (system docs)
│   ├── CORE.md             ← This file (read every session)
│   ├── protocols/          ← Command details (read on-demand)
│   ├── reference/          ← Conventions, glossary (consult when needed)
│   └── templates/          ← Document templates
├── inbox/                   ← Staged inputs before work items exist
│   ├── INBOX.md            ← Index of staged inputs
│   └── [files]/            ← Staged input files
├── work/                    ← Active work items
│   ├── WORK-INDEX.md       ← Index of all work items (optional but helpful)
│   ├── 001-feat-name/
│   └── 002-maint-name/
├── concepts/                ← Finalized concepts (after >>finalize)
├── workplans/               ← Finalized work plans (after >>finalize)
└── knowledge/               ← Project knowledge base
```

---

*This is your navigation hub. Keep it open, reference the protocol links as needed.*
