# Protocol: >>roadmap

**Trigger**: `>>roadmap` or "create a roadmap", "show dependencies"
**Purpose**: Generate roadmap with dependencies and visualization

---

## Protocol Steps

### 1. Analyze Dependencies

From `04-WORKPLAN.md`:
- Map all task/work package dependencies
- Identify critical path
- Find parallel opportunities
- Note bottlenecks

### 2. Generate 05-ROADMAP.md

```markdown
# Roadmap: [Name]

**Created**: [Date]
**Source Work Plan**: 04-WORKPLAN.md

## Dependency Analysis

### Critical Path
[Description of longest dependency chain]

Items on critical path:
1. [Item 1] → [Item 2] → [Item 3] → ...

### Parallel Opportunities
- [Items that can run in parallel]
- [More parallel work]

### Bottlenecks
| Bottleneck | Blocked Items | Mitigation |
|------------|---------------|------------|
| [Item] | [What it blocks] | [How to address] |

## Sequence Waves

### Wave 1: Foundation
**Can start immediately** - no dependencies

| Item | Type | Effort |
|------|------|--------|
| [WP/Task] | [Type] | [Estimate] |

### Wave 2: Core
**Requires**: Wave 1 complete

| Item | Type | Depends On | Effort |
|------|------|------------|--------|
| [WP/Task] | [Type] | [Dependency] | [Est] |

### Wave 3: Integration
**Requires**: Wave 2 complete

| Item | Type | Depends On | Effort |
|------|------|------------|--------|
| [WP/Task] | [Type] | [Dependency] | [Est] |

### Wave 4: Polish
**Requires**: Wave 3 complete

| Item | Type | Depends On | Effort |
|------|------|------------|--------|
| [WP/Task] | [Type] | [Dependency] | [Est] |

## Milestones

| Milestone | Wave | Key Deliverables |
|-----------|------|------------------|
| M1: [Name] | After Wave 1 | [What's delivered] |
| M2: [Name] | After Wave 2 | [What's delivered] |

## Risk Points

| Risk Point | Wave | Items Affected | Contingency |
|------------|------|----------------|-------------|
| [Risk] | [Wave] | [Items] | [Plan B] |
```

### 3. Generate 05-ROADMAP.mermaid.md

```markdown
# Roadmap Visualizations

## Dependency Graph

```mermaid
graph LR
    subgraph Wave1[Wave 1: Foundation]
        WP1[WP1: Name]
        WP2[WP2: Name]
    end

    subgraph Wave2[Wave 2: Core]
        WP3[WP3: Name]
        WP4[WP4: Name]
    end

    subgraph Wave3[Wave 3: Integration]
        WP5[WP5: Name]
    end

    WP1 --> WP3
    WP2 --> WP3
    WP2 --> WP4
    WP3 --> WP5
    WP4 --> WP5

    style WP1 fill:#90EE90
    style WP5 fill:#FFB6C1
```

## Timeline View (if dates available)

```mermaid
gantt
    title Project Roadmap
    dateFormat YYYY-MM-DD

    section Wave 1
    WP1: Name    :w1_1, 2025-01-01, 5d
    WP2: Name    :w1_2, 2025-01-01, 7d

    section Wave 2
    WP3: Name    :w2_1, after w1_1, 10d
    WP4: Name    :w2_2, after w1_2, 8d

    section Wave 3
    WP5: Name    :w3_1, after w2_1 w2_2, 5d
```

## Status Overview

```mermaid
pie title Work Distribution by Wave
    "Wave 1 - Foundation" : 4
    "Wave 2 - Core" : 6
    "Wave 3 - Integration" : 3
    "Wave 4 - Polish" : 2
```

## Critical Path Highlight

```mermaid
graph LR
    A[Start] --> B[WP1]
    B --> C[WP3]
    C --> D[WP5]
    D --> E[End]

    style A fill:#FFD700
    style B fill:#FF6347
    style C fill:#FF6347
    style D fill:#FF6347
    style E fill:#FFD700

    linkStyle 0,1,2,3 stroke:#FF0000,stroke-width:3px
```
```

### 4. Update OVERVIEW

Update `00-OVERVIEW.md`:
- Status to "Roadmapping" or "Ready for Review"
- Add roadmap summary

### 5. Present to Human

```
Roadmap generated.

Dependency Analysis:
- Critical Path: [Brief description]
- Parallel Opportunities: [Brief description]

Waves:
- Wave 1 (Foundation): [N] work packages - can start immediately
- Wave 2 (Core): [N] work packages - after Wave 1
- Wave 3 (Integration): [N] work packages - after Wave 2
...

Milestones: [N] defined

Created:
- 05-ROADMAP.md
- 05-ROADMAP.mermaid.md (visual diagrams)

Ready for >>finalize when roadmap is approved, or >>refine [phase] for changes.
```

---

## Related Protocols

- Creating work plan → [plan.md](plan.md)
- Refinement → [refine.md](refine.md)
- Finalizing → [finalize.md](finalize.md)
