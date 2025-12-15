# Work Types Reference

Detailed guide to the four work types supported by the workflow system.

---

## Overview

| Type | Prefix | Use For | Complexity |
|------|--------|---------|------------|
| Feature | `feat` | New functionality, enhancements | Medium-High |
| Bug | `bug` | Bug fixes | Low-Medium |
| Maintenance | `maint` | Updates, refactoring, security | Low-Medium |
| Concept | `concept` | Complex planning, roadmaps | High |

---

## Feature (`feat`)

**Use for**: New functionality, user-facing enhancements, major changes

### Documents
```
NNN-feat-name/
├── 00-OVERVIEW.md
├── 01-REQUIREMENTS.md         ← What to build
├── 02-IMPLEMENTATION-PLAN.md
├── 03-PROGRESS-LOG.md
├── 04-TESTING-CHECKLIST.md
├── 05-ANALYSIS.md             ← Optional: research
└── 06-PR-MESSAGE.md           ← Optional: PR draft
```

### Workflow
1. `>>start feat name` - Create folder, ask questions
2. Human answers → Create implementation plan
3. Human approves → Begin implementation
4. `>>test` - Create test scenarios
5. `>>wrap` - End session with handoff
6. `>>archive` - Complete work

### Key Points
- Full documentation required
- Questions before implementation plan
- PR message maintained throughout
- 05-ANALYSIS.md for feature-specific research

---

## Bug (`bug`)

**Use for**: Bug fixes, defect resolution, error corrections

### Documents
```
NNN-bug-name/
├── 00-OVERVIEW.md
├── 01-REQUIREMENTS.md         ← Bug description, repro, expected
├── 02-IMPLEMENTATION-PLAN.md
├── 03-PROGRESS-LOG.md
└── 04-TESTING-CHECKLIST.md
```

### Workflow
1. `>>start bug name` or `>>bug description` - Create/log bug
2. Gather reproduction steps
3. Investigate root cause
4. Propose fix, get approval
5. Implement and verify
6. `>>archive` when fixed

### Key Points
- Uses feature templates (lighter usage)
- Focus on reproduction steps
- Root cause analysis important
- Verify fix before archive

### Bug Severity

| Severity | Description | Response |
|----------|-------------|----------|
| High | Blocks work, crashes, data loss | Fix immediately |
| Medium | Incorrect behavior, workaround exists | Fix soon |
| Low | Minor issue, cosmetic, edge case | Fix when convenient |

---

## Maintenance (`maint`)

**Use for**: Dependency updates, refactoring, security audits, build changes

### Documents
```
NNN-maint-name/
├── 00-OVERVIEW.md
├── 01-SCOPE.md                ← What's included, compatibility
├── 02-IMPLEMENTATION-PLAN.md
├── 03-PROGRESS-LOG.md
└── 04-TESTING-CHECKLIST.md
```

### Workflow
1. `>>start maint name` - Create folder, define scope
2. Document compatibility concerns
3. Create implementation plan
4. Execute with careful testing
5. `>>archive` when complete

### Key Points
- Lighter documentation than features
- Focus on scope and compatibility
- Security and dependency work common
- Test impact on existing functionality

### Common Maintenance Types
- Dependency updates
- Code refactoring
- Security patches
- Build/CI changes
- Performance optimization
- Technical debt

---

## Concept (`concept`)

**Use for**: Complex planning, multi-phase projects, roadmaps

### Documents
```
NNN-concept-name/
├── 00-OVERVIEW.md
├── 01-INPUTS/
│   └── INDEX.md               ← Input inventory
├── 02-EXTRACTIONS.md          ← Extracted info with IDs
├── 03-CONCEPT.md              ← Main concept
├── 03-CONCEPT-[sub].md        ← Sub-concepts (max 7)
├── 04-WORKPLAN.md             ← Work breakdown
├── 05-ROADMAP.md              ← Sequencing
├── 05-ROADMAP.mermaid.md      ← Visualization
├── 06-PROGRESS-LOG.md
├── 07-REFINEMENT-LOG.md
├── 08-OPEN-QUESTIONS.md
└── 90-OUTPUTS/                ← Deliverables
```

### Workflow
```
Gathering → Extracting → Conceptualizing → Planning → Roadmapping → Finalizing
```

1. `>>start concept name` - Create folder
2. `>>add-input` - Add input sources
3. `>>extract` - Process inputs, create extraction IDs
4. `>>conceptualize` - Build concept (max 7 sub-concepts)
5. `>>plan` - Ask format first, create work plan
6. `>>roadmap` - Generate roadmap + Mermaid
7. `>>finalize` - Promote to concepts/, workplans/

### Finalized Output
```
ai-agent/concepts/[name]/v1/
├── CONCEPT.md
├── CONCEPT-[sub].md
└── INPUTS-SUMMARY.md

ai-agent/workplans/[name]/v1/
├── WORKPLAN.md
├── ROADMAP.md
└── ROADMAP.mermaid.md
```

### Key Points
- Full conceptualization workflow
- Source attribution with IDs (T1, R2, etc.)
- Traceability throughout
- Refinement cascades forward
- Finalization promotes to top-level folders

---

## Choosing Work Type

| Scenario | Work Type |
|----------|-----------|
| Adding a new feature | `feat` |
| Something is broken | `bug` |
| Updating dependencies | `maint` |
| Refactoring code | `maint` |
| Planning a large initiative | `concept` |
| Security patches | `maint` |
| User-requested enhancement | `feat` |
| Performance fix | Could be `bug` or `maint` |
| Multi-month planning | `concept` |

---

## Templates Location

| Work Type | Templates Folder |
|-----------|------------------|
| Feature | `meta/templates/features/` |
| Bug | `meta/templates/features/` |
| Maintenance | `meta/templates/maintenance/` |
| Concept | `meta/templates/concept/` |
