# Guide for Humans

## Quick Start

**First session** - tell the agent to read the system:
```
Please read ai-agent/meta/CORE.md - this explains our workflow system.
```

**After context loss** (agent crashed/closed):
```
Please read ai-agent/meta/CORE.md, then >>continue
```

That's it. The agent handles the rest.

---

## TL;DR Commands

**Setup** (first time):
- `>>init-knowledge` - Set up project knowledge
- `>>scan-repo` - Scan codebase and create maps

**Regular Work**:
- `>>start [TYPE] name` - Start new work (feat/maint/bug/concept)
- `>>continue` - Resume work
- `>>wrap` - End session
- `>>pause` - Pause work with full context
- `>>status` - Quick status check
- `>>test` - Start testing phase
- `>>checkpoint` - Capture knowledge mid-session

**Concept Work** (complex planning):
- `>>start concept name` - Start concept work
- `>>add-input [path]` - Add input sources
- `>>extract` - Process inputs
- `>>conceptualize` - Build concept
- `>>plan` - Generate work plan
- `>>roadmap` - Generate roadmap
- `>>finalize` - Complete and promote

---

## Work Types

| Type | Prefix | Use For |
|------|--------|---------|
| Feature | `feat` | New functionality, enhancements |
| Maintenance | `maint` | Dependency updates, refactoring, security |
| Bug | `bug` | Bug fixes |
| Concept | `concept` | Complex planning, work plans, roadmaps |

**Examples**:
```
>>start feat user-notifications
>>start maint deps-update
>>start bug login-timeout
>>start concept new-platform
```

---

## Project Structure

```
project-root/ai-agent/
├── meta/                    ← System docs (you're reading these)
│   ├── CORE.md             ← Agent reads this every session
│   ├── protocols/          ← Detailed command protocols
│   ├── reference/          ← Glossary, conventions
│   └── templates/          ← Document templates
├── work/                    ← Active work items
│   ├── 001-feat-login/
│   ├── 002-maint-deps/
│   └── 003-concept-platform/
├── concepts/                ← Finalized concepts
├── workplans/               ← Finalized work plans
└── knowledge/               ← Project knowledge base
```

---

## Typical Workflow

### 1. Start New Work
```
Human: >>start feat user-notifications
AI: Creates folder, asks questions
Human: Answers questions
AI: Creates implementation plan
Human: Approves plan
AI: Starts implementation
```

### 2. Continue Work
```
Human: >>continue
AI: Reads SSOT, summarizes state
    Work: User Notifications (feat)
    Status: Phase 2 - Backend API
    Next: Implement NotificationService

    Ready to continue?
Human: Yes
AI: Continues work
```

### 3. End Session
```
Human: >>wrap
AI: Updates progress log, sets next task
    Session complete.
    Next session: Continue Phase 3
```

### 4. Pause Work (mid-task interruption)
```
Human: >>pause urgent meeting
AI: Captures full context for resumption
    Work paused. Resume with >>continue
```

---

## Key Documents

Each work item has a folder with these documents:

| Document | Purpose |
|----------|---------|
| 00-OVERVIEW.md | **SSOT** - status, navigation, quick context |
| 01-REQUIREMENTS.md | What to build (features/bugs) |
| 01-SCOPE.md | What's included (maintenance) |
| 02-IMPLEMENTATION-PLAN.md | How to build |
| 03-PROGRESS-LOG.md | Session log (append-only) |
| 04-TESTING-CHECKLIST.md | Test scenarios |

**SSOT = Single Source of Truth** - Agent reads this first every session

---

## Knowledge System

The knowledge system helps agents understand your project:

```
ai-agent/knowledge/
├── SYSTEM-OVERVIEW.md      ← Project basics
├── REPOSITORY-MAP.md       ← Directory structure
├── CONCEPTS-INDEX.md       ← Patterns, APIs, models
├── COMMANDS.md             ← Project commands
└── subsystems/             ← Deep subsystem docs
```

**Setup** (optional but recommended):
```
>>init-knowledge    ← Answer questions about your project
>>scan-repo         ← Agent maps the codebase
```

Agent automatically reads and updates knowledge during work.

---

## Concept Workflow

For complex planning work that produces work plans and roadmaps:

```
GATHER → EXTRACT → CONCEPTUALIZE → PLAN → ROADMAP → FINALIZE
```

1. `>>start concept name` - Create concept work item
2. `>>add-input [path]` - Add documents, URLs, conversations
3. `>>extract` - Process inputs into structured data
4. `>>conceptualize` - Build concept with sub-concepts
5. `>>plan` - Generate work plan (agent asks format first)
6. `>>roadmap` - Create dependency map with visualizations
7. `>>finalize` - Promote to `concepts/` and `workplans/` folders

**Refinement**: Use `>>refine [phase]` to re-enter at any phase

---

## Best Practices

### Do ✅
- Use `>>` commands - agent knows exactly what to do
- Test after each phase - catch issues early
- Use `>>wrap` at end of sessions - preserves context
- Use `>>checkpoint` in long sessions - captures knowledge
- Check OVERVIEW when confused - it's the SSOT

### Don't ❌
- Give vague feedback - be specific
- Skip testing until the end
- Leave old work items around - use `>>archive`
- Assume agent remembers - each session reads SSOT

---

## Troubleshooting

| Problem | Solution |
|---------|----------|
| Too many files in work/ | Use `>>archive` for completed work |
| Don't know what to work on | Use `>>status` |
| Agent seems confused | Say `>>continue` (re-reads SSOT) |
| Tests failing | Use `>>bug` for each failure |
| Long session, worried about context | Use `>>checkpoint` |

---

## System Documentation

| File | Purpose | Who |
|------|---------|-----|
| [CORE.md](CORE.md) | Agent's core instructions | Agent reads every session |
| [protocols/](protocols/) | Detailed command protocols | Agent reads on-demand |
| [reference/](reference/) | Glossary, conventions | Agent consults as needed |
| [templates/](templates/) | Document templates | Agent copies for new work |
| FOR-HUMANS.md | This guide | You |

---

## Getting Help

- **About a command**: Check the agent - "What does >>test do?"
- **About documents**: Look in `meta/templates/`
- **About agent behavior**: Check `meta/CORE.md`
- **Still confused**: Ask the agent: "How does the workflow system work?"
