# Shared Agent Guidelines

This file contains common guidelines that all agents follow.

## Context Awareness

Before starting work:
1. Check `TaskList` for current tasks and priorities
2. Read `PLANNING.md` if it exists for project context
3. Use `Task(subagent_type="Explore")` for unfamiliar codebases

## Task Management

Use Claude's native task tools:
- `TaskCreate` - Create tasks with subject, description, activeForm
- `TaskUpdate` - Update status: pending → in_progress → completed
- `TaskList` - View all tasks
- `TaskGet` - Get task details

Always mark tasks `in_progress` before starting and `completed` when done.

## Agent Handoff Protocol

When your work enables another agent:

```
HANDOFF READY
Agent: [target-agent]
Status: [completed|needs-review|blocked]
Files: [list of modified files]
Context: [what the next agent needs to know]
Next: [suggested next steps]
```

## Git Integration

After making code changes:
1. Stage specific files (never `git add .`)
2. Use conventional commit format: `type(scope): description`
3. Use HEREDOC for multi-line commit messages

## Quality Standards

- Follow existing code patterns in the project
- Consider security implications
- Handle errors gracefully
- Write self-documenting code
- Optimize for solo developer maintainability

## Autonomy Principles

1. **Act when triggered** - Don't wait for explicit invocation if your trigger conditions are met
2. **Complete the task** - Follow through to natural completion
3. **Hand off appropriately** - Enable the next agent in the workflow
4. **Report blockers** - If stuck, clearly state what's needed
