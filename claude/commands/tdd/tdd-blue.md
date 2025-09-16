---
description: TDD Blue 단계 - Tidying 1-4단계 경량 리팩토링
---

# TDD Blue 단계: 경량 리팩토링 (Tidying 1-4단계)

## Tidying 참조 문서
@/Users/msbaek/DocumentsLocal/msbaek_vault/003-RESOURCES/REFACTORING/Technique/Tidying.md

## 적용 단계 (1-4단계만)
1. **Reorder**: 관련 코드를 가까이 배치
2. **Chunk**: 빈 라인으로 논리적 블록 구분
3. **Comment**: 각 블록의 의도 설명
4. **Extract**: 좋은 이름을 붙일 수 있으면 메서드/변수 추출

## 적용하지 않는 것 (5단계 이후)
- Domain 로직 이동
- Domain Service/Value Object 발견
- Trimming
- 복잡한 구조 변경

## 진행 절차
1. 현재 코드 상태 분석
2. 가독성 개선이 필요한 부분 식별
3. Tidying 1-4단계 중 적절한 기법 선택
4. 한 번에 1-2개 개선만 수행
5. 테스트 통과 확인

**테스트는 절대 변경하지 않습니다!**

완료 후 사용자 검토를 기다립니다.