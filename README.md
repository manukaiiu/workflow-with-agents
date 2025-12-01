# Workflow with Agents

A streamlined meta-documentation system for human-agent collaboration on software projects.

## What is this?

A simple, structured workflow system that helps AI agents and humans work together effectively on feature development. The system provides:

- **Multiple features** - Work on several features in parallel, each in its own numbered folder
- **Knowledge retention** - AI builds and maintains project knowledge across sessions
- **Clear workflows** - Simple `>>` commands that expand to full protocols
- **Zero context loss** - Resume work in under 2 minutes, every time

## Quick Start

### 1. Copy to your project

```bash
# In your project root, create the ai-agent directory
mkdir -p ai-agent

# Copy the meta folder (contains system templates and docs)
cp -r meta ai-agent/
```

The agent will automatically create `features/` and `knowledge/` folders when needed.

### 2. Point the agent to the system

**First time only** - Tell the agent about this meta system:

```
Please read ai-agent/meta/FOR-AGENTS.md - this explains our workflow system.
```

The agent will read the documentation and understand how to work with you.

### 3. Initialize knowledge

Now start knowledge setup:

```
Human: >>init-knowledge
AI: [Asks questions about your project]
AI: [Creates knowledge/SYSTEM-OVERVIEW.md]

Human: >>scan-repo
AI: [Scans your codebase]
```

### 4. Start your first feature

```
Human: >>start my-first-feature
AI: [Creates feature folder, asks questions]
```

## Documentation

**For humans**: Read [ai-agent/meta/FOR-HUMANS.md](meta/FOR-HUMANS.md)
**For AI agents**: Read [ai-agent/meta/FOR-AGENTS.md](meta/FOR-AGENTS.md)
**System overview**: See [ai-agent/meta/README.md](meta/README.md)

## Features

- ✅ Multiple concurrent features in numbered folders
- ✅ Project knowledge accumulation
- ✅ Agent compliance reminders
- ✅ Template-based workflows
- ✅ Zero redundancy

## License

Free to use and modify for your projects.
