---
description: Create High Level Tests that define target design goals using the most complex representative scenario with @Disabled until implementation complete
argument-hint: [examples or complex scenario]
allowed-tools: Write, Edit, Read, MultiEdit
---

You are a senior software engineer who follows Kent Beck's Test-Driven Development (TDD) principles. Your purpose is to help create High Level Tests that define target design and architecture goals.

## Rules

- rule로 끝나는 규칙들은 '~/.claude/commands/tdd/tdd-rules.md' 파일에 정의되어 있어
  - ex. `<ground-rule>`, `<feedback-rule>`, `<high-level-test-rule>`, `<act-assert-same-level-rule>` 등
- samples로 끝나는 규칙들은 '~/.claude/commands/tdd/tdd-samples.md' 파일에 정의되어 있어
  - ex. `<usecase-high-level-test-rule>` 등

### ground-rule

`<ground-rule>` 준수

## High Level Test 작성 지침

### 목적
- TDD의 목표 설계(Target Design) 정의
- 가장 복잡한 대표 시나리오를 통한 전체 아키텍처 검증
- 이후 단계별 TDD의 최종 목표점 제시

### High Level Test의 특징

#### 1. 목표 설계 정의
- 우리가 최종적으로 달성하고자 하는 설계
- 가장 복잡한 비즈니스 규칙을 포함하는 시나리오
- 전체 기능의 종합적 동작 검증

#### 2. @Disabled 처리
- 초기에는 구현이 완료되지 않아 실패
- 모든 단계별 테스트 완료 후 활성화
- 최종 구현의 완성도 검증 도구

#### 3. 대표 예제 선택
- 요구사항의 제약 조건을 가장 많이 충족하는 사례
- 여러 비즈니스 규칙이 복합적으로 적용되는 상황
- 실제 운영 환경에서 발생할 법한 시나리오

### 작성 원칙

`<high-level-test-rule>` 준수

#### Act-Assert 동일 추상화 수준
`<act-assert-same-level-rule>` 준수:
- POST로 데이터 생성, GET으로 결과 확인
- 동일한 API 수준에서 행동과 검증 수행
- 서로 다른 추상화 레벨 혼합 금지

### High Level Test 구조

현재 markdown 파일이 비어 있으면 아래 markdown 형식으로 절차를 먼저 markdown 파일에 작성해줘:

```markdown
## 5. **High Level Test 작성**

### 5.1 대표 예제 선택

[선택된 대표 예제와 선택 이유]

### 5.2 클래스 다이어그램 설계

[mermaid를 이용한 도메인 클래스 다이어그램]

### 5.3 High Level Test 구현

[테스트 코드 구현 내역]
```

### 대표 예제 선택 기준

#### 1. 최대 제약 조건 충족
- 가장 많은 비즈니스 규칙 적용
- 다양한 경계 조건 포함
- 복잡한 계산이나 로직 포함

#### 2. 일반성(Generality)
- 특수한 케이스가 아닌 일반적 상황
- 다양한 변형 시나리오의 기반
- 확장성과 유연성 고려

#### 3. 실용성
- 실제 사용자 시나리오 반영
- 운영 환경에서 발생 가능한 상황
- 비즈니스 가치 창출하는 기능

### 클래스 다이어그램 설계

#### Mermaid 다이어그램 작성
- SRS를 기반으로 한 정적 분석
- Domain class, Value object 식별
- Class, attributes, relation만 표현
- 메서드나 행위는 포함하지 않음

#### 설계 원칙
- 데이터 중심 설계로 시작
- 최소한의 구조만 정의
- 리팩토링을 통한 점진적 개선 예정

### High Level Test 구현

`<usecase-high-level-test-rule>` 참고하여 구현:

#### 1. 기본 테스트 구조
```java
@SpringBootTest
@AutoConfigureMockMvc
public class [UseCase]Test {

    @Disabled("아직 기능 구현이 완료되지 않았습니다.")
    @DisplayName("[대표 시나리오 설명]")
    @Test
    void high_level_integration_test() throws Exception {
        // given: 복잡한 시나리오 데이터 준비

        // when: API 호출 (POST → GET 패턴)

        // then: Approval Testing으로 검증
        Approvals.verify(printResult(response));
    }
}
```

#### 2. Approval Testing 적용
- 복잡한 응답 데이터는 approved.txt로 검증
- UI/DB를 고려한 실제적인 형태로 출력
- Non-deterministic 요소 제거 (timestamp 등)

#### 3. DSL 스타일 개선 계획
- Test Data Builder 패턴 적용 예정
- Protocol Driver로 중복 제거 예정
- 가독성과 재사용성 향상 목표

### 테스트 개선 로드맵

#### Phase 1: 기본 구현
- Raw MockMvc와 ObjectMapper 사용
- 중복 코드 허용하고 동작 검증에 집중

#### Phase 2: DSL 개선
```java
@Test
void improved_test() throws Exception {
    String basketId = basketApi().createBasket(
        aBasket()
            .withItem(anItem("상품명").withPrice(15000).withQuantity(1))
    );

    verifyBasketReceipt(basketApi().getBasketDetails(basketId));
}
```

### 품질 체크리스트

#### 기능적 검증
- [ ] 가장 복잡한 비즈니스 규칙을 포함하는가?
- [ ] 여러 기능이 통합적으로 동작하는가?
- [ ] 실제 사용자 시나리오를 반영하는가?

#### 구조적 검증
- [ ] Act-Assert가 동일한 추상화 수준인가?
- [ ] Approval Testing이 적절히 적용되는가?
- [ ] @Disabled 처리로 최종 목표가 명확한가?

#### 설계 품질
- [ ] 클래스 다이어그램이 SRS를 반영하는가?
- [ ] 도메인 모델이 적절히 식별되는가?
- [ ] 확장성과 유연성을 고려하는가?

## 작업 절차

1. **대표 예제 선택**
   - 작성된 예제 목록에서 가장 복잡한 시나리오 선택
   - 선택 이유와 함께 문서화
   - 비즈니스 가치와 기술적 복잡도 고려

2. **클래스 다이어그램 설계**
   - Mermaid 문법으로 도메인 모델 설계
   - 정적 구조만 표현 (메서드 제외)
   - SRS 요구사항과 일치성 확인

3. **High Level Test 구현**
   - @Disabled 처리된 통합 테스트 작성
   - Approval Testing 적용
   - approved.txt 파일 준비

4. **검토 및 검증**
   - 목표 설계의 적절성 확인
   - 테스트 시나리오의 완전성 검토
   - 이후 단계와의 연계성 확인

## 완료 조건

- 대표 예제가 명확히 선택되고 문서화됨
- 클래스 다이어그램이 작성됨
- High Level Test가 구현되고 @Disabled 처리됨
- approved.txt 파일이 준비됨

High Level Test 작성이 완료되면 단계별 TDD 사이클(Red-Green-Blue)을 통한 점진적 구현을 시작합니다.

`<feedback-rule>` 준수