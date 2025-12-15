# Protocol: Context Recovery

**Trigger**: After context summarization, new agent continuing, or feeling disoriented
**Purpose**: Re-establish workflow awareness and work state

---

## When This Applies

- Your context was just summarized/compressed
- You're a new agent continuing previous work
- You feel uncertain about the current state
- Human says "you seem to have lost context"

---

## Recovery Steps

### 1. Check Git Status

```bash
git status
```

Are there uncommitted changes? Note them.

### 2. Find Active Work

```bash
ls ai-agent/work/
```

Identify which work item is active (look for "In Progress" or "Paused" status).

### 3. Read Work SSOT

Open the active work item's `00-OVERVIEW.md`. Extract:
- Work name and type
- Current status (In Progress, Paused, etc.)
- Current phase
- **Quick Context** section (critical for recovery)

### 4. Read Progress Log

Open `03-PROGRESS-LOG.md` (or `06-PROGRESS-LOG.md` for concepts).
- Find "Next Session Start Here" in last entry
- Note specific files and tasks mentioned

### 5. Check for Pause Context

If `00-OVERVIEW.md` has a "Pause Context" section:
- Read "State at pause"
- Follow "To resume" steps
- This is your recovery roadmap

### 6. Re-read Relevant Knowledge

If the work involves specific subsystems:
- Check `knowledge/subsystems/` for relevant docs
- Check `knowledge/CONCEPTS-INDEX.md` for patterns

### 7. Confirm with Human

Before proceeding:

```
I've recovered context from the documents.

Work: [Name] ([type])
Status: [status]
Phase: [phase]
Last: [last completed from log]
Next: [next task from log]

[If uncommitted changes:]
Note: There are uncommitted changes in git.

Is this understanding correct? Should I proceed with [next task]?
```

---

## Recovery Checklist

```markdown
[ ] Checked git status
[ ] Found active work item
[ ] Read 00-OVERVIEW.md
[ ] Read last progress log entry
[ ] Checked for Pause Context
[ ] Reviewed relevant knowledge docs
[ ] Confirmed understanding with human
```

---

## If Documents Are Missing

If expected documents don't exist:

```
I'm trying to recover context but:
- [ ] 00-OVERVIEW.md is missing/incomplete
- [ ] Progress log has no recent entries
- [ ] Cannot determine current state

Could you help me understand:
1. What work item should I continue?
2. What was the last completed task?
3. What should I work on next?
```

---

## If Multiple Work Items

When multiple work folders exist:

```
I found multiple work items:
- 001-feat-user-auth (In Progress, Phase 2)
- 002-concept-platform (Paused)
- 003-bug-login-fix (Complete)

Which should I continue? Or should I start something new?
```

---

## Proactive Recovery Question

After recovering context, ask:

```
I've recovered context from the documents.

Should I update knowledge with any insights from the previous session
before continuing?
```

---

## Signs You Need Recovery

- Referring to files/tasks not in current context
- Confusion about project structure
- Uncertainty about what to do next
- Human corrects your understanding
- You're making assumptions instead of checking documents

---

## Related Protocols

- Continuing work → [protocols/continue.md](continue.md)
- Work was paused → Check Pause Context in OVERVIEW
- Knowledge checkpoint → [protocols/checkpoint.md](checkpoint.md)
