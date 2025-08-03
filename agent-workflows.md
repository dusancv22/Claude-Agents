# Agent Workflows - Detailed Interaction Patterns

This document describes the detailed workflows and interaction patterns between agents in the Claude Agents system.

## Core Workflow Principles

1. **Single Source of Truth**: All agents reference shared files (PLANNING.md, TASKS.md) for context
2. **Clear Delegation Chain**: Architect coordinates, specialists execute
3. **Autonomous Operation**: Each agent operates independently within their role
4. **Quality Gates**: Code review and testing happen before commits
5. **Context Preservation**: All changes update relevant documentation

## Primary Workflows

### 1. New Feature Implementation Workflow

```mermaid
sequenceDiagram
    participant User
    participant Architect
    participant TaskManager as Task Manager
    participant ContextManager as Project Context Manager
    participant CodeWriter as Code Writer
    participant GitManager as Git Manager
    participant CodeReviewer as Code Reviewer
    participant TestWriter as Test Writer
    participant DocWriter as Documentation Writer

    User->>Architect: "I want to implement user authentication"
    
    Architect->>TaskManager: Create tasks in TASKS.md
    TaskManager->>TaskManager: Add specific implementation tasks
    
    Architect->>ContextManager: Update PLANNING.md with feature info
    ContextManager->>ContextManager: Add feature to planned features
    
    Architect->>CodeWriter: Implement authentication system
    CodeWriter->>CodeWriter: Write authentication code
    CodeWriter->>GitManager: Request micro-commit
    GitManager->>GitManager: Create micro-commit "feat: add auth components"
    
    CodeWriter->>CodeReviewer: Review authentication code
    CodeReviewer->>CodeReviewer: Check code quality, security
    
    alt Code Review Passes
        CodeReviewer->>TestWriter: Create tests for auth system
        TestWriter->>TestWriter: Write comprehensive tests
        TestWriter->>GitManager: Request micro-commit for tests
        GitManager->>GitManager: Create micro-commit "test: add auth tests"
        
        TestWriter->>DocWriter: Document authentication API
        DocWriter->>DocWriter: Update README and API docs
        DocWriter->>GitManager: Request micro-commit for docs
        GitManager->>GitManager: Create micro-commit "docs: update auth documentation"
        
        DocWriter->>GitManager: Create feature commit
        GitManager->>GitManager: Create feature commit "feat(auth): complete user authentication system"
        
        GitManager->>TaskManager: Mark tasks as completed
        TaskManager->>TaskManager: Update task status in TASKS.md
        
        TaskManager->>ContextManager: Update feature status
        ContextManager->>ContextManager: Move feature to completed in PLANNING.md
    else Code Review Fails
        CodeReviewer->>CodeWriter: Request fixes
        CodeWriter->>CodeWriter: Implement fixes
        Note over CodeWriter, CodeReviewer: Repeat until passes
    end
```

### 2. Bug Fix Workflow

```mermaid
sequenceDiagram
    participant User
    participant Architect
    participant TaskManager as Task Manager
    participant Debugger
    participant CodeWriter as Code Writer
    participant GitManager as Git Manager
    participant CodeReviewer as Code Reviewer
    participant TestWriter as Test Writer

    User->>Architect: "Login form validation is not working"
    
    Architect->>TaskManager: Create bug fix task
    TaskManager->>TaskManager: Add bug investigation task
    
    Architect->>Debugger: Investigate login validation bug
    Debugger->>Debugger: Analyze code, reproduce issue
    Debugger->>Debugger: Identify root cause
    
    Debugger->>CodeWriter: Implement bug fix
    CodeWriter->>CodeWriter: Fix validation logic
    CodeWriter->>GitManager: Request micro-commit
    GitManager->>GitManager: Create micro-commit "fix: correct email validation logic"
    
    CodeWriter->>CodeReviewer: Review bug fix
    CodeReviewer->>CodeReviewer: Verify fix and check for regressions
    
    CodeReviewer->>TestWriter: Add test to prevent regression
    TestWriter->>TestWriter: Create test for bug scenario
    TestWriter->>GitManager: Request micro-commit
    GitManager->>GitManager: Create micro-commit "test: add validation regression test"
    
    TestWriter->>GitManager: Create feature commit
    GitManager->>GitManager: Create commit "fix(auth): resolve email validation bug"
    
    GitManager->>TaskManager: Mark bug fix complete
    TaskManager->>TaskManager: Update TASKS.md
```

### 3. Code Quality Review Workflow

```mermaid
sequenceDiagram
    participant CodeWriter as Code Writer
    participant CodeReviewer as Code Reviewer
    participant Debugger
    participant TestWriter as Test Writer
    participant GitManager as Git Manager

    CodeWriter->>CodeReviewer: Review this new component
    
    CodeReviewer->>CodeReviewer: Check syntax and style
    CodeReviewer->>CodeReviewer: Verify security practices
    CodeReviewer->>CodeReviewer: Assess performance impact
    CodeReviewer->>CodeReviewer: Review maintainability
    
    alt Issues Found
        CodeReviewer->>CodeWriter: Issues found - need fixes
        Note over CodeReviewer: Lists specific issues:
        Note over CodeReviewer: - Security vulnerability in input handling
        Note over CodeReviewer: - Performance issue with large datasets
        Note over CodeReviewer: - Inconsistent error handling
        
        CodeWriter->>CodeWriter: Address issues
        CodeWriter->>CodeReviewer: Re-submit for review
        Note over CodeWriter, CodeReviewer: Repeat until approved
    else Code Approved
        CodeReviewer->>TestWriter: Code approved - create tests
        TestWriter->>TestWriter: Verify test coverage adequate
        
        alt Tests Pass
            TestWriter->>GitManager: Ready for commit
        else Tests Fail
            TestWriter->>Debugger: Tests reveal issues
            Debugger->>CodeWriter: Fix test failures
        end
    end
```

### 4. Task Management Workflow

```mermaid
sequenceDiagram
    participant Architect
    participant TaskManager as Task Manager
    participant Agents as Other Agents

    Architect->>TaskManager: Create new feature tasks
    TaskManager->>TaskManager: Add tasks to TASKS.md
    TaskManager->>TaskManager: Set initial status to pending
    
    loop For each task
        Agents->>TaskManager: Mark task as in-progress
        TaskManager->>TaskManager: Update status in TASKS.md
        
        Agents->>Agents: Complete work
        
        Agents->>TaskManager: Mark task as completed
        TaskManager->>TaskManager: Update status in TASKS.md
        TaskManager->>TaskManager: Count completed tasks
        
        alt Completed tasks >= 20
            TaskManager->>TaskManager: Create ARCHIVED_TASKS.md entry
            TaskManager->>TaskManager: Move completed tasks to archive
            TaskManager->>TaskManager: Clean up TASKS.md
            TaskManager->>TaskManager: Reset completed counter
        end
    end
```

### 5. Documentation Update Workflow

```mermaid
sequenceDiagram
    participant ContextManager as Project Context Manager
    participant DocWriter as Documentation Writer
    participant CodeWriter as Code Writer
    participant GitManager as Git Manager

    CodeWriter->>ContextManager: Feature implementation complete
    ContextManager->>ContextManager: Update PLANNING.md
    ContextManager->>ContextManager: Move feature to completed section
    ContextManager->>ContextManager: Add implementation details
    
    ContextManager->>DocWriter: Update related documentation
    DocWriter->>DocWriter: Check README.md for updates needed
    DocWriter->>DocWriter: Update API documentation
    DocWriter->>DocWriter: Add usage examples
    DocWriter->>DocWriter: Update troubleshooting guide if needed
    
    DocWriter->>GitManager: Request documentation commit
    GitManager->>GitManager: Create micro-commit "docs: update feature documentation"
```

## Agent Communication Patterns

### 1. Context Sharing

All agents access shared context through:

```
PLANNING.md → Current project state and architecture
TASKS.md → Active work and priorities  
Git History → Development timeline and changes
Code Files → Current implementation state
```

### 2. Status Updates

Agents update status through:

```
Task Manager → Updates task completion in TASKS.md
Project Context Manager → Updates feature status in PLANNING.md
Git Manager → Creates commit history for timeline
Documentation Writer → Updates README and docs
```

### 3. Quality Assurance Gates

Every code change goes through:

```
Code Writer → Implements change
↓
Git Manager → Creates micro-commit  
↓
Code Reviewer → Reviews quality
↓
Test Writer → Ensures test coverage
↓  
Documentation Writer → Updates docs
↓
Git Manager → Creates feature commit
```

## Error Handling Workflows

### 1. Code Review Failure

```
Code Reviewer identifies issues
→ Provides specific feedback
→ Code Writer addresses issues  
→ Re-submits for review
→ Repeat until approved
```

### 2. Test Failures

```
Test Writer runs tests
→ Tests fail
→ Debugger investigates failures
→ Code Writer implements fixes
→ Test Writer re-runs tests
→ Repeat until tests pass
```

### 3. Git Conflicts

```
Git Manager detects conflict
→ Analyzes conflicting changes
→ Resolves conflicts appropriately
→ Verifies resolution doesn't break functionality
→ Creates resolution commit
```

## Performance Optimization

### 1. Parallel Operations

Where possible, agents work in parallel:

```
Code Writer implements → Git Manager commits
                     ↓
Code Reviewer reviews → Test Writer creates tests
                     ↓
Documentation Writer updates docs
```

### 2. Context Efficiency

Agents minimize redundant file reads:

```
Read PLANNING.md once per workflow
Cache task status during operations
Share context between related operations
```

### 3. Commit Optimization

Git operations are batched when appropriate:

```
Multiple micro-commits → Single push
Related changes → Combined review
Documentation updates → Batched commits
```

## Troubleshooting Workflows

### Common Issues and Resolutions

1. **Agent Not Responding**
   - Check agent file exists in `.claude/agents/`
   - Verify agent has required tools
   - Confirm Claude Code can access files

2. **Context Out of Sync**
   - Have Project Context Manager refresh PLANNING.md
   - Task Manager updates TASKS.md status
   - Review git history for recent changes

3. **Quality Gates Failing**
   - Code Reviewer provides specific feedback
   - Debugger investigates test failures
   - Iterate until quality standards met

4. **Performance Issues**
   - Minimize agent tool usage
   - Batch related operations
   - Use specific rather than general agents

This workflow system ensures consistent, high-quality development while maintaining full automation and context preservation.