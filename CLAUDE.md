# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This repository contains a comprehensive agent system designed to streamline development workflows. The agents work together autonomously to handle various aspects of software development.

## Agent System Architecture

### Core Agents

1. **Architect** (.claude/agents/architect.md)
   - Main orchestrator that analyzes requirements and delegates tasks
   - Creates implementation plans and manages workflow between agents

2. **Project Context Manager** (.claude/agents/project-context-manager.md)
   - Maintains PLANNING.md with project information
   - Updates documentation after feature implementations

3. **Task Manager** (.claude/agents/task-manager.md)
   - Maintains TASKS.md for active tasks
   - Archives completed tasks to ARCHIVED_TASKS.md after 20 completions

4. **Code Writer** (.claude/agents/code-writer.md)
   - Implements features across multiple tech stacks
   - Follows project conventions and patterns

5. **Git Manager** (.claude/agents/git-manager.md)
   - Creates micro-commits for checkpoint functionality
   - Manages feature branches and pull requests

6. **Code Reviewer** (.claude/agents/code-reviewer.md)
   - Reviews all code changes for quality
   - Checks syntax, style, security, performance, and best practices

7. **Debugger** (.claude/agents/debugger.md)
   - Identifies and fixes bugs
   - Provides detailed diagnostic reports

8. **Test Writer** (.claude/agents/test-writer.md)
   - Creates and maintains test suites
   - Ensures adequate test coverage

9. **Documentation Writer** (.claude/agents/documentation-writer.md)
   - Creates and updates technical documentation
   - Maintains code comments and README files

## Key Files

- **PLANNING.md** - Central project context document
- **TASKS.md** - Active task tracking
- **ARCHIVED_TASKS.md** - Historical task archive
- **agent-workflows.md** - Detailed agent interaction patterns

## Usage Instructions

### Starting a New Feature
1. Describe your requirement to the Architect agent
2. The system will automatically:
   - Create tasks in TASKS.md
   - Update PLANNING.md
   - Implement the feature with micro-commits
   - Review and test the code
   - Create a final feature commit

### Agent Commands
- Use `/agents` to see available agents
- Agents operate with full autonomy
- All agents have access to this context

## Development Workflow

1. **Micro-commits**: Every small change is committed for checkpoint functionality
2. **Feature branches**: All work happens on feature branches
3. **Automated reviews**: Code is reviewed before every commit
4. **Task tracking**: All work is tracked in TASKS.md
5. **Context maintenance**: PLANNING.md is kept up-to-date

## Important Notes

- Agents have full autonomy to make changes
- All code changes trigger micro-commits
- Tasks are automatically archived after 20 completions
- The system is designed for solo development workflows