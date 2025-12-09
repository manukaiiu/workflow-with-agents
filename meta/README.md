# Meta Documentation System

**Purpose**: Streamlined system for managing development work (features, maintenance, bugs, concepts) and project knowledge with AI assistance.

## What's Here

```
meta/
├── README.md              ← You are here (overview)
├── FOR-HUMANS.md          ← Human guide + meta-instructions
├── FOR-AGENTS.md          ← Agent protocol + workflows
└── templates/
    ├── features/          ← Feature/bug templates
    │   ├── 00-OVERVIEW.md
    │   ├── 01-REQUIREMENTS.md
    │   ├── 02-IMPLEMENTATION-PLAN.md
    │   ├── 03-PROGRESS-LOG.md
    │   ├── 04-TESTING-CHECKLIST.md
    │   ├── 05-ANALYSIS.md         ← Optional
    │   └── 06-PR-MESSAGE.md       ← Optional
    ├── maintenance/       ← Maintenance templates
    │   ├── 00-OVERVIEW.md
    │   ├── 01-SCOPE.md
    │   ├── 02-IMPLEMENTATION-PLAN.md
    │   ├── 03-PROGRESS-LOG.md
    │   └── 04-TESTING-CHECKLIST.md
    ├── concept/           ← Concept workflow templates
    │   ├── 00-OVERVIEW.md
    │   ├── 01-INPUTS-INDEX.md
    │   ├── 02-EXTRACTIONS.md
    │   ├── 03-CONCEPT.md
    │   ├── 03-CONCEPT-SUBCONCEPT.md
    │   ├── 04-WORKPLAN.md
    │   ├── 04-WORKPLAN-JIRA.md
    │   ├── 05-ROADMAP.md
    │   ├── 05-ROADMAP-MERMAID.md
    │   ├── 06-PROGRESS-LOG.md
    │   ├── 07-REFINEMENT-LOG.md
    │   └── 08-OPEN-QUESTIONS.md
    └── knowledge/         ← Project knowledge templates
        ├── SYSTEM-OVERVIEW.md
        ├── REPOSITORY-MAP.md
        ├── CONCEPTS-INDEX.md
        ├── COMMANDS.md
        └── subsystems/TEMPLATE.md
```

## Quick Start

### For Humans
→ Read `FOR-HUMANS.md` (5 minutes)

**Starting new work**: Say `>>start [TYPE] name` (TYPE: feat/maint/bug/concept)
**Continuing work**: Say `>>continue`
**Ending session**: Say `>>wrap`
**Mid-session checkpoint**: Say `>>checkpoint`

### For AI Agents
→ Read `FOR-AGENTS.md` when human points you to it

Parse meta-instructions (like `>>start`, `>>continue`, `>>wrap`)
Follow the protocols defined there

## Full Project Structure

When using this system, your project will be organized like this:

```
project-root/
└── ai-agent/
    ├── meta/                           ← This directory (system docs & templates)
    ├── work/                           ← Active work (created by agent)
    │   ├── 001-feat-user-auth/         ← Feature work
    │   │   ├── 00-OVERVIEW.md
    │   │   ├── 01-REQUIREMENTS.md
    │   │   ├── 02-IMPLEMENTATION-PLAN.md
    │   │   ├── 03-PROGRESS-LOG.md
    │   │   ├── 04-TESTING-CHECKLIST.md
    │   │   ├── 05-ANALYSIS.md          ← Optional
    │   │   └── 06-PR-MESSAGE.md        ← Optional
    │   ├── 002-maint-deps-update/      ← Maintenance work
    │   │   └── [maintenance documents]
    │   ├── 003-bug-login-fix/          ← Bug fix work
    │   │   └── [feature documents]
    │   └── 004-concept-platform/       ← Concept work (during creation)
    │       ├── 00-OVERVIEW.md
    │       ├── 01-INPUTS/INDEX.md
    │       ├── 02-EXTRACTIONS.md
    │       ├── 03-CONCEPT.md
    │       └── [other concept docs]
    ├── concepts/                       ← Finalized concepts (after >>finalize)
    │   └── [name]/v1/
    │       ├── CONCEPT.md
    │       └── CONCEPT-[sub].md
    ├── workplans/                      ← Finalized work plans (after >>finalize)
    │   └── [name]/v1/
    │       ├── WORKPLAN.md
    │       ├── ROADMAP.md
    │       └── ROADMAP.mermaid.md
    └── knowledge/                      ← Project knowledge (created by agent)
        ├── SYSTEM-OVERVIEW.md
        ├── REPOSITORY-MAP.md
        ├── CONCEPTS-INDEX.md
        ├── COMMANDS.md
        └── subsystems/
            └── [subsystem].md
```

**Note**: Only the `meta/` folder needs to be copied to your project. The agent automatically creates `work/`, `knowledge/`, `concepts/`, and `workplans/` folders as needed. Suggestion is to add an `ai-agent` folder (or similar), which is the new home of the `meta/` folder and the agent created folders and documents.

## Core Concepts

### Work Types
The system supports four work types:

| Type | Prefix | Use For |
|------|--------|---------|
| Feature | `feat` | New functionality, enhancements |
| Maintenance | `maint` | Dependency updates, refactoring, security audits |
| Bug | `bug` | Bug fixes |
| Concept | `concept` | Complex conceptualization, work plans, roadmaps |

Each work item gets a numbered folder: `NNN-TYPE-name` (e.g., `001-feat-user-auth`, `002-concept-platform`)

### Core Documents
All work types share these core documents:
- **00-OVERVIEW.md** - SSOT (Single Source of Truth)
- **02-IMPLEMENTATION-PLAN.md** - How to build it
- **03-PROGRESS-LOG.md** - Session log (append-only)
- **04-TESTING-CHECKLIST.md** - Test scenarios

Type-specific documents:
- **01-REQUIREMENTS.md** - For features/bugs
- **01-SCOPE.md** - For maintenance
- **05-ANALYSIS.md** - Optional feature research
- **06-PR-MESSAGE.md** - Optional PR draft

### Knowledge System
AI builds and maintains project knowledge to work more efficiently:

- **SYSTEM-OVERVIEW.md** - High-level project info (human or AI-filled)
- **REPOSITORY-MAP.md** - Directory structure and workflows
- **CONCEPTS-INDEX.md** - Patterns, APIs, models discovered
- **COMMANDS.md** - Project-specific commands and gotchas
- **subsystems/** - Deep dives into specific subsystems

### Meta-Instructions
Shortcuts starting with `>>` that expand to full workflows:

**Setup** (first time):
- `>>init-knowledge` - Setup knowledge base (human + QnA combined)
- `>>scan-repo` - Scan codebase and generate maps

**Work** (regular work):
- `>>start [TYPE] name` - Initialize new work (feat/maint/bug/concept)
- `>>continue` - Resume work
- `>>wrap` - End session with handoff
- `>>checkpoint` - Capture knowledge mid-session
- `>>status` - Quick status check
- `>>test` - Create test checklist
- `>>bug description` - Report and fix bug
- `>>archive` - Complete and archive work

**Concept work** (for complex planning):
- `>>start concept name` - Start concept work
- `>>add-input [path]` - Add input sources
- `>>extract` - Process inputs into structured data
- `>>conceptualize` - Build concept from extractions
- `>>plan` - Generate work plan (asks format first)
- `>>roadmap` - Generate roadmap with Mermaid visualization
- `>>refine [phase]` - Enter refinement cycle
- `>>finalize` - Promote to concepts/ and workplans/
- `>>new-version` - Create new version for major revision

## Philosophy

1. **Work Types**: Features, maintenance, bugs, and concepts each have appropriate documentation
2. **Knowledge Accumulation**: Insights from one task help with later tasks
3. **Separation of Concerns**: Humans read FOR-HUMANS, agents read FOR-AGENTS
4. **Meta-instructions**: Simple shortcuts expand to full protocols
5. **Templates**: Pre-filled structure, just customize content
6. **Append-only log**: Never create duplicate summaries
7. **Context preservation**: Knowledge checkpoints prevent loss in long sessions
8. **Conciseness**: Prioritize clarity and brevity
9. **Traceability**: Concept work maintains cross-references throughout

## Getting Started

### First Time Setup

**Option 1 - Full knowledge setup** (recommended):
1. Optionally: Fill out `ai-agent/knowledge/SYSTEM-OVERVIEW.md` with what you know
2. Run `>>init-knowledge` - AI reads your overview, asks questions to fill gaps
3. Run `>>scan-repo` - AI scans codebase and creates maps
4. Start first work: `>>start feat my-first-feature`

**Option 2 - Quick knowledge setup**:
1. Run `>>init-knowledge` - AI asks questions, creates overview
2. Start first work: `>>start feat my-first-feature`
3. Skip repo scanning for now (can run `>>scan-repo` anytime)

**Option 3 - Jump right in**:
1. Say `>>start feat my-first-feature`
2. AI learns about your project as it works
3. Knowledge accumulates naturally
4. Add formal knowledge later with `>>init-knowledge` and `>>scan-repo`

### Working on Tasks

**New to this system?**
1. Read `FOR-HUMANS.md` (5 min)
2. Say `>>start feat my-feature-name`
3. Answer AI's questions
4. Approve plan
5. AI implements

**Continuing work?**
1. Say `>>continue`
2. AI reads state from work folder
3. Confirms next task
4. You approve
5. Work continues

### Ending Sessions

1. Say `>>wrap`
2. AI performs knowledge checkpoint
3. AI updates progress log
4. AI marks completed tasks
5. AI sets clear next steps
6. Session ends cleanly

### Long Sessions

Use `>>checkpoint` to capture knowledge before context compression:
1. Say `>>checkpoint`
2. AI updates knowledge docs
3. AI preserves current context
4. Work continues

## Key Features

✅ **Work types**: Features, maintenance, bugs, and concepts with appropriate templates
✅ **Concept workflow**: Full lifecycle for complex planning (gather→extract→conceptualize→plan→roadmap)
✅ **Knowledge retention**: AI remembers project insights across sessions
✅ **Clear organization**: Numbered folders with type prefix
✅ **No context loss**: Resume work in < 2 minutes
✅ **Knowledge checkpoints**: Preserve insights in long sessions
✅ **Automated updates**: AI maintains checkboxes and progress
✅ **Template-based**: Consistent structure every time
✅ **Mermaid roadmaps**: Visual dependency graphs for concept work
✅ **Versioning**: Major concept revisions tracked in version folders

## Success Metrics

Your project is well-managed if:

- Each work item is in its own numbered folder (NNN-TYPE-name)
- Knowledge docs exist and are up-to-date
- `>>continue` gets you working in < 2 minutes
- Progress logs show clear progression
- `>>checkpoint` used in long sessions
- AI references knowledge docs before starting work

---

That's it! The system is designed to be simple, focused, and scalable.
