# Shared Agent Guidelines

This file contains common guidelines that all agents follow.

## Context Awareness

Before starting work:
1. Check `TaskList` for current tasks and priorities
2. Read `CLAUDE.md` in the project root if it exists
3. Read `PLANNING.md` if it exists for project context
4. Use `Task(subagent_type="Explore")` for unfamiliar codebases

## Task Management

Use Claude's native task tools:
- `TaskCreate` - Create tasks with subject, description, activeForm
- `TaskUpdate` - Update status: pending → in_progress → completed
- `TaskList` - View all tasks
- `TaskGet` - Get task details

Always mark tasks `in_progress` before starting and `completed` when done.

## Agent Handoff Protocol

When your work enables another agent, end your output with:

```
HANDOFF READY
Agent: [target-agent]
Status: [completed|needs-review|blocked]
Files: [list of modified files]
Context: [what the next agent needs to know]
Next: [suggested next steps]
```

Note: Handoffs are informational — the user decides whether to invoke the next agent.

## Strict Rules

- **NEVER** add "Co-Authored-By" lines to any commits or code
- **NEVER** commit secrets, credentials, or `.env` files
- **NEVER** use destructive git commands without explicit user request
- Only git-manager handles git operations — other agents should not stage, commit, or push
- Keep changes focused and atomic — don't refactor code you weren't asked to touch
- Don't over-engineer — solve the current problem, not hypothetical future ones

## Quality Standards

- Follow existing code patterns in the project
- Consider security implications
- Handle errors gracefully
- Write self-documenting code
- Optimize for solo developer maintainability

## Autonomy Principles

1. **Act when triggered** - Don't wait for explicit invocation if your trigger conditions are met
2. **Complete the task** - Follow through to natural completion
3. **Hand off appropriately** - Signal when the next agent could help
4. **Report blockers** - If stuck, clearly state what's needed
