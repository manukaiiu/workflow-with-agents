# Meta System Enhancement - Implementation Plan

## Overview
Enhancing the meta documentation system to support multiple features, knowledge collection, and improved agent compliance.

## Fixes

### Fix 1: Agent Compliance for Checkbox Updates
**Issue**: Agents don't consistently update checkboxes in progress tracking.
**Solution**: Add explicit reminder in FOR-AGENTS.md in the most effective location.
**Location**: After each relevant workflow section where checkboxes are used.
**Status**: Pending

### Fix 2: Command Prefix Replacement
**Issue**: `/` prefix conflicts with Claude's native commands.
**Chosen Solution**: Use `>>` prefix (clean, distinct, typing-friendly)
**Alternatives considered**: `!`, `@`, `::`, `%%`
**Why `>>`**: Visually suggests "forward action", no conflicts, easy to type
**Impact**: All documentation files need updating
**Status**: Pending

## New Features

### Feature 1: Multiple Features Support

**Folder Structure**:
```
project-root/ai-agent/
├── meta/
│   ├── FOR-AGENTS.md
│   ├── FOR-HUMANS.md
│   ├── README.md
│   └── templates/
│       ├── features/              # NEW - moved here
│       │   ├── 00-FEATURE-OVERVIEW.md
│       │   ├── 01-REQUIREMENTS.md
│       │   ├── 02-IMPLEMENTATION-PLAN.md
│       │   ├── 03-PROGRESS-LOG.md
│       │   └── 04-TESTING-CHECKLIST.md
│       └── knowledge/             # NEW - for knowledge system
│           └── [TBD]
└── features/                      # NEW - actual features live here
    ├── 001_feature-name/
    │   ├── 00-FEATURE-OVERVIEW.md
    │   ├── 01-REQUIREMENTS.md
    │   ├── 02-IMPLEMENTATION-PLAN.md
    │   ├── 03-PROGRESS-LOG.md
    │   └── 04-TESTING-CHECKLIST.md
    └── 002_another-feature/
        └── [same structure]
```

**Workflow Changes**:
1. `>>start` now creates numbered feature folder first
2. Then copies templates from `meta/templates/features/` to feature folder
3. All work happens in the feature-specific folder
4. Feature folder naming: `NNN_concise-feature-name` (e.g., `001_user-auth`)

**Implementation Steps**:
- [x] Move current templates to `meta/templates/features/`
- [x] Update `>>start` workflow in FOR-AGENTS.md
- [x] Update FOR-HUMANS.md with new structure
- [x] Update README.md

**Status**: Pending

### Feature 2: Knowledge Collection System

**Philosophy**:
- Agents need structured knowledge about projects
- Knowledge grows incrementally through work
- Multiple acquisition methods for different contexts

**Three Knowledge Workflows**:

#### 1. Initial Knowledge Creation (Human-Driven)
**Template**: `SYSTEM-OVERVIEW.md` (filled by human or through QnA)
**Contains**:
- Project purpose and domain
- Tech stack and architecture patterns
- Key concepts and terminology
- Major subsystems and their roles
- Critical conventions and patterns

#### 2. Repository Scanning (Agent-Driven)
**Template**: `REPOSITORY-MAP.md` (agent-generated)
**Contains**:
- Directory structure and organization
- Key files and their purposes
- Module dependencies
- Entry points and main workflows

**Template**: `CONCEPTS-INDEX.md` (agent-generated)
**Contains**:
- Discovered patterns and abstractions
- Common utilities and helpers
- Data models and schemas
- API structure

#### 3. Incremental Knowledge (During Feature Development)
**Template**: `SUBSYSTEM-NOTES.md` (agent-maintained)
**Structure**:
```markdown
# Subsystem: [Name]

## Last Updated
[Date] - [Feature that prompted this]

## Purpose
[What this subsystem does]

## Key Files
- file.ts:123 - [purpose]

## Important Patterns
- [Pattern discovered]

## Gotchas
- [Things to watch out for]

## Related Subsystems
- [Links to other notes]
```

**Knowledge Folder Structure**:
```
project-root/ai-agent/meta/knowledge/
├── SYSTEM-OVERVIEW.md          # Human-filled or QnA-generated
├── REPOSITORY-MAP.md           # Agent-generated from scan
├── CONCEPTS-INDEX.md           # Agent-generated catalog
└── subsystems/
    ├── auth.md                 # Incremental notes
    ├── database.md
    └── api.md
```

**Integration with Feature Development**:
- FOR-AGENTS.md will reference knowledge directory
- Before starting feature: "Check knowledge/ for relevant context"
- During feature: "Update knowledge/ when discovering important patterns"
- Lightweight workflow: Don't over-document, focus on reusable insights

**Implementation Steps**:
- [x] Design knowledge folder structure
- [x] Create template files for all three workflows
- [x] Document knowledge creation workflows in FOR-AGENTS.md
- [x] Document knowledge usage in FOR-HUMANS.md
- [x] Add knowledge lookup guidance to feature development workflow

**Status**: Pending

## Implementation Order

1. **Fix: Command Prefix** (affects all docs, do first)
2. **Fix: Agent Compliance** (small addition)
3. **Feature: Multiple Features** (structural change)
4. **Feature: Knowledge System** (new capability)
5. **Final Review** (ensure no redundancy, all docs updated)

## Files to Update

### Must Update (Command Prefix Change)
- [ ] meta/FOR-AGENTS.md
- [ ] meta/FOR-HUMANS.md
- [ ] meta/README.md

### Must Update (Multiple Features)
- [ ] meta/FOR-AGENTS.md (>>start workflow)
- [ ] meta/FOR-HUMANS.md (folder structure)
- [ ] meta/README.md (overview)
- [ ] Move: meta/templates/*.md → meta/templates/features/*.md

### Must Create (Knowledge System)
- [ ] meta/templates/knowledge/SYSTEM-OVERVIEW.md
- [ ] meta/templates/knowledge/REPOSITORY-MAP.md
- [ ] meta/templates/knowledge/CONCEPTS-INDEX.md
- [ ] meta/templates/knowledge/subsystems/TEMPLATE.md

### Must Update (Knowledge Integration)
- [ ] meta/FOR-AGENTS.md (add knowledge workflows)
- [ ] meta/FOR-HUMANS.md (add knowledge section)

## Success Criteria

- [ ] No slash commands in documentation
- [ ] All templates in correct new locations
- [ ] Feature creation creates numbered folders
- [ ] Knowledge system fully documented
- [ ] No duplicate information across files
- [ ] All references updated consistently
- [ ] System remains concise and readable
