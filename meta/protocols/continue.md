# Protocol: >>continue

**Trigger**: `>>continue` or "resume", "keep going", "continue where we left off"
**Purpose**: Resume work on existing work item

---

## Protocol Steps

### 1. Check Knowledge Base (Do First)

Review if they exist:
- `ai-agent/knowledge/SYSTEM-OVERVIEW.md` - project context
- `ai-agent/knowledge/COMMANDS.md` - useful commands
- Relevant `knowledge/subsystems/` docs

### 2. Find Active Work Item

```bash
ls ai-agent/work/
```

- If multiple folders exist, check which has status "In Progress" or "Paused"
- If unclear, ask human which work item to continue

### 3. Read Work SSOT

Open `00-OVERVIEW.md` in the work folder. Extract:
- Work name and type
- Current status
- Current phase
- **Quick Context** section (if present)

### 4. Check for Pause Context

If "Pause Context" section exists in OVERVIEW:
- Follow its "To resume" steps
- After resuming, archive or remove the pause context

### 5. Read Progress Log

Open `03-PROGRESS-LOG.md` (or `06-PROGRESS-LOG.md` for concepts)
- Find "Next Session Start Here" in last entry
- Note the specific next task

### 6. Summarize to Human (Max 4 Sentences)

```
Work: [Name] ([type])
Status: [status]
Phase: [current phase]
Next: [specific task with file path if applicable]

Ready to proceed?
```

### 7. Wait for Confirmation

Do NOT start working until human confirms.

---

## Do NOT

- Start working without confirming with human
- Re-read entire codebase (focus on specific files mentioned)
- Create new summary documents
- Assume context from previous session (always re-read SSOT)

---

## Response Template

```
Work: [Name from SSOT] ([TYPE])
Status: [Status from SSOT]
Current Phase: [Phase X - Name]

Last completed: [From progress log]
Next task: [Specific task with file path]

Ready to proceed with [next task]?
```

---

## If Multiple Work Items

When multiple work folders exist and it's unclear which to continue:

```
I found multiple work items:
- 001-feat-user-auth (In Progress)
- 002-concept-platform (Paused)

Which would you like to continue?
```

---

## Resuming Paused Work

If `00-OVERVIEW.md` has a "Pause Context" section:

1. Read the "State at pause" to understand where things stand
2. Follow the "To resume" steps exactly
3. Update status from "PAUSED" to "In Progress"
4. Continue with the next task

---

## Related Protocols

- Work was paused? Check Pause Context in OVERVIEW
- Need to pause now? → [protocols/pause.md](pause.md)
- Ending this session? → [protocols/wrap.md](wrap.md)
- Context feels stale? → [protocols/recovery.md](recovery.md)
- Concept work? → [protocols/concept/overview.md](concept/overview.md)
