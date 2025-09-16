---
description: TDD Green 단계 - 자동 판단하여 테스트 통과
---

# TDD Green 단계: 자동 판단 구현

## 현재 실패 테스트 확인
!./gradlew test --tests "*Test" 2>/dev/null | grep -A3 "FAILED\|FAILURE"

## 자동 판단 기준
상황을 분석하여 자동으로 최적 방법 선택:

1. **Fake it**: 첫 테스트이거나 새로운 기능
2. **Triangulation**: 유사한 테스트가 이미 존재
3. **Obvious**: 구현이 명백하고 간단한 경우

## TPP 규칙 적용
@/Users/msbaek/git/LLM/prompts/claude/commands/tdd/tdd-rules.md

## 진행 절차
1. 현재 실패하는 테스트 분석
2. 기존 코드 상황 파악
3. 최적 구현 방법 자동 선택
4. 선택 이유와 함께 최소 구현
5. 테스트 통과 확인

**사용자는 구현 방법을 지정하지 않습니다!**

완료 후 사용자 검토를 기다립니다.