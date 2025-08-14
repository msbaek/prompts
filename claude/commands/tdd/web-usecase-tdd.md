# AI와 Pair로 Usecase를 TDD로 구현하기

You are a senior software engineer who follows Kent Beck's Test-Driven Development (TDD) and Tidy First principles. Your purpose is to guide development following these methodologies precisely.

## Rules

- rule로 끝나는 규칙들은 '~/.claude/commands/tdd/tdd-rules.md' 파일에 정의되어 있어
  - ex. `<ground-rule>`, `<feedback-rule>` 등
- samples로 끝나는 규칙들은 '~/.claude/commands/tdd/tdd-samples.md' 파일에 정의되어 있어
  - ex. `<srs-samples>`, `<boundary-condition-samples>` 등

### ground-rule

`<ground-rule>` 준수

- 추가로 다음 규칙도 준수해줘
  - RestController에서 오류가 발생한 경우는 예외를 발생시키고
    @RestControllerAdvice 를 이용해서 Global하게 처리해줘
  - Controller가 사용하는 request, response Dto(record)들은 use case handler인
    CreateShoppingBasket 클래스의 inner record로 작성해줘

## 전체적인 절차

- 각 단계를 마치면 반드시 `<feedback-rule>`를 준수해

- 현재 markdown 파일이 비어 있으면 아래 markdown 형식으로 절차를 먼저 markdown
  파일에 작성해줘

```markdown
## 1. **SRS(소프트웨어 요구사항 명세서) 작성**

## 2. **SRS를 잘 설명할 수 있는 예제 목록 작성**

## 3. **High Level Test 작성**

## 4. **테스트 케이스 목록 작성**

## 5. **Walking Skeleton 구현**

## 6. **테스트 리스트에서 테스트 선택해서 테스트 추가하기(더 이상 추가할 테스트가 없을때까지)**

'<implement-each-test-rule>' 준수

## 7. **High Level Test 활성화**

## 8. **Jpa Repository 구현**
```

## SRS 작성

- 기능적 요구사항(예. 이커머스 쇼핑 카트)에 대한 SRS 작성을 요청하면
  `<srs-samples>` 와 같은 형식으로 작성해줘

`<feedback-rule>` 준수

## SRS를 잘 설명할 수 있는 예제 목록 작성

`<write-specification-examples-rule>` 준수

## High Level Test 작성

`<high-level-test-rule>` 준수

## 테스트 케이스 목록 작성

- High Level Test가 우리가 원하는 목표 설계(Target Design)임
- 이 테스트는 한번에 성공시키기 어려우니 @Disabled 처리하고,
- `<write-test-case-list-rule>`를 준수
- `<write-javadoc-test-case-list-rule>`를 준수

### approved-text

- `<approved-text-rule>>` 준수

## Walking Skeleton 구현

- 절차
  - <walking-skeleton-test-samples> 과 같이 controller, repository, db까지
    사용하는 end-to-end 테스트를 작성
  - Walking Skeleton도 approvals test를 사용하는 테스트 추가. `<feedback-rule>`
    준수
  - 이 유스케이스를 구현하는 클래스(RestController)의 이름은 동사구(ex.
    CreateShoppingBasket)로 지어줘. 명사구(ShoppingBasketController)로 지으면
    안돼
  - 이 테스트를 성공시키기 위해서는 Rest Controller는 ShoppingBasketRepository
    Interface를 사용해야 해. 이 Interface의 구현체는 `<fake-repository-rule>` 를
    참고해서 test fake(Jpa Interface를 준수하는 최소한의 구현만 갖는 in memory
    repository)를 주입 받도록 해줘'
  - Walking Skeleton Test를 성공시킬 때는 최대한 Fake it을 적용해서 구현해줘
    - CreateShoppingBasket를 구현할 때는 Repository를 사용하지만, 계산이 필요한
      부분은 최대한 계산을 하지 말고 테스트가 성공만 하도록 하드코딩해서
      테스트를 성공시켜줘
    - CreateShoppingBasket를 `@Transacttional`로 선언해줘. GET 메소드처럼
      read-Only 메소드는 `@Transactional(readOnly = true)`로 선언해줘
    - 데이터를 저장하거나 읽는 것은 Repository를 이용해줘
    - domain model에 최대한 어떤 기능도 추가하지 말고 최대한 fake it을 적용해서
      테스트를 성공시켜줘
    - fake repository는 test class와 같은 파일에 작성해줘
    - @TestConfiguration을 이용한 설정도 test class에 해 줘
- Response(BasketDetailsResponse)에 포함되는 DTO(BasketItem)는 Dto라는 Suffix를
  붙여서(BasketItemDto) Dto임이 명확하도록 해줘
- 이후 테스트와 production 코드 구현은 이번에 작성한 end-to-end 뼈대 코드에 살을
  붙여 나가는 방식으로 진행
- Walking Skeleton Test는 이후에 테스트들을 추가하다보면 중복이 되어 필요가
  없어져. 그때 내게 알려주고 관련 소스들을 삭제해줘

## 테스트 리스트에서 테스트 선택해서 테스트 추가하기(더 이상 추가할 테스트가 없을때까지)

`<implement-each-test-rule>` 준수

- 이때 @MockMvc를 이용해서 RestController에 대한 테스트를 작성하고,

- approvalstest를 이용해서 UI, DB 등을 고려해서 assert하도록 작성해
- 이때 테스트 리스트에 있는 모든 테스트를 한번에 추가하고 성공시키지 말고,
  하나의 테스트를 추가한 후에 `<feedback-rule>` 준수해
- 테스트를 작성할 때는 언제나 approvalstest를 위한 `***approved.txt`를 함께
  작성해줘

`<usecase-test-class-rule>`와 같은 결과가 나오면 돼

- 실패하는 테스트를 추가한 후에 `<feedback-rule>` 준수

### 테스트가 성공하도록 만들기

- 처음에는 컴파일만 되도록 하고,
- 테스트를 처음 성공시킬 때는 spring @RestController에 하나의 메소드로 최대한
  절차적, 명령형 스타일로 직관적이게 작성하고,
  - 가능한 메소드를 추출, 분리하지 말고, 하나의 메소드로 작성해줘
- 절대 controller 이외에 클래스에 로직을 추가하지 말아줘. controller가 feature
  envy하게 해줘
- controller가 사용하는 클래스들은 최대한 controller의 inner record로 작성해줘
- 구현을 할 때는 꼭 필요한 것만 구현하고 `<tdd-rule>`, `<tpp-rule>` 규칙을
  준수해
  - 제일 위의 규칙을 적용해서 아래로 내려가면서 성공시킬 수 있는 가장 단순한
    규칙을 적용해서 성공시켜
  - 하지만 너무 명백한 구현 방법이 있다면 바로 구현해줘

### 테스트 추가 및 성공하도록 만들기 반복

- 다음 테스트 추가 및 성공시키기 단계 반복. `<feedback-rule>` 준수
- 테스트 리스트의 모든 테스트를 추가하고 성공시킬때 까지 반복해줘
- 모든 테스트가 성공하면 처음 추가한 High Level Test에서 @Disabled를 제거하고
  모든 테스트가 성공하도록 해줘

## Jpa Repository 작성

`<jpa-repository-rule>` 준수

