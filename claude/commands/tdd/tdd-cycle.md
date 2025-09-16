---
description: TDD RGB 사이클 전체 진행
argument-hint: "[test-description] (선택사항)"
---

# TDD RGB 사이클 진행

테스트 설명: $ARGUMENTS

## 현재 상황 분석
!./gradlew test --tests "*Test" 2>/dev/null | grep -E "(PASSED|FAILED|test|BUILD)"

## RGB 사이클 순서

### 1. Red 단계
- 실패하는 테스트 작성
- approved.txt 파일 생성
- 사용자 검토 대기

### 2. Green 단계
- 상황 자동 분석
- 최적 구현 방법 선택 (Fake it/Triangulation/Obvious)
- 최소 구현으로 테스트 통과
- 사용자 검토 대기

### 3. Blue 단계
- Tidying 1-4단계 적용
- 가독성 개선 리팩토링
- 사용자 검토 대기

## 마이크로 사이클
각 단계는 2-3분 이내 작업으로 빠른 피드백을 받습니다.

## 참조 문서
@/Users/msbaek/git/LLM/prompts/claude/commands/tdd/web-usecase-tdd.md

지금 어느 단계부터 시작할까요?

1. `/tdd-red [테스트 설명]` - 새 테스트 작성
2. `/tdd-green` - 실패 테스트 통과
3. `/tdd-blue` - 리팩토링
4. `/tdd-status` - 현재 상황 확인