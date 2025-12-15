# Protocol: >>archive

**Trigger**: `>>archive` or "work complete", "let's archive this"
**Purpose**: Complete work item and archive for reference

---

## When to Archive

Use `>>archive` when:
- All requirements/scope met
- All tests passing
- All implementation phases complete
- Ready to close out the work item

Do NOT archive when:
- Work is incomplete (use `>>pause` instead)
- Tests are failing
- Requirements unchecked

---

## Protocol Steps

### 1. Verify Completion

Check these documents:

**For Features/Bugs**:
- `01-REQUIREMENTS.md` - All checkboxes `[x]`?
- `04-TESTING-CHECKLIST.md` - All tests Pass?
- `02-IMPLEMENTATION-PLAN.md` - All phases `[x]`?

**For Maintenance**:
- `01-SCOPE.md` - All items `[x]`?
- `02-IMPLEMENTATION-PLAN.md` - All phases `[x]`?

**For Concepts**:
- All inputs processed (check INDEX.md)
- No unresolved questions in `08-OPEN-QUESTIONS.md`
- Use `>>finalize` instead for concepts

### 2. If Incomplete

```
Cannot archive - work not complete:
❌ [List incomplete items]

Complete these first, then use >>archive
```

### 3. If Complete

1. Create archive summary:
   - `archive/YYYY-MM-DD-[name]-FINAL.md`
   - Contains: completion summary, key decisions, lessons learned

2. Move old session summaries to archive/ (if any)

3. Keep core docs in folder (for reference)

4. Update `00-OVERVIEW.md`:
   - Status: "Complete"
   - Completed: [date]

### 4. Update Work Index

If `ai-agent/work/WORK-INDEX.md` exists:
- Move entry from "Active Work Items" to "Completed Work Items"
- Add completion date and one-line summary

### 5. Confirm to Human

```
Verifying completion...
✓ All requirements/scope met
✓ All tests passing
✓ All phases complete

Created: archive/YYYY-MM-DD-[name]-FINAL.md
Updated: 00-OVERVIEW.md (status: Complete)
Updated: WORK-INDEX.md (moved to Completed)

Work complete! 🎉
```

---

## Archive Behavior Clarification

The archive process does **NOT** move the work item folder. Instead:

1. **Work item folder stays in place** (`work/NNN-TYPE-name/`)
2. **Status updated** to "Complete" in OVERVIEW
3. **Archive subfolder created** with summary (`work/NNN-TYPE-name/archive/`)
4. **Core docs preserved** for future reference

This allows:
- Easy reference to completed work
- Historical context preserved
- Clear distinction via status in WORK-INDEX.md

---

## Archive Summary Template

```markdown
# Archive Summary: [Work Item Name]

**Completed**: YYYY-MM-DD
**Work Item**: NNN-TYPE-name
**Duration**: [Start date] to [End date]

## What Was Done
- [Key accomplishment 1]
- [Key accomplishment 2]
- [Key accomplishment 3]

## Key Decisions
- [Decision 1 and rationale]
- [Decision 2 and rationale]

## Files Changed
- [List of significant files modified/created]

## Lessons Learned
- [Any insights for future work]

## Reference
- Original requirements: 01-REQUIREMENTS.md
- Implementation plan: 02-IMPLEMENTATION-PLAN.md
- Progress log: 03-PROGRESS-LOG.md
```

---

## Related Protocols

- Testing before archive → [protocols/test.md](test.md)
- Ending session without archiving → [protocols/wrap.md](wrap.md)
- Concept finalization → [protocols/concept/finalize.md](concept/finalize.md)
