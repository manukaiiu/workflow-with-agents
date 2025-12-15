# Protocol: >>pause

**Trigger**: `>>pause [reason]` or "let's stop here", "need to interrupt", "pause this"
**Purpose**: Pause work item with full context for easy resumption

---

## When to Pause (vs Wrap)

| Situation | Use |
|-----------|-----|
| Mid-task interruption | `>>pause` |
| Higher priority work emerged | `>>pause` |
| Blocker discovered, need external input | `>>pause` |
| Natural stopping point, session ending | `>>wrap` |
| Work complete, ending session | `>>wrap` |

---

## Protocol Steps

### 1. Update Status in 00-OVERVIEW.md

Change status to PAUSED with reason:

```markdown
**Status**: PAUSED - [reason]
**Paused**: [YYYY-MM-DD]
```

### 2. Add Pause Context Section

Add this section to `00-OVERVIEW.md`:

```markdown
## Pause Context

**Paused on**: [YYYY-MM-DD]
**Reason**: [Why - user request, blocker, priority shift]
**Resume with**: `>>continue` or read this OVERVIEW

**State at pause**:
- [What's done]
- [What's in progress]
- [Blockers or pending questions]

**To resume**:
1. [First specific step to pick up]
2. [Second step]
3. [Continue as needed]

**Files in progress**:
- [file.ts:line - what was being done]
```

### 3. Update Progress Log

Add brief entry to progress log:

```markdown
## [YYYY-MM-DD] Session Paused

**Paused at**: [time/phase]
**Reason**: [reason]
**Resume instructions**: See 00-OVERVIEW.md Pause Context
```

### 4. Update Work Index

If `ai-agent/work/WORK-INDEX.md` exists:
- Move entry from "Active Work Items" to "Paused Work Items"
- Add paused date, reason, and resume command

### 5. Confirm to Human

```
Work item paused.

Status: PAUSED - [reason]
State: [brief description of where things stand]

To resume later: >>continue
The OVERVIEW contains full context for resumption.
```

---

## Pause Context Template

```markdown
## Pause Context

**Paused on**: YYYY-MM-DD
**Reason**: [User request / Blocker: X / Priority shift to Y]
**Resume with**: `>>continue`

**State at pause**:
- Phase 2 (Implementation) ~60% complete
- UserService.ts refactoring done
- AuthController.ts in progress (line 145)
- Tests not yet updated

**Blockers** (if any):
- Waiting for [X] from [person/team]

**To resume**:
1. Open src/controllers/AuthController.ts
2. Continue refactoring from line 145
3. Update corresponding tests
4. Run test suite

**Files in progress**:
- src/controllers/AuthController.ts:145 - mid-refactor
- src/services/UserService.ts - complete, needs review
```

---

## Do NOT

- Pause when work is actually complete (use `>>archive`)
- Leave vague resume instructions
- Forget to update the status in OVERVIEW
- Skip the progress log entry

---

## Resuming Paused Work

When `>>continue` is called on paused work:
1. Read the Pause Context section
2. Follow "To resume" steps
3. Update status back to "In Progress"
4. Remove or archive the Pause Context section

---

## Related Protocols

- Resuming paused work → [protocols/continue.md](continue.md)
- Ending session normally → [protocols/wrap.md](wrap.md)
- Context recovery → [protocols/recovery.md](recovery.md)
