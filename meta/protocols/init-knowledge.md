# Protocol: >>init-knowledge

**Trigger**: `>>init-knowledge` or "let's set up knowledge", "initialize project"
**Purpose**: Initialize project knowledge base through human input and QnA

---

## When to Use

Use `>>init-knowledge` when:
- Starting with a new project
- Knowledge base doesn't exist yet
- Project context is unclear
- Before first feature work

---

## Protocol Steps

### 1. Ensure Knowledge Directory

```bash
mkdir -p ai-agent/knowledge
mkdir -p ai-agent/knowledge/subsystems
```

### 2. Check Existing Knowledge

Look for `ai-agent/knowledge/SYSTEM-OVERVIEW.md`:
- If exists: Read it and identify gaps
- If doesn't exist: Full QnA needed

### 3. Prepare QnA Questions

Review what human already provided, then ask about missing info:

**Core Questions** (ask only if not already known):
1. What does this project do? What problem does it solve?
2. What domain is this in? (e.g., e-commerce, fintech, education)
3. What's the tech stack? (language, framework, database)
4. What's the high-level architecture? (monolith, microservices, etc.)
5. What are the major components or subsystems?
6. Are there important conventions or patterns I should know?
7. How do developers typically run this locally?
8. Are there any known gotchas or quirks?

### 4. Conduct QnA Session

Present questions to human:

```
I'll help set up your project knowledge base.

[If SYSTEM-OVERVIEW.md exists:]
I found your existing system overview. Let me ask a few questions to fill in gaps:

[If doesn't exist:]
I'll ask some questions to understand your project:

Questions:
1. [Question 1]
2. [Question 2]
...

Please answer what you can - partial answers are fine!
```

### 5. Create/Update SYSTEM-OVERVIEW.md

After receiving answers:
1. Merge human-provided content + QnA answers
2. Fill template completely (see template below)
3. Save to `ai-agent/knowledge/SYSTEM-OVERVIEW.md`

### 6. Confirm Completion

```
Created/Updated: ai-agent/knowledge/SYSTEM-OVERVIEW.md

Captured:
- Project purpose and domain
- Tech stack: [summary]
- Architecture: [summary]
- Key conventions: [count] documented

Next: Run >>scan-repo to map the codebase structure.
```

---

## SYSTEM-OVERVIEW.md Template

```markdown
# System Overview

**Project**: [Name]
**Domain**: [Domain/Industry]
**Last Updated**: [Date]

## Purpose
[What the project does, problem it solves]

## Tech Stack
- **Language**: [Primary language(s)]
- **Framework**: [Main framework(s)]
- **Database**: [Database(s) used]
- **Other**: [Key libraries, services]

## Architecture
[High-level architecture description]
- Type: [Monolith / Microservices / Serverless / etc.]
- [Key architectural patterns]

## Major Components
1. **[Component 1]**: [Purpose]
2. **[Component 2]**: [Purpose]
3. **[Component 3]**: [Purpose]

## Conventions
- [Naming conventions]
- [File organization patterns]
- [Code style notes]

## Development Setup
```bash
# How to run locally
[commands]
```

## Gotchas & Notes
- [Known quirk 1]
- [Important consideration]
- [Things to watch out for]
```

---

## Next Steps After Init

1. **Run `>>scan-repo`** - Map repository structure
2. **Start first feature** - `>>start feat [name]`
3. **Update incrementally** - Add subsystem docs as you learn

---

## Related Protocols

- Repository scanning → [protocols/scan-repo.md](scan-repo.md)
- Starting work → [protocols/start.md](start.md)
- Knowledge checkpoint → [protocols/checkpoint.md](checkpoint.md)
