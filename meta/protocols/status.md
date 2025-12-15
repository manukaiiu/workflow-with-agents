# Protocol: >>status

**Trigger**: `>>status` or "what's the status", "where are we"
**Purpose**: Quick status check without making changes

---

## Protocol Steps

### 1. Read SSOT

Read `00-OVERVIEW.md`:
- Work name and type
- Overall status
- Current phase

### 2. Read Implementation Plan

Read `02-IMPLEMENTATION-PLAN.md`:
- Count completed phases (marked `[x]`)
- Count total phases
- Calculate percentage

### 3. Present Status

**Do NOT modify anything** - this is read-only.

```
Work: [Name] (TYPE)
Overall: [X]% complete ([Y] of [Z] phases done)
Current Phase: [Phase X - Name]
Last update: [Date from progress log]

Completed:
✓ Phase 1: [Name]
✓ Phase 2: [Name]

In Progress:
~ Phase 3: [Name] ([%] done)

Pending:
- Phase 4: [Name]
- Phase 5: [Name]

Next: [Next task from progress log]
```

---

## Status Indicators

| Symbol | Meaning |
|--------|---------|
| ✓ | Completed |
| ~ | In Progress |
| - | Pending |
| ❌ | Blocked |
| ⏸ | Paused |

---

## For Concept Work

For concept work items, also show:

```
Concept Phase: [Gathering/Extracting/Conceptualizing/Planning/Roadmapping]
Inputs: [X] processed / [Y] total
Open Questions: [N] pending

Documents:
✓ 01-INPUTS/INDEX.md
✓ 02-EXTRACTIONS.md
~ 03-CONCEPT.md
- 04-WORKPLAN.md
- 05-ROADMAP.md
```

---

## When Multiple Work Items Exist

If `ai-agent/work/` has multiple folders:

```
Active Work Items:

1. 001-feat-user-auth (In Progress)
   Phase: 3/5 - Implementation

2. 002-maint-deps-update (Paused)
   Reason: Waiting for review

3. 003-concept-new-platform (Draft)
   Phase: Conceptualizing

Which would you like details on? (or specify with >>status 001)
```

---

## Related Protocols

- Continuing work → [protocols/continue.md](continue.md)
- Checking specific phase → [protocols/checkpoint.md](checkpoint.md)
