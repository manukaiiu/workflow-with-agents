# Meta Documentation v2

**Purpose**: Streamlined system for managing feature development with AI assistance.

## What's Here

```
meta-v2/
├── README.md              ← You are here (overview)
├── FOR-HUMANS.md          ← Human guide + meta-instructions
├── FOR-AGENTS.md          ← Agent protocol + meta-instruction handlers
└── templates/             ← Template files for documents
    ├── 00-FEATURE-OVERVIEW.md
    ├── 01-REQUIREMENTS.md
    ├── 02-IMPLEMENTATION-PLAN.md
    ├── 03-PROGRESS-LOG.md
    └── 04-TESTING-CHECKLIST.md
```

## Quick Start

### For Humans
→ Read `FOR-HUMANS.md` (3 minutes)

**Starting new feature**: Say `/start [feature-name]`
**Continuing work**: Say `/continue`
**Ending session**: Say `/wrap`

### For AI Agents
→ Read `FOR-AGENTS.md` when human points you to it

Parse meta-instructions (like `/start`, `/continue`, `/wrap`)
Follow the protocols defined there

## Core Concept

**5 core documents** in `/claude/`:
```
00-FEATURE-OVERVIEW.md     ← SSOT (Single Source of Truth)
01-REQUIREMENTS.md
02-IMPLEMENTATION-PLAN.md
03-PROGRESS-LOG.md         ← Append-only
04-TESTING-CHECKLIST.md
```

**Meta-instructions**: Shortcuts humans use (e.g., `/start`, `/continue`)
**Agents interpret** these using `FOR-AGENTS.md`

## Philosophy

1. **Separation**: Humans read FOR-HUMANS, agents read FOR-AGENTS
2. **Meta-instructions**: Simple shortcuts (like `/continue`) expand to full protocols
3. **Templates**: Pre-filled structure, just customize content
4. **Append-only log**: Never create duplicate summaries

## Getting Started

**New to this system?**
1. Read `FOR-HUMANS.md` (3 min)
2. Say `/start my-feature-name`
3. Answer AI's questions
4. Approve plan
5. AI implements

**Continuing work?**
1. Say `/continue`
2. AI reads state
3. Confirms next task
4. You approve
5. Work continues

That's it! The system is simple and focused.
