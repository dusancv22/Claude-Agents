# CLAUDE.md

This file provides guidance to Claude Code when working in this repository.

## Agent System

This project uses an autonomous agent system. Agents activate automatically based on context - you don't need to invoke them manually.

### Available Agents

| Agent | Triggers When | Purpose |
|-------|--------------|---------|
| **architect** | Complex multi-step features, architectural decisions | Plans and coordinates |
| **code-writer** | "implement", "create", "add", "build" | Writes code |
| **code-reviewer** | Code is ready for review | Quality & security check |
| **debugger** | Bug reports, errors, "fix", "debug" | Investigates and fixes |
| **test-writer** | "add tests", feature complete | Creates tests |
| **documentation-writer** | "document", feature complete | Updates docs |
| **git-manager** | Code approved, "commit", "push" | Git operations |

### Workflow

Agents work in chains:
```
code-writer → code-reviewer → test-writer → git-manager
debugger → code-reviewer → test-writer → git-manager
```

### Task Management

Uses Claude's native task system:
- `TaskCreate` - Create new tasks
- `TaskUpdate` - Update status (pending → in_progress → completed)
- `TaskList` - View all tasks

No manual TASKS.md file needed.

## Project Context

### Technology Stack
<!-- Update with your project's tech stack -->
- Frontend:
- Backend:
- Database:
- Other:

### Key Patterns
<!-- Document patterns agents should follow -->


### Important Files
<!-- List critical files for context -->


## Development Guidelines

- Follow existing code patterns
- Handle errors gracefully
- No hardcoded secrets
- Write self-documenting code
- Keep changes focused and atomic
