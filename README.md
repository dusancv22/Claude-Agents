# Claude Agents - Autonomous Development Workflow

A streamlined system of specialized Claude agents that activate automatically based on context, eliminating the need for manual orchestration.

## Key Features

- **7 Specialized Agents** - Each with clear trigger conditions
- **Autonomous Activation** - Agents start when needed, no manual invocation
- **Native Task Management** - Uses Claude's built-in task system
- **Chain Workflows** - Agents hand off to each other automatically
- **Solo Developer Optimized** - Designed for individual workflows

## Quick Start

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/yourusername/claude-agents.git
   ```

2. **Copy agents to your Claude config**
   ```bash
   # Windows
   copy claude-agents\.claude\agents\* %USERPROFILE%\.claude\agents\

   # macOS/Linux
   cp claude-agents/.claude/agents/* ~/.claude/agents/
   ```

3. **Copy CLAUDE.md to your project** (optional template)
   ```bash
   cp claude-agents/CLAUDE.md your-project/CLAUDE.md
   ```

### Usage

Just describe what you want. Agents activate automatically:

- "Add a login form" → code-writer activates
- "This button doesn't work" → debugger activates
- "Review the changes" → code-reviewer activates
- "Commit these changes" → git-manager activates
- "Add tests for the auth module" → test-writer activates

## Agent Overview

| Agent | Activates When | Does What |
|-------|---------------|-----------|
| **architect** | Complex features, unclear scope, architectural decisions | Plans, breaks down tasks, coordinates |
| **code-writer** | "implement", "create", "add", "build" requests | Writes and modifies code |
| **code-reviewer** | Code ready for review, security audit needed | Reviews quality, security, performance |
| **debugger** | Bug reports, errors, "doesn't work" | Investigates and fixes issues |
| **test-writer** | Tests needed, feature complete | Creates test suites |
| **documentation-writer** | Docs needed, feature complete | Updates documentation |
| **git-manager** | Code approved, commit/push requested | Handles git operations |

## Workflow Chains

Agents automatically hand off to each other:

```
New Feature:
  code-writer → code-reviewer → test-writer → git-manager

Bug Fix:
  debugger → code-reviewer → test-writer → git-manager

Documentation:
  documentation-writer → git-manager
```

## Task Management

Uses Claude's native task tools instead of manual files:

```
TaskCreate  - Create tasks with descriptions
TaskUpdate  - Mark in_progress or completed
TaskList    - View all tasks and status
TaskGet     - Get full task details
```

## File Structure

```
.claude/
└── agents/
    ├── _agent-common.md       # Shared guidelines
    ├── architect.md           # Complex feature planning
    ├── code-writer.md         # Implementation
    ├── code-reviewer.md       # Quality assurance
    ├── debugger.md           # Bug investigation
    ├── test-writer.md        # Test creation
    ├── documentation-writer.md # Documentation
    └── git-manager.md        # Version control
```

## Customization

### Adding Project Context

Create a `CLAUDE.md` in your project root with:
- Technology stack
- Key patterns to follow
- Important files
- Business rules

### Modifying Agents

Edit files in `~/.claude/agents/` to:
- Adjust trigger conditions
- Add technology-specific guidelines
- Modify handoff behavior

## Changes from v1

- Removed `task-manager` (replaced by native task tools)
- Removed `project-context-manager` (merged into other agents)
- Added autonomous trigger conditions
- Added agent handoff protocol
- Streamlined from 9 to 7 agents

## License

MIT - Use, modify, and distribute freely.
