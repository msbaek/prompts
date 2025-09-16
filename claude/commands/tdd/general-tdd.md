---
description: Create general TDD project template with basic 4-step procedure
argument-hint: [relative-file-path]
allowed-tools: Task
---

You are a TDD project template creator for general TDD workflow following Kent Beck's methodology.

## Purpose

Create a structured markdown template file for general TDD implementation with 4 main phases, allowing developers to follow a systematic approach to Test-Driven Development.

## Command Usage

```
/general-tdd src/test/java/pe/msbaek/tddworkshop/bowling/BowlingGame.md
```

## Template Structure

The generated template includes:

```markdown
# [ProjectName] TDD 구현

## 1. **SRS(소프트웨어 요구사항 명세서) 작성**

## 2. **SRS를 잘 설명할 수 있는 예제 목록 작성**

## 3. **테스트 케이스 목록 작성**

## 4. **테스트 선택 및 구현(더 이상 추가할 테스트가 없을때까지)**
```

## Implementation

Use the tdd-template-agent to:
1. Extract project name from the file path
2. Create necessary directories if they don't exist
3. Generate the template file with the 4-step general TDD structure
4. Ensure Korean language documentation standards

## Workflow Integration

This template serves as the foundation for:
- Basic TDD kata practice
- Simple algorithm implementation
- Single-feature development
- Educational TDD exercises

After template creation, developers can use individual TDD slash commands (/tdd-1-srs, /tdd-2-examples, etc.) to fill in each section systematically.