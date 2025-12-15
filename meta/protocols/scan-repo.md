# Protocol: >>scan-repo

**Trigger**: `>>scan-repo` or "scan the repository", "map the codebase"
**Purpose**: Scan repository and generate knowledge maps

---

## When to Use

Use `>>scan-repo` when:
- After `>>init-knowledge` to map structure
- Starting work on unfamiliar codebase
- Project structure has changed significantly
- Need to understand what exists

---

## Protocol Steps

### 1. Ensure Knowledge Directory

```bash
mkdir -p ai-agent/knowledge
```

### 2. Scan Directory Structure

Map the repository:
- Folder organization
- Key files in each directory
- Entry points (main, server, CLI)
- Configuration files
- Build and test setup

### 3. Create REPOSITORY-MAP.md

```markdown
# Repository Map

**Scanned**: [Date]
**Root**: [project-root]

## Directory Structure

```
project-root/
├── src/                    ← [Purpose]
│   ├── components/         ← [Purpose]
│   ├── services/           ← [Purpose]
│   └── utils/              ← [Purpose]
├── tests/                  ← [Purpose]
├── config/                 ← [Purpose]
└── [other directories]
```

## Entry Points
- **Main**: [path/to/main.ts]
- **Server**: [path/to/server.ts] (if applicable)
- **CLI**: [path/to/cli.ts] (if applicable)

## Configuration Files
- [config file 1]: [purpose]
- [config file 2]: [purpose]

## Build & Test
- **Build**: [command]
- **Test**: [command]
- **Dev**: [command]

## File Statistics
- Total files: [N]
- [Language 1]: [N] files
- [Language 2]: [N] files
```

### 4. Analyze Code Patterns

Scan for:
- Data models/schemas
- API endpoints/routes
- Utilities and helpers
- Design patterns
- Auth/authorization setup

### 5. Create CONCEPTS-INDEX.md

```markdown
# Concepts Index

**Last Updated**: [Date]

## Data Models
| Model | Location | Purpose |
|-------|----------|---------|
| User | src/models/user.ts | User entity |
| [Model] | [path] | [purpose] |

## API Endpoints
| Endpoint | Method | Location | Purpose |
|----------|--------|----------|---------|
| /api/users | GET | src/routes/users.ts:15 | List users |
| [endpoint] | [method] | [path:line] | [purpose] |

## Patterns & Conventions
- **[Pattern 1]**: [Description, where used]
- **[Pattern 2]**: [Description, where used]

## Key Utilities
| Utility | Location | Purpose |
|---------|----------|---------|
| [name] | [path] | [purpose] |

## Authentication
- Type: [JWT/Session/OAuth/etc.]
- Location: [path]
- Notes: [key details]
```

### 6. Confirm Completion

```
Scanning repository structure...

Created: ai-agent/knowledge/REPOSITORY-MAP.md
- [X] directories mapped
- [Y] entry points found
- [Z] configuration files documented

Created: ai-agent/knowledge/CONCEPTS-INDEX.md
- [N] data models cataloged
- [M] API endpoints mapped
- [P] patterns identified

Key findings:
- Architecture: [detected type]
- Entry point: [main file]
- Test framework: [detected framework]

Your knowledge base is ready! Use >>start [feature-name] to begin.
```

---

## Scanning Guidelines

### Do Scan
- Entry points and main workflows
- Repeated patterns
- Key abstractions
- Important dependencies
- Configuration structure

### Don't Over-Document
- Every single file
- Obvious self-explanatory code
- Generated files
- Dependencies/node_modules

### Keep Updates Manageable
- Focus on high-value information
- Can run multiple times as project evolves
- Update incrementally rather than full re-scan

---

## Token Considerations

For large repositories:
- Focus on src/ or main code directories first
- Skip generated/vendor directories
- Document structure, not every file
- Create subsystem docs for deep areas

---

## Related Protocols

- Initialize knowledge → [protocols/init-knowledge.md](init-knowledge.md)
- Starting work → [protocols/start.md](start.md)
- Knowledge checkpoint → [protocols/checkpoint.md](checkpoint.md)
