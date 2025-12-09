# Roadmap: [Concept Name]

**Status**: Draft | Complete
**Last Updated**: [YYYY-MM-DD]
**Work Plan Reference**: [04-WORKPLAN.md](04-WORKPLAN.md)

---

## Dependency Analysis

### Critical Path
[Description of the longest dependency chain - what must happen sequentially]

Example: WP 1.1 → WP 1.2 → WP 2.1 → WP 3.1

### Parallel Opportunities
[What can be done simultaneously to optimize delivery]

- WP 1.1 and WP 1.4 can start together
- WP 2.1 and WP 2.2 can run in parallel after their dependencies

### Bottlenecks
- **WP X.X**: [Why this is a bottleneck and mitigation]

---

## Sequence Waves

### Wave 1: Foundation
**Can Start**: Immediately
**Enables**: Wave 2

| Work Package | Description | Enables |
|--------------|-------------|---------|
| WP 1.1 | [Name/brief description] | WP 1.2, WP 2.1 |
| WP 1.4 | [Name/brief description] | WP 2.2 |

**Wave 1 Completion Criteria**:
- [ ] [Criterion 1]
- [ ] [Criterion 2]

---

### Wave 2: Core
**Can Start**: After Wave 1
**Enables**: Wave 3

| Work Package | Description | Depends On | Enables |
|--------------|-------------|------------|---------|
| WP 1.2 | [Name] | WP 1.1 | WP 2.1 |
| WP 1.3 | [Name] | WP 1.1 | WP 2.2 |

**Wave 2 Completion Criteria**:
- [ ] [Criterion 1]
- [ ] [Criterion 2]

---

### Wave 3: Integration
**Can Start**: After Wave 2
**Enables**: Wave 4 / Completion

| Work Package | Description | Depends On | Enables |
|--------------|-------------|------------|---------|
| WP 2.1 | [Name] | WP 1.2 | WP 3.1 |
| WP 2.2 | [Name] | WP 1.3, WP 1.4 | WP 3.1 |

**Wave 3 Completion Criteria**:
- [ ] [Criterion 1]

---

### Wave 4: Finalization
**Can Start**: After Wave 3
**Enables**: Project Completion

| Work Package | Description | Depends On |
|--------------|-------------|------------|
| WP 3.1 | [Name] | WP 2.1, WP 2.2 |

**Wave 4 Completion Criteria**:
- [ ] [Criterion 1]

---

## Milestones

| ID | Milestone | After Wave | Success Criteria | Target (optional) |
|----|-----------|------------|------------------|-------------------|
| M1 | [Name] | Wave 1 | [Criteria] | [Date if known] |
| M2 | [Name] | Wave 2 | [Criteria] | |
| M3 | [Name] | Wave 4 | [Criteria] | |

---

## Risk Points

### Bottleneck: WP X.X
**Risk**: [Description]
**Impact**: Delays Wave [N] and everything after
**Mitigation**: [Strategy]

### Dependency Chain: [Description]
**Risk**: [Description]
**Impact**: [Impact]
**Mitigation**: [Strategy]

---

## Visualization

See [05-ROADMAP.mermaid.md](05-ROADMAP.mermaid.md) for visual diagrams.

---

## Timeline (Optional)

> Fill in only if concrete dates are available. Otherwise, use relative waves.

| Wave | Target Start | Target End | Notes |
|------|--------------|------------|-------|
| Wave 1 | [Date] | [Date] | |
| Wave 2 | [Date] | [Date] | |
| Wave 3 | [Date] | [Date] | |
| Wave 4 | [Date] | [Date] | |

---
**Target Length**: ~3 pages (plus Mermaid file)
