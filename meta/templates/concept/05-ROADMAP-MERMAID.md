# Roadmap Visualization: [Concept Name]

> **Note**: This file is auto-generated from [05-ROADMAP.md](05-ROADMAP.md).
> Edit the source roadmap document for changes.

**Last Generated**: [YYYY-MM-DD]

---

## Dependency Graph

```mermaid
graph LR
    subgraph Wave1[Wave 1: Foundation]
        WP1.1[WP 1.1: Name]
        WP1.4[WP 1.4: Name]
    end

    subgraph Wave2[Wave 2: Core]
        WP1.2[WP 1.2: Name]
        WP1.3[WP 1.3: Name]
    end

    subgraph Wave3[Wave 3: Integration]
        WP2.1[WP 2.1: Name]
        WP2.2[WP 2.2: Name]
    end

    subgraph Wave4[Wave 4: Finalization]
        WP3.1[WP 3.1: Name]
    end

    WP1.1 --> WP1.2
    WP1.1 --> WP1.3
    WP1.2 --> WP2.1
    WP1.3 --> WP2.2
    WP1.4 --> WP2.2
    WP2.1 --> WP3.1
    WP2.2 --> WP3.1

    M1((M1)) -.-> Wave1
    M2((M2)) -.-> Wave2
    M3((M3)) -.-> Wave4

    style M1 fill:#ffd700
    style M2 fill:#ffd700
    style M3 fill:#ffd700
```

---

## Timeline View (if dates available)

```mermaid
gantt
    title Project Roadmap
    dateFormat YYYY-MM-DD

    section Wave 1
    WP 1.1 - Name    :wp11, 2025-01-01, 2w
    WP 1.4 - Name    :wp14, 2025-01-01, 1w

    section Wave 2
    WP 1.2 - Name    :wp12, after wp11, 2w
    WP 1.3 - Name    :wp13, after wp11, 1w

    section Wave 3
    WP 2.1 - Name    :wp21, after wp12, 2w
    WP 2.2 - Name    :wp22, after wp13 wp14, 3w

    section Wave 4
    WP 3.1 - Name    :wp31, after wp21 wp22, 2w

    section Milestones
    M1 - Foundation Complete    :milestone, m1, after wp11 wp14, 0d
    M2 - Core Complete          :milestone, m2, after wp12 wp13, 0d
    M3 - Project Complete       :milestone, m3, after wp31, 0d
```

---

## Critical Path Highlight

```mermaid
graph LR
    subgraph Critical[Critical Path]
        direction LR
        CP1[WP 1.1] --> CP2[WP 1.2] --> CP3[WP 2.1] --> CP4[WP 3.1]
    end

    subgraph Parallel[Parallel Work]
        P1[WP 1.4]
        P2[WP 1.3]
        P3[WP 2.2]
    end

    style Critical fill:#ffcccc
    style Parallel fill:#ccffcc
```

---

## Status Overview (update during execution)

```mermaid
pie title Work Package Status
    "Completed" : 0
    "In Progress" : 0
    "Not Started" : 7
```

---

## Notes

- Solid arrows (→) indicate hard dependencies
- Dashed arrows (-.→) indicate milestone checkpoints
- Update this file when roadmap changes using `>>roadmap`

---
**Auto-generated**: Do not edit directly
