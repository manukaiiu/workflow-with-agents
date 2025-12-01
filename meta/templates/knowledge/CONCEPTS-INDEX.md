# Concepts Index

**Generated**: [Date]
**Purpose**: Catalog of discovered patterns, abstractions, and key concepts

## Design Patterns

### [Pattern Name]
**Location**: `[file:line]`
**Description**: [What pattern is used and why]
**Example**:
```
[Code example if helpful]
```

## Data Models

### [Model Name]
**Definition**: `[file:line]`
**Purpose**: [What data this represents]
**Key fields**:
- `[field]`: [type] - [purpose]
- `[field]`: [type] - [purpose]

**Related models**:
- [Model 2]
- [Model 3]

## API Endpoints

### [Category of endpoints]

#### `[METHOD] /path/to/endpoint`
**Handler**: `[file:line]`
**Purpose**: [What it does]
**Auth required**: [Yes/No]
**Parameters**:
- `[param]`: [type] - [description]

**Response**: [Description]

## Utilities & Helpers

### [Utility Name]
**Location**: `[file:line]`
**Purpose**: [What it does]
**Used by**: [List of files that use it]

## State Management

### [State container name]
**Type**: [Redux/Context/Zustand/etc.]
**Location**: `[file]`
**Manages**: [What state]
**Actions**:
- `[action]` - [What it does]

## Common Abstractions

### [Abstraction Name]
**Pattern**: [e.g., Factory, Builder, Repository]
**Location**: `[file:line]`
**Purpose**: [Why this abstraction exists]
**Usage**: [How to use it]

## Authentication & Authorization

**Method**: [JWT/Session/OAuth/etc.]
**Implementation**: `[file:line]`
**User model**: `[file:line]`
**Protected routes**: [How protection is applied]

## Database Access

**ORM/Query Builder**: [TypeORM/Sequelize/Prisma/etc.]
**Connection**: `[file:line]`
**Migrations**: `[location and how to run]`
**Common queries**: [Common patterns observed]

## Error Handling

**Strategy**: [How errors are handled globally]
**Custom errors**: `[file:line]`
**Logging**: `[file:line]`

## Configuration

**Method**: [Environment vars/config files/etc.]
**Location**: `[file]`
**Key settings**:
- `[setting]` - [purpose]

## Testing Patterns

**Framework**: [Jest/Pytest/etc.]
**Patterns observed**:
- [Pattern 1]
- [Pattern 2]

**Helper functions**: `[file:line]`
**Fixtures/Mocks**: `[location]`

## Build & Deployment

**Build command**: `[command]`
**Output**: `[directory]`
**Deployment**: [Method if discovered]

## Notable Dependencies

### [Dependency 1]
**Purpose**: [Why used]
**Version**: [version]
**Key usage**: `[file:line]`

## Cross-cutting Concerns

### Logging
**Library**: [winston/pino/etc.]
**Location**: `[file]`

### Validation
**Library**: [zod/joi/etc.]
**Location**: `[file]`

### Caching
**Method**: [Redis/in-memory/etc.]
**Location**: `[file]`
