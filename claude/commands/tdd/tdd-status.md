---
description: TDD 진행 상황 확인
---

# TDD 진행 상황 체크

## 현재 테스트 상태
!./gradlew test --tests "*Test" --info 2>/dev/null | tail -10

## Git 상태 확인
!git status --porcelain

## 변경사항 확인
!git diff --stat

## 테스트 리스트 확인
현재 테스트 파일에서 테스트 리스트를 확인합니다:
@src/test/java/pe/msbaek/tdd_workshop/shopping/CreateShoppingBasketTest.java

## TDD 진행 가이드
- **Red**: 실패하는 테스트가 있나요?
- **Green**: 모든 테스트가 통과하나요?
- **Blue**: 리팩토링이 필요한 중복이 있나요?

## 다음 단계 추천
현재 상황에 따른 다음 단계를 추천합니다:

1. 실패하는 테스트가 있으면 → `/tdd-green`
2. 모든 테스트가 통과하고 중복이 있으면 → `/tdd-blue`
3. 새로운 테스트가 필요하면 → `/tdd-red [테스트 설명]`