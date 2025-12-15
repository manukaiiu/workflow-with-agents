# Protocol: >>wrap

**Trigger**: `>>wrap` or "end session", "that's it for now", "let's stop"
**Purpose**: End session with proper handoff for future resumption

---

## Protocol Steps

### 1. Update Implementation Plan

In `02-IMPLEMENTATION-PLAN.md`:
- Mark completed phases with `[x]`
- Update any task checkboxes

### 2. Knowledge Checkpoint (Critical)

Before logging, capture any insights:

**Ask yourself:**
- Did I discover patterns worth documenting? → Update `CONCEPTS-INDEX.md`
- Were there gotchas future agents should know? → Update relevant subsystem doc
- Did I learn useful commands? → Update `COMMANDS.md`
- Any significant codebase insights? → Create/update subsystem doc

### 3. Append to Progress Log

Add to `03-PROGRESS-LOG.md` (or `06-PROGRESS-LOG.md` for concepts):

```markdown
## [YYYY-MM-DD] Session N

**Duration**: [X hours/minutes]
**Phase**: [Current phase]

**Completed**:
- [x] Item 1
- [x] Item 2

**Issues Encountered & Resolved**:
- Issue: [desc] → Solution: [desc] → Location: file.ts:line

**Knowledge Updated**:
- [List any knowledge docs updated, or "None"]

**Next Session Start Here**:
Priority 1: [Most important next task]
Priority 2: [Second task]

Context: [Any specific knowledge needed]
Files: [Files to review]

Quick start: ">>continue"
```

### 4. Update SSOT (If Major Milestone)

Update `00-OVERVIEW.md` if:
- Phase changed
- Status changed
- Major decision made
- Blockers changed

Update the **Quick Context** section with current state.

### 5. Update PR Message (If Exists)

If `06-PR-MESSAGE.md` exists, keep it current with latest changes.

### 6. Summarize to Human

```
Session summary:
✓ Completed: [List]
✓ Tests: [Status]
✓ Knowledge: [Updated X / No updates needed]

Updated:
- 03-PROGRESS-LOG.md (with handoff)
- 02-IMPLEMENTATION-PLAN.md (marked Phase X complete)
- [Any knowledge docs updated]

Next session: [Specific next task]
```

---

## Do NOT

- Leave vague handoffs ("continue the feature")
- Skip the knowledge checkpoint
- Forget to mark completed checkboxes
- Create new summary documents (append to progress log only)

---

## Response Template

```
Session summary:
✓ Completed: [List of completed items]
✓ Tests: [Passing / X failures / Not run]
✓ Knowledge: [Updated CONCEPTS-INDEX.md with X / No updates needed]

Updated:
- 03-PROGRESS-LOG.md (with handoff)
- 02-IMPLEMENTATION-PLAN.md (marked [phases] complete)
[- knowledge/[file].md (added [insight])]

Next session: [Specific next task with file path]

Quick resume: >>continue
```

---

## Wrap vs Pause

| Situation | Use |
|-----------|-----|
| Natural stopping point, work progressing | `>>wrap` |
| Interrupted, need to switch context | `>>pause` |
| End of day, clean stopping point | `>>wrap` |
| Urgent issue, mid-task interruption | `>>pause` |

---

## Related Protocols

- Need to pause mid-task? → [protocols/pause.md](pause.md)
- Resuming later → [protocols/continue.md](continue.md)
- Capturing knowledge → [protocols/checkpoint.md](checkpoint.md)
