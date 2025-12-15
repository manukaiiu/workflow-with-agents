# Protocol: >>plan

**Trigger**: `>>plan` or "let's create a work plan", "break this down into tasks"
**Purpose**: Generate work plan from concept

---

## Protocol Steps

### 1. Ask Format First (CRITICAL)

Before generating, ask human:

```
What format would you like for the work plan?
- `generic` - Flexible phases/work-packages/tasks
- `jira` - Epics/Stories (with optional sub-tasks)
- `github` - Issues with labels and milestones
- `custom` - Describe your structure
```

### 2. Wait for Human Response

Do not proceed until format is confirmed.

### 3. Generate Work Plan

Based on chosen format, create `04-WORKPLAN.md`:

#### Generic Format
```markdown
# Work Plan: [Name]

**Format**: Generic (Phases/Work Packages/Tasks)
**Created**: [Date]
**Source Concept**: 03-CONCEPT.md

## Overview
- **Phases**: [N]
- **Work Packages**: [N]
- **Tasks**: [N]
- **Complexity**: [High/Medium/Low]

## Traceability
| Work Package | Concept Elements | Requirements |
|--------------|------------------|--------------|
| WP1 | Section 1 | R1, R3 |
| WP2 | Section 2 | R2, R5 |

## Phase 1: [Name]

### WP1.1: [Work Package Name]
**Concept Source**: [Section reference]
**Requirements**: R1, R3

| Task | Type | Depends On | Complexity |
|------|------|------------|------------|
| T1.1.1 | Development | - | Medium |
| T1.1.2 | Testing | T1.1.1 | Low |

### WP1.2: [Work Package Name]
...

## Phase 2: [Name]
...

## Progress Summary
| Phase | Work Packages | Tasks | Status |
|-------|---------------|-------|--------|
| Phase 1 | 3 | 12 | [ ] Not Started |
| Phase 2 | 2 | 8 | [ ] Not Started |
```

#### Jira Format
```markdown
# Work Plan: [Name]

**Format**: Jira (Epics/Stories)
**Created**: [Date]

## Overview
- **Epics**: [N]
- **Stories**: [N]
- **Story Points**: [Total estimate]

## Epic 1: [Name]
**Concept Source**: [Section reference]

### Story 1.1: [User Story]
**As a** [role], **I want** [feature], **so that** [benefit]
**Points**: [N]
**Acceptance Criteria**:
- [ ] [Criterion 1]
- [ ] [Criterion 2]
**Depends On**: -

### Story 1.2: [User Story]
...
```

#### GitHub Format
```markdown
# Work Plan: [Name]

**Format**: GitHub (Issues/Milestones)
**Created**: [Date]

## Milestones
1. **[Milestone 1]** - [Description]
2. **[Milestone 2]** - [Description]

## Issues

### Issue #1: [Title]
**Milestone**: [Milestone name]
**Labels**: `feature`, `priority:high`
**Description**: [Details]
**Tasks**:
- [ ] [Task 1]
- [ ] [Task 2]
**Depends On**: -

### Issue #2: [Title]
...
```

### 4. Cross-Reference Update

Link all items to concept elements:
- Every work package/epic/issue traces to concept
- Requirements coverage verified

### 5. Present for Feedback

```
Work plan created in [format] format.

Overview:
- Phases/Epics: [N]
- Work Packages/Stories: [N]
- Tasks: [N]
- Complexity: [High/Medium/Low]

Structure:
Phase 1: [Name] - [N] work packages
Phase 2: [Name] - [N] work packages
...

Created: 04-WORKPLAN.md

All items traced to concept elements.

Ready for >>roadmap when plan is approved.
```

---

## Task Types

| Type | Description |
|------|-------------|
| Development | Code implementation |
| Testing | Test creation/execution |
| Documentation | Docs, comments |
| Research | Investigation, spike |
| Design | Architecture, UI/UX |
| Infrastructure | DevOps, setup |
| Review | Code/design review |

---

## Related Protocols

- Building concept → [conceptualize.md](conceptualize.md)
- Creating roadmap → [roadmap.md](roadmap.md)
- Refinement → [refine.md](refine.md)
