# Protocol: >>test

**Trigger**: `>>test` or "let's test", "create test checklist"
**Purpose**: Start testing phase with structured test scenarios

---

## Protocol Steps

### 1. Check for Existing Checklist

Does `04-TESTING-CHECKLIST.md` exist?
- If yes: Show existing checklist, ask if updates needed
- If no: Create from template

### 2. Analyze Implementation

Review completed implementation to identify:
- Happy path scenarios
- Edge cases
- Error conditions
- Regression risks (what could break)

### 3. Create/Update Testing Checklist

Populate `04-TESTING-CHECKLIST.md` with scenarios:

```markdown
# Testing Checklist: [Work Item Name]

## Happy Path Tests
- [ ] **Test 1**: [Description]
  - Steps: [How to test]
  - Expected: [Expected result]

- [ ] **Test 2**: [Description]
  - Steps: [How to test]
  - Expected: [Expected result]

## Edge Cases
- [ ] **Test 3**: [Description]
  - Steps: [How to test]
  - Expected: [Expected result]

## Error Handling
- [ ] **Test 4**: [Description]
  - Steps: [How to test]
  - Expected: [Expected result]

## Regression Tests
- [ ] **Test 5**: [Description]
  - Steps: [How to test]
  - Expected: [Expected result]

## Test Results
| Test | Status | Notes |
|------|--------|-------|
| Test 1 | [ ] Pass / [ ] Fail | |
```

### 4. Present to Human

```
Created 04-TESTING-CHECKLIST.md with [N] test scenarios:

Happy Path:
- Scenario 1: [Description]
- Scenario 2: [Description]

Edge Cases:
- Scenario 3: [Description]

Error Handling:
- Scenario 4: [Description]

Regression:
- Scenario 5: [Description]

Ready for testing. Update checklist as you test each scenario.
Use >>bug [description] to report any issues found.
```

---

## Test Scenario Structure

Each test should have:
- **Description**: What's being tested
- **Steps**: How to reproduce/test
- **Expected**: What should happen
- **Status**: Checkbox for Pass/Fail

---

## After Testing

When tests are complete:
1. Update checklist with results
2. Use `>>bug` for any failures that need fixing
3. Once all pass, work item can be archived

---

## Related Protocols

- Bug found during testing → [protocols/bug.md](bug.md)
- Archiving completed work → [protocols/archive.md](archive.md)
- Ending session → [protocols/wrap.md](wrap.md)
