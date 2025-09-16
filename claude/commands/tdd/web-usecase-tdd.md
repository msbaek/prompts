---
description: Create web usecase TDD project template with comprehensive 9-step procedure
argument-hint: [relative-file-path]
allowed-tools: Task
---

You are a TDD project template creator for web usecase TDD workflow following Kent Beck's methodology and Spring Boot best practices.

## Purpose

Create a structured markdown template file for comprehensive web usecase TDD implementation with 9 main phases, allowing developers to follow a systematic approach to full-stack Test-Driven Development.

## Command Usage

```
/web-usecase-tdd src/test/java/pe/msbaek/tddworkshop/shopping/ShoppingBasket.md
```

## Template Structure

The generated template includes:

```markdown
# AI와 Pair로 [UseCase] Usecase를 TDD로 구현하기

## 전체적인 절차

## 1. **SRS(소프트웨어 요구사항 명세서) 작성**

## 2. **SRS를 잘 설명할 수 있는 예제 목록 작성**

## 3. **High Level Test 작성**

## 4. **테스트 케이스 목록 작성**

가장 단순한 특수 케이스(degenerate)에서 일반적인 케이스(general)로 진행하는 테스트 리스트:

- [ ] [첫 번째 테스트 - 보통 degenerate case]
- [ ] [두 번째 테스트 - 단순 case]
- [ ] [세 번째 테스트 - 일반적인 case]
- [ ] [네 번째 테스트 - 복잡한 case]

## 5. **Walking Skeleton 구현**

## 6. **테스트 리스트에서 테스트 선택해서 테스트 추가하기(더 이상 추가할 테스트가 없을때까지)**

### TDD 사이클 진행 방법:
1. **Red**: `tdd-red-agent` 사용 - 다음 체크되지 않은 테스트 구현
2. **Green**: `tdd-green-agent` 사용 - 최소 구현으로 테스트 통과
3. **Blue**: `tdd-blue-agent` 사용 - 코드 정리 및 리팩토링

### 진행 내역
[Red-Green-Blue 사이클을 진행하면서 각 테스트의 구현 내역을 간단히 기록]

## 7. **High Level Test 활성화**

## 8. **Jpa Repository 구현**

## 9. **테스트 코드 DSL 개선**
```

## Implementation

Use the tdd-template-agent to:
1. Extract usecase name from the file path
2. Create necessary directories if they don't exist
3. Generate the template file with the 9-step web usecase TDD structure
4. Ensure Korean language documentation standards

## Workflow Integration

This template serves as the foundation for:
- Full-stack web application development
- Spring Boot REST API implementation
- JPA entity and repository design
- End-to-end integration testing
- DSL-based test improvement

## Web Usecase TDD Features

The 9-step process includes:
- **High Level Test**: @Disabled integration test defining target architecture
- **Walking Skeleton**: End-to-end minimal implementation
- **JPA Repository**: Database layer implementation
- **DSL Improvement**: Test readability enhancement with builders and protocol drivers

After template creation, developers can use specialized TDD slash commands (/tdd-3-testlist, /tdd-4-skeleton, /tdd-5-highlevel) to implement each phase systematically with Spring Boot integration.