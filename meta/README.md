# Meta Documentation System

**Purpose**: Streamlined system for managing feature development and project knowledge with AI assistance.

## What's Here

```
meta/
├── README.md              ← You are here (overview)
├── FOR-HUMANS.md          ← Human guide + meta-instructions
├── FOR-AGENTS.md          ← Agent protocol + workflows
└── templates/
    ├── features/          ← Feature development templates
    │   ├── 00-FEATURE-OVERVIEW.md
    │   ├── 01-REQUIREMENTS.md
    │   ├── 02-IMPLEMENTATION-PLAN.md
    │   ├── 03-PROGRESS-LOG.md
    │   └── 04-TESTING-CHECKLIST.md
    └── knowledge/         ← Project knowledge templates
        ├── SYSTEM-OVERVIEW.md
        ├── REPOSITORY-MAP.md
        ├── CONCEPTS-INDEX.md
        └── subsystems/TEMPLATE.md
```

## Quick Start

### For Humans
→ Read `FOR-HUMANS.md` (5 minutes)

**Starting new feature**: Say `>>start [feature-name]`
**Continuing work**: Say `>>continue`
**Ending session**: Say `>>wrap`

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
    ├── features/                       ← Feature work (created by agent)
    │   ├── 001_feature-name/
    │   │   ├── 00-FEATURE-OVERVIEW.md
    │   │   ├── 01-REQUIREMENTS.md
    │   │   ├── 02-IMPLEMENTATION-PLAN.md
    │   │   ├── 03-PROGRESS-LOG.md
    │   │   └── 04-TESTING-CHECKLIST.md
    │   └── 002_another-feature/
    │       └── [same 5 documents]
    └── knowledge/                      ← Project knowledge (created by agent)
        ├── SYSTEM-OVERVIEW.md
        ├── REPOSITORY-MAP.md
        ├── CONCEPTS-INDEX.md
        └── subsystems/
            └── [subsystem].md
```

**Note**: Only the `meta/` folder needs to be copied to your project. The agent automatically creates `features/` and `knowledge/` folders when you run `>>start` or `>>init-knowledge`.

## Core Concepts

### Multiple Features
Each feature gets its own numbered folder (001_, 002_, etc.) containing **5 core documents**:

```
00-FEATURE-OVERVIEW.md     ← SSOT (Single Source of Truth)
01-REQUIREMENTS.md         ← What to build
02-IMPLEMENTATION-PLAN.md  ← How to build it
03-PROGRESS-LOG.md         ← Session log (append-only)
04-TESTING-CHECKLIST.md    ← Test scenarios
```

### Knowledge System
AI builds and maintains project knowledge to work more efficiently:

- **SYSTEM-OVERVIEW.md** - High-level project info (human or AI-filled)
- **REPOSITORY-MAP.md** - Directory structure and workflows
- **CONCEPTS-INDEX.md** - Patterns, APIs, models discovered
- **subsystems/** - Deep dives into specific subsystems

### Meta-Instructions
Shortcuts starting with `>>` that expand to full workflows:

**Setup** (first time):
- `>>init-knowledge` - Setup knowledge base (human + QnA combined)
- `>>scan-repo` - Scan codebase and generate maps

**Features** (regular work):
- `>>start feature-name` - Initialize new feature
- `>>continue` - Resume work
- `>>wrap` - End session with handoff
- `>>status` - Quick status check
- `>>test` - Create test checklist
- `>>bug description` - Report and fix bug
- `>>archive` - Complete and archive feature

## Philosophy

1. **Multiple Features**: Each feature isolated in its own folder, numbered for clarity
2. **Knowledge Accumulation**: Insights from one feature help with later features
3. **Separation of Concerns**: Humans read FOR-HUMANS, agents read FOR-AGENTS
4. **Meta-instructions**: Simple shortcuts expand to full protocols
5. **Templates**: Pre-filled structure, just customize content
6. **Append-only log**: Never create duplicate summaries
7. **Conciseness**: Prioritize clarity and brevity

## Getting Started

### First Time Setup

**Option 1 - Full knowledge setup** (recommended):
1. Optionally: Fill out `ai-agent/knowledge/SYSTEM-OVERVIEW.md` with what you know
2. Run `>>init-knowledge` - AI reads your overview, asks questions to fill gaps
3. Run `>>scan-repo` - AI scans codebase and creates maps
4. Start first feature: `>>start my-first-feature`

**Option 2 - Quick knowledge setup**:
1. Run `>>init-knowledge` - AI asks questions, creates overview
2. Start first feature: `>>start my-first-feature`
3. Skip repo scanning for now (can run `>>scan-repo` anytime)

**Option 3 - Jump right in**:
1. Say `>>start my-first-feature`
2. AI learns about your project as it works
3. Knowledge accumulates naturally
4. Add formal knowledge later with `>>init-knowledge` and `>>scan-repo`

### Working on Features

**New to this system?**
1. Read `FOR-HUMANS.md` (5 min)
2. Say `>>start my-feature-name`
3. Answer AI's questions
4. Approve plan
5. AI implements

**Continuing work?**
1. Say `>>continue`
2. AI reads state from feature folder
3. Confirms next task
4. You approve
5. Work continues

### Ending Sessions

1. Say `>>wrap`
2. AI updates progress log
3. AI marks completed tasks
4. AI sets clear next steps
5. Session ends cleanly

## Key Features

✅ **Multiple features**: Work on several features simultaneously
✅ **Knowledge retention**: AI remembers project insights across sessions
✅ **Clear organization**: Numbered folders, consistent structure
✅ **No context loss**: Resume work in < 2 minutes
✅ **Automated updates**: AI maintains checkboxes and progress
✅ **Template-based**: Consistent structure every time

## Success Metrics

Your project is well-managed if:

- Each feature is in its own numbered folder
- Knowledge docs exist and are up-to-date
- `>>continue` gets you working in < 2 minutes
- Progress logs show clear progression
- Only 5 core docs per feature (plus archive)
- AI references knowledge docs before starting work

---

That's it! The system is designed to be simple, focused, and scalable.
