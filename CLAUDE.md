# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Common Commands

This repository contains no build system, but operates through prompt templates and configuration sync:

```bash
# Git post-commit hook automatically syncs slash commands to ~/.claude
git commit -m "Updated prompts"

# Check project structure
tree -d -L 3
```

## Extension Development Guidelines

When creating custom extensions for this prompt system:

- **Slash Commands**: Follow the official Claude Code documentation at https://docs.anthropic.com/en/docs/claude-code/slash-commands
- **Sub-agents**: Refer to the sub-agent guidelines at https://docs.anthropic.com/en/docs/claude-code/sub-agents

These resources provide comprehensive patterns and best practices for extending the system's capabilities.

## High-Level Architecture

This repository is a comprehensive prompt engineering workspace for AI-assisted software development, with particular focus on Test-Driven Development (TDD) and Kent Beck's methodologies.

### Directory Structure

- **claude/**: Core prompt system organized into specialized components
  - **agents/**: Specialized AI agent configurations for different development tasks
  - **commands/**: Slash command templates organized by domain
    - **tdd/**: TDD-specific prompts following Kent Beck's principles
    - **obsidian/**: Knowledge management and note-taking workflows
    - **tdp/**: Test-Driven development Patterns
  - **obsidian-presets/**: Configuration files for Obsidian vault operations

### Key Prompt Categories

#### TDD Development System

- **general-tdd.md**: Single-feature TDD workflow with AI pair programming
- **web-usecase-tdd.md**: Full-stack use case development with Spring Boot, REST, JPA
- **tdd-rules.md**: Comprehensive TDD rules and patterns following Kent Beck's three laws
- **tdd-samples.md**: Reference examples and approved test patterns

#### Specialized Agents

- **kent-beck-expert.md**: Kent Beck methodology guidance
- **tdd-expert.md**: TDD-specific expertise
- **spring-expert.md**: Spring ecosystem development
- **vibe-coding-coach.md**: Conversational application building
- **code-refactorer.md**: Code improvement without functionality changes

#### Development Workflow Integration

- Git post-commit hooks automatically sync prompts to `~/.claude/`
- Supports IntelliJ IDEA workflow with open file context
- Korean language support for documentation and communication

### Prompt Engineering Patterns

#### Reference System

- Rules defined in `tdd-rules.md` referenced as `<ground-rule>`, `<feedback-rule>`
- Samples defined in `tdd-samples.md` referenced as `<srs-samples>`, `<boundary-condition-samples>`
- Modular, reusable prompt components

#### TDD Workflow

1. SRS (Software Requirements Specification) creation
2. Example generation for specification validation
3. Test case list development
4. Iterative test implementation following red-green-refactor cycle
5. Walking skeleton for end-to-end architecture

#### Quality Assurance

- Approval testing patterns for complex output validation
- Boundary condition testing
- Feedback loops at each development stage
- Korean documentation standards

### Special Considerations

- **Pair Programming Focus**: Prompts designed for human-AI collaboration
- **Language Mixing**: Korean instructions with English code standards
- **Context Preservation**: Markdown documentation for session continuity
- **Incremental Development**: Emphasis on small, verifiable steps
- **No Premature Refactoring**: Explicit rules against early optimization

This system enables structured, methodical development with AI assistance while maintaining Kent Beck's TDD discipline and providing clear guidance for complex software engineering tasks.