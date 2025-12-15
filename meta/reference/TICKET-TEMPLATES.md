# Jira Ticket Templates for AI Collaboration

Guidelines for structuring Jira tickets to enable effective human-AI co-implementation.

---

## Core Principle

**Provide context, not just tasks.**

AI agents work best when they understand:
- **Why** this work matters (business context)
- **What** success looks like (acceptance criteria)
- **Where** to look (relevant code areas)
- **How much** freedom they have (constraints vs. open decisions)

---

## Ticket Size Tiers

Different ticket sizes need different levels of detail:

| Tier | Effort | Examples | Detail Level |
|------|--------|----------|--------------|
| **XS** | < 1 hour | Typo fix, config change, simple UI tweak | Minimal - just what & where |
| **S** | 1-4 hours | Bug fix, add field, simple feature | Basic - what, where, acceptance |
| **M** | 1-2 days | New component, API endpoint, integration | Standard - full template |
| **L** | 3-5 days | Multi-part feature, refactoring | Detailed - with design notes |
| **XL** | 1+ week | Major feature, architecture change | Consider splitting or use concept workflow |

---

## Minimal Template (XS/S Tickets)

```markdown
## Summary
[One sentence: what needs to happen]

## Context
[Why this is needed - 1-2 sentences]

## Acceptance Criteria
- [ ] [Criterion 1]
- [ ] [Criterion 2]

## Location Hints
- File(s): [path/to/relevant/file.ts]
- Related: [any related code or docs]
```

**Example - XS:**
```markdown
## Summary
Change the "Submit" button label to "Save Changes" on the profile page.

## Context
User research showed "Submit" feels too formal for a profile update.

## Acceptance Criteria
- [ ] Button text changed to "Save Changes"
- [ ] No other button labels affected

## Location Hints
- File: src/components/Profile/ProfileForm.tsx
```

---

## Standard Template (M Tickets)

```markdown
## Summary
[One sentence: what this feature/fix does]

## Business Context
[Why this matters - who benefits, what problem it solves]

## User Story (if applicable)
As a [role], I want [capability], so that [benefit].

## Acceptance Criteria
- [ ] [Specific, testable criterion 1]
- [ ] [Specific, testable criterion 2]
- [ ] [Specific, testable criterion 3]

## Technical Notes
### Relevant Code Areas
- [path/to/file.ts] - [what's here]
- [path/to/other.ts] - [what's here]

### Approach Hints (optional)
[If you have a preferred approach, mention it. Otherwise, let agent propose.]

### Constraints
- [Must use existing X]
- [Don't modify Y]
- [Performance requirement: Z]

## Out of Scope
- [What this ticket does NOT include]

## Dependencies
- Blocked by: [other tickets]
- Blocks: [other tickets]

## Questions for Discussion
- [Any open questions to resolve during implementation]
```

**Example - M:**
```markdown
## Summary
Add email notification when a user's subscription is about to expire.

## Business Context
Users are churning because they forget to renew. A reminder 7 days before
expiration should improve retention.

## User Story
As a subscribed user, I want to receive an email reminder before my
subscription expires, so that I can renew in time.

## Acceptance Criteria
- [ ] Email sent 7 days before expiration
- [ ] Email includes: expiration date, renewal link, current plan
- [ ] Email not sent if user already renewed
- [ ] Email not sent if user has auto-renew enabled
- [ ] Logs created for sent notifications

## Technical Notes
### Relevant Code Areas
- src/services/subscription/ - subscription logic
- src/services/email/ - email sending
- src/jobs/ - scheduled jobs

### Constraints
- Use existing EmailService (don't create new email mechanism)
- Must work with our job queue (Bull)

## Out of Scope
- SMS notifications (separate ticket)
- Multiple reminder emails (just one for now)

## Dependencies
- None

## Questions for Discussion
- Should we include a "snooze reminder" option?
```

---

## Detailed Template (L Tickets)

```markdown
## Summary
[Feature/change in one sentence]

## Business Context
[Detailed context: problem, opportunity, stakeholders affected]

## User Stories
1. As a [role], I want [X], so that [Y]
2. As a [role], I want [X], so that [Y]

## Acceptance Criteria
### Must Have
- [ ] [Critical criterion 1]
- [ ] [Critical criterion 2]

### Should Have
- [ ] [Important but not blocking]

### Nice to Have
- [ ] [If time permits]

## Technical Design
### Architecture Overview
[High-level approach - can be brief, agent will elaborate]

### Key Components
| Component | Purpose | New/Modified |
|-----------|---------|--------------|
| [Component] | [Purpose] | New |

### Relevant Code Areas
- [path] - [what & why relevant]

### API Changes (if applicable)
- New endpoints: [list]
- Modified endpoints: [list]

### Database Changes (if applicable)
- New tables/columns: [list]
- Migrations needed: [yes/no]

### Constraints
- [Technical constraints]
- [Business constraints]
- [Timeline constraints]

## Edge Cases to Consider
- [Edge case 1]
- [Edge case 2]

## Out of Scope
- [Explicit exclusions]

## Dependencies
- [Other tickets, external systems]

## Testing Notes
- [Key scenarios to test]
- [Known tricky areas]

## Open Questions
- [ ] [Question 1]
- [ ] [Question 2]

## Design Assets (if applicable)
- [Links to Figma, mockups, etc.]
```

---

## What Makes Tickets AI-Friendly

### ✅ Good Practices

1. **Specific acceptance criteria** with checkboxes
   - Agent knows exactly when done
   - Human can verify completion

2. **Location hints**
   - Reduces time searching codebase
   - Agent can focus on implementation

3. **Explicit constraints**
   - Prevents wrong approaches
   - Clarifies boundaries early

4. **Out of scope section**
   - Prevents scope creep
   - Agent knows where to stop

5. **Business context**
   - Agent makes better design decisions
   - Can suggest improvements

6. **Open questions explicitly marked**
   - Agent knows to ask before deciding
   - Prevents assumptions

### ❌ Avoid

1. **Vague criteria**: "Make it work better" → *How is "better" measured?*
2. **Missing context**: "Add X feature" → *Why? For whom?*
3. **Implicit constraints**: *If there's a preferred approach, say so*
4. **Assumed knowledge**: *Don't assume agent knows your conventions*
5. **Bundled scope**: *One ticket = one cohesive unit of work*

---

## Scaling Detail by Complexity

| Ticket Aspect | XS | S | M | L |
|---------------|----|----|----|----|
| Summary | ✓ | ✓ | ✓ | ✓ |
| Context | Brief | Brief | Yes | Detailed |
| User Story | - | Optional | Yes | Multiple |
| Acceptance Criteria | 1-2 | 2-4 | 4-8 | Prioritized |
| Technical Notes | File path | File + hint | Section | Design doc |
| Constraints | - | If any | Yes | Detailed |
| Out of Scope | - | If needed | Yes | Yes |
| Edge Cases | - | - | Consider | List |
| Open Questions | - | If any | Yes | Yes |

---

## From Ticket to Work Item

When starting work from a Jira ticket:

1. **Copy ticket content** to `inbox/` or directly to work item's `01-INPUTS/`
2. **Run `>>start feat [name]`** (or appropriate type)
3. **Agent reads ticket** and asks clarifying questions
4. **Iterate** until requirements are clear
5. **Agent creates implementation plan** based on ticket

The ticket becomes the primary input; agent may discover additional questions during implementation.

---

## Example: Same Feature, Different Sizes

### XS Version (bug fix)
```markdown
## Summary
Fix: Subscription renewal emails showing wrong expiration date.

## Acceptance Criteria
- [ ] Email shows correct date

## Location
- src/services/email/SubscriptionEmail.ts:45
```

### M Version (new feature)
```markdown
## Summary
Add subscription expiration reminder email (7 days before).

## Context
[As shown in standard template example above]
```

### L Version (notification system)
```markdown
## Summary
Build notification system for subscription lifecycle events.

[Would include: multiple event types, preferences, delivery channels,
templates, scheduling, retry logic, etc.]
```

---

## Quick Reference

**Always include:**
- Summary (what)
- Context (why)
- Acceptance criteria (done when)

**Scale up with complexity:**
- Technical notes (where to look)
- Constraints (must/must not)
- Out of scope (boundaries)
- Open questions (uncertainties)
