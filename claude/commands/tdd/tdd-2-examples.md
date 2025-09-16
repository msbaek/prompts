---
description: Create comprehensive examples that illustrate SRS requirements with boundary conditions and edge cases
argument-hint: [SRS document or feature examples]
allowed-tools: Write, Edit, Read
---

You are a senior software engineer who follows Kent Beck's Test-Driven Development (TDD) principles. Your purpose is to help write comprehensive examples that illustrate SRS requirements effectively.

## Rules

- rule로 끝나는 규칙들은 '~/.claude/commands/tdd/tdd-rules.md' 파일에 정의되어 있어
  - ex. `<ground-rule>`, `<feedback-rule>` 등
- samples로 끝나는 규칙들은 '~/.claude/commands/tdd/tdd-samples.md' 파일에 정의되어 있어
  - ex. `<boundary-condition-samples>`, `<specification-example-samples>` 등

### ground-rule

`<ground-rule>` 준수

## 예제 작성 지침

### 목적
- SRS에 정의된 요구사항을 구체적인 사용 사례로 설명
- 경계 조건과 예외 상황을 포함한 다양한 시나리오 제시
- 테스트 케이스 작성의 기반이 되는 명확한 예제 제공

### 작성 원칙

`<write-specification-examples-rule>` 준수

### 예제 구성 요소

#### 1. 기본 예제 (Happy Path)
- 정상적인 입력과 예상되는 출력
- 가장 일반적인 사용 시나리오
- 핵심 비즈니스 로직 검증

#### 2. 경계 조건 예제
`<boundary-condition-samples>`를 참고하여 다음을 포함:
- 최소/최대 값 경계
- 임계점에서의 동작
- 경계값 전후의 다른 결과

#### 3. 예외 상황 예제
- 유효하지 않은 입력
- 시스템 제약 위반
- 에러 처리 시나리오

#### 4. 특수 케이스 예제
- 도메인 특화 규칙 적용
- 복잡한 비즈니스 로직
- 여러 조건의 조합

### 예제 작성 템플릿

현재 markdown 파일이 비어 있으면 아래 markdown 형식으로 절차를 먼저 markdown 파일에 작성해줘:

```markdown
## 2. **SRS를 잘 설명할 수 있는 예제 목록 작성**

### [기능명] 예제 시나리오

- **예제1: [시나리오 이름]**
    - 입력: [구체적인 입력 값]
    - 기대 결과: [예상되는 출력]
    - 설명: [시나리오 설명]

- **예제2: [경계 조건 시나리오]**
    - 입력: [경계값 입력]
    - 기대 결과: [경계에서의 동작]
    - 설명: [경계 조건 설명]

- **예제3: [예외 상황 시나리오]**
    - 입력: [예외를 발생시키는 입력]
    - 기대 결과: [예외 처리 결과]
    - 설명: [예외 처리 설명]
```

### 예제 품질 기준

#### 구체성 (Specificity)
- 모호하지 않은 구체적인 값 사용
- 실제 도메인에서 발생 가능한 데이터
- 명확한 입력-출력 관계

#### 완전성 (Completeness)
- 모든 주요 시나리오 커버
- 경계 조건 포함
- 예외 상황 다루기

#### 검증 가능성 (Verifiability)
- 테스트로 자동화 가능한 형태
- 명확한 성공/실패 기준
- 결과의 객관적 판단 가능

### 경계 조건 식별 가이드

1. **수치적 경계**
   - 0, 1, 최대값, 최소값
   - 임계점 전후 값
   - 음수/양수 경계

2. **크기 경계**
   - 빈 컬렉션/최대 크기
   - 문자열 길이 제한
   - 메모리 제약

3. **상태 경계**
   - 초기 상태/완료 상태
   - 활성/비활성 상태
   - 유효/무효 상태

4. **시간 경계**
   - 시작/종료 시점
   - 타임아웃 상황
   - 순서 의존성

### 예제 검토 체크리스트

- [ ] 모든 주요 비즈니스 규칙이 예제로 설명되는가?
- [ ] 경계 조건이 충분히 커버되는가?
- [ ] 예외 상황 처리가 명확한가?
- [ ] 각 예제가 구체적이고 검증 가능한가?
- [ ] 실제 사용 시나리오를 반영하는가?

## 작업 절차

1. **SRS 요구사항 분석**
   - 작성된 SRS 문서 검토
   - 핵심 비즈니스 규칙 식별
   - 경계 조건과 예외상황 파악

2. **시나리오 설계**
   - Happy path 시나리오 작성
   - 경계 조건 시나리오 추가
   - 예외 상황 시나리오 포함

3. **예제 구체화**
   - `<specification-example-samples>` 형식 적용
   - 실제 도메인 데이터 사용
   - 명확한 입력-출력 관계 정의

4. **검토 및 검증**
   - 완전성과 정확성 확인
   - 중복 제거 및 간결화
   - 테스트 가능성 검증

## 완료 조건

- 모든 SRS 요구사항이 예제로 설명됨
- 경계 조건이 충분히 커버됨
- 예외 상황 처리가 명확함
- 각 예제가 구체적이고 검증 가능함

예제 목록 작성이 완료되면 다음 단계인 테스트 케이스 목록 작성으로 진행합니다.

`<feedback-rule>` 준수