# Protocol: >>bug

**Trigger**: `>>bug <description>` or "found a bug", "this is broken"
**Purpose**: Report and handle a bug during work

---

## When to Use

Use `>>bug` when:
- User reports a bug during development
- You discover a bug while working
- Testing reveals unexpected failures
- Something isn't working as expected

---

## Protocol Steps

### 1. Log the Bug

Append to `03-PROGRESS-LOG.md`:

```markdown
### 🐛 Bug: [Short description]

**Reported**: [Date]
**Description**: [From human or your observation]
**Severity**: [High/Medium/Low]

**Questions**:
1. Steps to reproduce?
2. Expected vs actual behavior?
3. Error messages or logs?
```

### 2. Gather Information

Ask human for reproduction steps (if not provided):

```
Bug logged in progress log.

Questions to help investigate:
1. How do you trigger this issue?
2. What did you expect to happen?
3. What actually happened?
4. Any error messages visible?

I'll investigate [likely file/area] after your answers.
```

### 3. Investigate

After getting answers:
1. Find likely location in code
2. Analyze root cause
3. Propose fix approach

### 4. Document Findings

Update progress log with investigation:

```markdown
**Investigation**:
- Root cause: [What's causing it]
- Location: [file.ts:line]
- Impact: [What's affected]

**Proposed Fix**:
- [Fix approach]
- [Files to modify]
```

### 5. Implement Fix

After human approval:
1. Make the fix
2. Test the fix
3. Update progress log with resolution

### 6. Update Progress Log

```markdown
**Resolution**:
- Fixed in: [file.ts:line]
- Approach: [What was done]
- Verified: [How you confirmed it's fixed]
```

---

## Bug During Testing

If bug found during `>>test` workflow:

1. Mark test as failed in `04-TESTING-CHECKLIST.md`
2. Follow bug protocol above
3. After fix, re-run test and mark as passed

---

## Creating Bug Work Items

For significant bugs that need their own tracking:

```bash
>>start bug [bug-description]
```

This creates a full work item folder:
- `ai-agent/work/NNN-bug-description/`
- Uses feature templates with lighter documentation
- Focus on reproduction, root cause, and fix

---

## Severity Guide

| Severity | Description | Response |
|----------|-------------|----------|
| High | Blocks work, crashes, data loss | Fix immediately |
| Medium | Incorrect behavior, workaround exists | Fix soon |
| Low | Minor issue, cosmetic, edge case | Fix when convenient |

---

## Related Protocols

- Testing workflow → [protocols/test.md](test.md)
- Starting bug work item → [protocols/start.md](start.md)
- Wrapping session after fix → [protocols/wrap.md](wrap.md)
