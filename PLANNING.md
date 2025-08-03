# PLANNING.md

## Project Overview

This is the Claude Agents system - a comprehensive development workflow automation using specialized AI agents for streamlined software development.

**Purpose**: Create a team of specialized Claude agents that work together to handle different aspects of software development, from planning to testing to deployment.

**Main Goals**:
- Automate repetitive development tasks
- Maintain high code quality through systematic reviews
- Provide checkpoint functionality through micro-commits
- Enable efficient solo development workflows
- Create reusable agent templates for future projects

## Technology Stack

- **Development Tools**: Claude Code CLI, Git
- **Documentation**: Markdown files (PLANNING.md, TASKS.md, README.md)
- **Agent System**: Claude subagents with specialized roles
- **Version Control**: Git with dual-commit strategy (micro + feature commits)
- **Target Languages**: React/JavaScript, Python, C#, RhinoCommon
- **Deployment**: Local development environment

## User Personas

### Primary User: Solo Developer (You)
- **Description**: Experienced developer working on multiple projects across different tech stacks
- **Needs**: 
  - Efficient development workflow
  - High code quality without manual oversight
  - Checkpoint/rollback functionality
  - Comprehensive documentation
  - Automated testing and reviews
- **Pain Points**:
  - Managing multiple aspects of development alone
  - Maintaining consistency across projects
  - Manual code reviews and testing
  - Context switching between different technologies
  - Losing work due to lack of checkpoints

## Features

### Completed Features
- **Agent System Architecture**: Designed and implemented 9 core agents with specialized roles - Added 2024-01-03
- **Architect Agent**: Main orchestrator for task delegation and workflow coordination - Added 2024-01-03
- **Project Context Manager**: Maintains PLANNING.md with comprehensive project information - Added 2024-01-03
- **Task Manager**: Manages TASKS.md with automatic archiving after 20 completed tasks - Added 2024-01-03
- **Code Writer**: Multi-technology code implementation (React, Python, C#, RhinoCommon) - Added 2024-01-03
- **Git Manager**: Dual-commit strategy with micro-commits and feature commits - Added 2024-01-03
- **Code Reviewer**: Comprehensive code quality checks (syntax, style, security, performance) - Added 2024-01-03
- **Debugger**: Systematic bug identification and fixing - Added 2024-01-03
- **Test Writer**: Comprehensive test suite creation and maintenance - Added 2024-01-03
- **Documentation Writer**: Technical documentation and API reference creation - Added 2024-01-03
- **Agent Communication Framework**: Clear workflow for agent interaction and coordination - Added 2024-01-03

### In-Progress Features
- Initial project setup and testing workflows

### Planned Features
- **Specialized Technology Agents**: React, Supabase, Python, C#, RhinoCommon specialists
- **Performance Optimizer Agent**: Code performance analysis and optimization
- **Security Auditor Agent**: Security vulnerability scanning and fixes
- **Deployment Agent**: Automated deployment and CI/CD management
- **Monitoring Agent**: Application monitoring and alert management
- **Migration Agent**: Database schema and code migration handling

## Architecture

### System Architecture
The agent system follows a hierarchical structure with the Architect as the main orchestrator:

```
Architect (Orchestrator)
├── Project Context Manager (PLANNING.md)
├── Task Manager (TASKS.md)
├── Code Writer (Implementation)
├── Git Manager (Version Control)
├── Code Reviewer (Quality Assurance)
├── Debugger (Issue Resolution)
├── Test Writer (Test Coverage)
└── Documentation Writer (Documentation)
```

### File Structure
```
.claude/
└── agents/
    ├── architect.md
    ├── project-context-manager.md
    ├── task-manager.md
    ├── code-writer.md
    ├── git-manager.md
    ├── code-reviewer.md
    ├── debugger.md
    ├── test-writer.md
    └── documentation-writer.md

CLAUDE.md
PLANNING.md (this file)
TASKS.md
ARCHIVED_TASKS.md (created when needed)
README.md
agent-workflows.md
.gitignore
```

### Agent Communication Flow
1. User provides requirement to Architect
2. Architect delegates to Task Manager for task creation
3. Project Context Manager updates PLANNING.md
4. Code Writer implements features
5. Git Manager creates micro-commits
6. Code Reviewer validates quality
7. Test Writer creates/updates tests
8. Documentation Writer updates docs
9. Git Manager creates feature commit
10. Task Manager marks tasks complete

## Development Guidelines

### Agent Interaction
- All agents have full autonomy within their roles
- Communication happens through shared files (PLANNING.md, TASKS.md)
- Clear delegation chains prevent conflicts
- Each agent references shared context before action

### Code Quality Standards
- All code must pass code reviewer checks
- Comprehensive test coverage required
- Documentation must be updated with changes
- Security considerations mandatory
- Performance impact assessed

### Git Workflow
- Feature branches for all new work
- Micro-commits for checkpoint functionality
- Clean feature commits for main history
- Conventional commit message format
- No direct commits to main branch

### Task Management
- All work tracked in TASKS.md
- Tasks archived after 20 completions
- Clear, actionable task descriptions
- Progress tracking in real-time
- Priority-based task organization

## Business Rules

1. **Checkpoint Principle**: Every small change must be committed for rollback capability
2. **Quality Gate**: No code proceeds without reviewer approval
3. **Documentation Currency**: All docs must stay current with code changes
4. **Test Coverage**: New features require corresponding tests
5. **Context Preservation**: PLANNING.md must reflect current project state
6. **Agent Autonomy**: Agents operate independently within defined roles
7. **Solo Optimization**: All workflows optimized for single developer

## Integration Points

- **Claude Code CLI**: Primary interface for agent interaction
- **Git Repository**: Version control and history management
- **Local File System**: Document and code storage
- **Development Environment**: IDE integration through file system

## Performance Considerations

- **Agent Efficiency**: Minimize token usage through targeted agent calls
- **File Management**: Lightweight task tracking with automatic archiving
- **Context Sharing**: Efficient information sharing through structured documents
- **Workflow Optimization**: Parallel agent operations where possible

## Security Measures

- **No Sensitive Data**: Agents never commit secrets or credentials
- **Code Review**: All code reviewed for security vulnerabilities
- **Access Control**: Agents have limited tool access based on roles
- **Audit Trail**: Complete git history for accountability

## Future Considerations

### Scalability
- Template system for creating new agent types
- Multi-project agent sharing
- Team collaboration extensions

### Enhancement Areas
- AI-powered performance optimization
- Automated security scanning
- Advanced deployment pipelines
- Real-time monitoring integration

### Technology Evolution
- Support for new frameworks and languages
- Cloud-native development workflows
- Container-based development environments
- Advanced testing strategies

---

*This document is maintained by the Project Context Manager agent and updated automatically as the project evolves.*