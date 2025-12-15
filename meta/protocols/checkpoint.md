# Protocol: >>checkpoint

**Trigger**: `>>checkpoint` or proactively at ~70-80% context usage
**Purpose**: Capture knowledge mid-session before context compression

---

## When to Use

- Long sessions approaching context limits
- Before expected context compression/summarization
- When you've accumulated significant insights not yet documented
- Human explicitly requests knowledge capture
- **Proactively**: When you sense context is getting full

**Note**: This does NOT end the session. Continue working after checkpoint.

---

## Protocol Steps

### 1. Review Session Activity

Ask yourself:
- What patterns have I discovered?
- What gotchas or issues were encountered?
- What commands or workflows were useful?
- What subsystem knowledge was gained?

### 2. Update Knowledge Docs

Based on review, update as appropriate:

| Insight Type | Update |
|--------------|--------|
| Patterns, APIs, models | `knowledge/CONCEPTS-INDEX.md` |
| Useful commands | `knowledge/COMMANDS.md` |
| Deep subsystem insights | `knowledge/subsystems/[name].md` |
| Architecture insights (rare) | `knowledge/SYSTEM-OVERVIEW.md` |

### 3. Update Progress Log

Add checkpoint entry:

```markdown
### Knowledge Checkpoint [YYYY-MM-DD HH:MM]

**Captured**:
- [What was documented]
- [Where it was added]

**Context for continuation**:
- Current task: [What you're working on]
- Key files: [Files currently relevant]
- Pending decisions: [Any open questions]

**State summary**:
- [Brief state description for context recovery]
```

### 4. Summarize to Human

```
Knowledge checkpoint captured.

Updated:
- [List of knowledge docs updated]

Current context preserved for continuation.
Ready to proceed.
```

---

## Proactive Checkpointing

As an agent, you should proactively checkpoint when:

1. **Before large operations**: "I'll set a checkpoint before processing this large input."
2. **After significant discoveries**: "I've learned important patterns - let me checkpoint."
3. **When context feels full**: "We've covered a lot - let me capture this before continuing."

Announce it: "I'll set a checkpoint before proceeding with [task]."

---

## What to Capture

### Always Capture
- Patterns discovered during work
- Gotchas that took time to figure out
- Non-obvious relationships between components
- Commands that required research

### Don't Over-Capture
- Obvious code patterns
- Standard framework usage
- Information already documented
- Temporary debugging findings

---

## Response Template

```
Knowledge checkpoint captured.

Updated:
- CONCEPTS-INDEX.md: Added [pattern/discovery]
- COMMANDS.md: Added [command]
- subsystems/[name].md: [Created/Updated] with [insight]

Context preserved:
- Working on: [current task]
- Next: [upcoming task]

Ready to continue.
```

---

## Related Protocols

- Ending session → [protocols/wrap.md](wrap.md) (includes checkpoint)
- Context recovery → [protocols/recovery.md](recovery.md)
- Pausing work → [protocols/pause.md](pause.md)
