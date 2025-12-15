# Meta-Feedback 009: Work Item Pause and Resume Protocol

**Date**: 2025-12-12
**Category**: Workflow
**Status**: Proposal
**Observed During**: Work item 003 (Catalogue Integration)

---

## Observation

During work item 003, the user needed to interrupt for a higher-priority issue. The current workflow system (FOR-AGENTS.md) defines states like "In Progress," "Draft," "Review," and "Finalize" but does not cover:

1. How to pause a work item mid-progress
2. What context to capture for easy resumption
3. How to resume paused work (same session or new session)

This is a common real-world scenario - work gets interrupted by urgent issues, context switches, or end-of-day.

---

## Current Gap

**FOR-AGENTS.md workflow states**:
- [ ] Not started
- [~] In progress
- [x] Complete

**Missing**:
- [P] Paused

**No guidance on**:
- What information to capture when pausing
- How to signal "ready to resume"
- How agent should re-orient when resuming

---

## Recommendation: PAUSED State Protocol

### 1. Status Convention

Add `PAUSED` as a valid work item status:

```markdown
**Status**: PAUSED - [Brief reason]
**Paused**: YYYY-MM-DD
```

In Quick Status tables, use `[P]`:
```markdown
| Phase | Status | Notes |
|-------|--------|-------|
| Draft | [P] PAUSED | Interrupted for [reason] |
```

### 2. Pause Context Section

When pausing, add a "Pause Context" section to 00-OVERVIEW.md containing:

```markdown
## Pause Context

**Paused on**: YYYY-MM-DD
**Reason**: [Why paused - user request, blocker, priority shift]
**Resume with**: `>>continue [item-number]` or read this OVERVIEW

**State at pause**:
- [What's done]
- [What's in progress]
- [Any blockers or pending questions]

**To resume**:
1. [First step to pick up]
2. [Second step]
3. [etc.]
```

### 3. Resume Protocol

**For Agent (new session)**:
1. Read 00-OVERVIEW.md of the work item
2. Check "Pause Context" section
3. Follow "To resume" steps
4. Update status back to "In Progress"

**For User**:
- Use `>>continue [item-number]` command
- Or simply say "let's resume work item 003"

### 4. Pause Triggers

Work items should be paused when:
- User explicitly requests pause/interrupt
- Blocker discovered that requires external input
- Higher-priority work item emerges
- End of session with incomplete work

Work items should NOT be paused when:
- Just waiting for user review (use "Awaiting Review" status instead)
- Work is complete (use "Ready for Finalize")

---

## Implementation Suggestion

### Update FOR-AGENTS.md

Add to "Work Item Lifecycle" section:

```markdown
### Pausing Work Items

When a work item must be interrupted:

1. Update status to `PAUSED - [reason]`
2. Add `**Paused**: YYYY-MM-DD` to header
3. Add "Pause Context" section with:
   - State at pause (what's done, what's pending)
   - Resume instructions (specific next steps)
4. Commit/save changes

To resume:
1. Read 00-OVERVIEW.md
2. Follow "To resume" steps in Pause Context
3. Update status back to "In Progress"
4. Remove or archive Pause Context section
```

### Add to Quick Commands

```markdown
- `>>pause [reason]` - Pause current work item with context
- `>>continue [item-number]` - Resume paused work item
```

---

## Benefits

1. **Context preservation** - No loss of progress or orientation when resuming
2. **Multi-session support** - Agent can pick up work across conversation boundaries
3. **Priority management** - Easy to switch between work items
4. **Transparency** - User sees exactly where things stand

---

## Example: Work Item 003 Pause

This pattern was applied ad-hoc to work item 003:

```markdown
**Status**: PAUSED - Awaiting Review
**Paused**: 2025-12-12

## Pause Context

**Paused on**: 2025-12-12
**Reason**: User interrupted for higher-priority issue
**Resume with**: `>>continue 003` or read this OVERVIEW

**State at pause**:
- All drafts complete in `90-OUTPUTS/`
- Ready for human review of deliverables
- No blocking issues

**To resume**:
1. Review `90-OUTPUTS/section-4-5-draft.md`
2. Review `90-OUTPUTS/appendix-a-altai-mapping.md`
3. Verify section numbers match actual M12 Report
4. Refine or `>>finalize`
```

---

## Decision Needed

- [ ] Accept this as standard protocol
- [ ] Modify approach
- [ ] Reject (keep workflow simple)

---

**Feedback from**: AI Agent (Claude)
**Applies to**: FOR-AGENTS.md workflow system
