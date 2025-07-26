# TDD 규칙 및 설정

이 파일은 TDD(테스트 주도 개발) 진행 시 Claude와 함께 작업할 때 필요한 기본 규칙과 설정을 포함합니다.

## ground-rule

<ground-rule>

```markdown
- 모르는 정보면 모른다고 확실히 대답해
- 내 요청에 답변하기 위해 내게 필요한 정보가 있으면 요청에 답변하기 전에 내게 관련된 질문을 해줘
    - ex. 내가 SRS 작성을 요청했는데 정보가 부족하면 간결하게 질문해줘
        - 단어와 column no를 입력 받아서 줄바꿈을 삽입하는 기능을 구현하기를 구현할 때 column no가 단어의 길이보다 작은 경우 단어를 잘라야 하는지 ? 자르지 말아야하는지 ?
          등은 내게 물어보고 SRS를 작성해줘
- 코드는 모두 최신 java, spring-boot 기준으로 작성해. use Context7
- 내가 요청하지 않는 한 리팩터링하지 말고, 절차적, 명령형 스타일로 하나의 메소드로 작성해서 직관적이고 이해하기 쉽게 작성해줘.
    - 최대한 메소드 추출(extract method)이나 변수 추출(extract variable / field)을 하지마. 이건 나중에 내가 할거야.
- "빌드", "테스트 실행", "커밋" 등 실행과 관련된 일은 내가 할테니 너는 시도하지 말어.
- 금액, 거리, 무게 등은 대한민국 기준으로 처리해줘
- getter, setter 등은 lombok을 이용해서 간결하게 작성해줘, 최대한 record를 많이 활용해줘
- 테스트를 작성할 때는
    - approved.txt 파일 생성이 가능하면 이 파일을 생성하고 기대되는 결과를 채워줘
    - 단순히 한 두개의 값만 비교하면 되는 경우(bowling game의 score, 계산기의 연산 결과 등)처럼 approvals test를 적용하기엔 검증이 너무 단순한 경우는 assertj의
      assertThat() 사용해서 검증해줘
    - 네가 판단하기 어려우면 assert를 작성하기 전에 내게 물어봐줘
    - 'general-tdd-rules.md의 <approved-text-samples> 섹션' 준수
- Class 파일에 코드를 추가할 때는 중요한 public method가 먼저 나오고, private 메소드가 가장 나중에 나오게 해줘.
- 코드나 파일을 읽고 쓰기 위해 intellij 툴을 사용할 때는 'general-tdd-rules.md의 <feedback-rule> 섹션'을 준수해줘
- 마크다운 문서를 확인하고 "## 전체적인 절차"의 각 단계가 없으면 절차를 먼저 마크다운 문서에 작성하고 그 절차에 맞게 진행하자. 그리고 마크다운 문서는 한글로
  작성해줘.
- "## 전체적인 절차"의 각 단계를 마치면
    - 관련된 markdown 파일에 현재 진행 내역을 작업 절차의 각 단계 중 적합한 절차 영역에 작성해줘
    - 이때 최대한 기존에 작성된 내용을 변경하지 말고, append only로 갱신해줘
- 코드를 추가할 때는 반드시 'general-tdd-rules.md의 <tdd-rule> 섹션'을 준수해줘
- 대화(새로운 chat)를 시작할 때는 'general-tdd-rules.md의 <session-start-rule> 섹션' 규칙을 준수해줘
```

</ground-rule>

### test-desiderta-rule

<test-desiderta-rule>

- Isolated — tests should return the same results regardless of the order in which they are run.
- Composable — if te ests are isolated, then I can run 1 or 10 or 100 or 1,000,000 and get the same results.
- Fast — tests should run quickly.
- Inspiring — passing the tests should inspire confidence
- Writable — tests should be cheap to write relative to the cost of the code being tested.
- Readable — tests should be comprehensible for reader, invoking the motivation for writing this particular test.
- Behavioral — tests should be sensitive to changes in the behavior of the code under test. If the behavior changes, -
  the test result should change.
- Structure-insensitive — tests should not change their result if the structure of the code changes.
- Automated — tests should run without human intervention.
- Specific — if a test fails, the cause of the failure should be obvious.
- Deterministic — if nothing changes, the test result shouldn’t change.
- Predictive — if the tests all pass, then the code under test should be suitable for production.

</test-desiderta-rule>

### feedback-rule

<feedback-rule>

```markdown
- 한 단계에서 관련된 코드를 생성한 후에는 반드시 내게 피드백을 구해
- 내가 보고 수정이 필요하면 수정을 할거야
- 내가 명시적으로 다음 단계로 진행하는 것을 결정해야만 다음 단계로 진행해줘
- 피드백이 필요할 때마다 다음 형식으로 질문해: "이 [구현/테스트/설계]에 대한 피드백을 주시겠어요? 특히 [집중해야 할 부분]에 대해서요."
```

</feedback-rule>

### tdd-rule

<tdd-rule>

```markdown
- 'general-tdd-rules.md의 <three-laws-of-tdd-rule> 섹션' 준수
- don't write code without a failing test.
- only write the code necessary to get the test to pass(little gold game).
    - 'general-tdd-rules.md의 <make-it-work-rule> 섹션' 준수
- never delete tests without express permission.
- 테스트를 추가할 때는 반드시 한번에 하나씩 추가해. 실패하는 테스트가 있을 때는 절대 새로운 테스트를 추가할 수 없어.
```

</tdd-rule>

### three-laws-of-tdd-rule

<three-laws-of-tdd-rule>

- "Write NO production code except to pass a failing test."
- "Write only ENOUGH of a test to demonstrate a failure."
- "Write only ENOUGH production code to pass the test."

</three-laws-of-tdd-rule>

### session-start-rule

<session-start-rule>

```markdown
- 대화를 시작할 때는 지금 열려 있는 jetbrains intellij 프로젝트의 각 탭에 있는
  파일들을 확인해줘.
- 확인할 파일들은
    - 기능명.java(ex. ChangePassword.java, BowlingGame.java)
    - 기능명Test.java(ex. ChangePasswordTest.java, BowlingGameTest.java)
    - 기능명.md(ex. ChangePassword.md, BowlingGame.md)
    - 등이야.
- jetbrains intellj에서 필요한 파일들이 열려 있지 않으면 내게 필요한 파일들을
  열어달라고 요청해
```

</session-start-rule>

## implement-each-test-rule

<implement-each-test-rule>

```markdown
- 새로운 테스트를 추가하고 코드를 구현할 때는 다음과 같은 절차를 따라줘.
    - 'general-tdd-rules.md의 <tdd-rule>' 준수
    - **실패하는 테스트** 추가
        - '<test-desiderta-rule>' 준수
    - 최소한의 코드로 테스트가 성공하도록 구현을 추가(little golf game, 'general-tdd-rules.md의 <make-it-work-rule>' 준수)
        - 이때는 'general-tdd-rules.md의 <tpp-rule>' 준수
        - 하나의 테스트가 성공하면 javadoc comment에 있는 테스트 항목에 완료 표시('X')를 해줘
    - 작업한 내역을 마크다운 파일에 반영
        - 각각의 테스트에 대한 작업 내역을 '### n.x' 레벨로 추가
        - multiline git commit message 수준으로 작성해줘
        - "gutter test 추가"처럼 제목을 달고, 빈칸 넣고, 다음 라인에 이번 테스트
          구현에 주목할 만한 내용들을 2~3줄 정도라 작성해줘
        - code는 markdown 파일에 추가하지 말아줘
    - 중복 제거가 필요한 경우 리팩터링을 통해 중복 제거
    - 내게 피드백 구하기
        - "이 테스트 구현에 대한 피드백을 주시겠어요? 특히 [구현 방식/테스트 명확성/코드 품질] 부분에 대해서요."
```

</implement-each-test-rule>

## make-it-work-rule

<make-it-work-rule>

1. Obvious implementation:
    - 구현 방법이 명확할 때 직접 올바른 코드 작성
    - 단, Getting Stuck 위험 있음
2. Fake it till you make it:
    - 하드코딩이라도 테스트를 통과시키기에 필요한 최소한의 코드만 작성
    - 다음 테스트를 통해 코드를 일반화
3. Triangulation:
    - 두 개 이상의 테스트 케이스가 있어야 코드를 일반화할 수 있음
    - 테스트가 1개만 있다면 코드는 상수를 반환해서 fake it 가능
    - 하지만 동일 기능에 또 다른 결과를 기대하는 테스트가 있다면 fake it 불가
    - 삼각측량처럼 여러 각도에서 같은 함수를 테스트

- 이 단계에서는
    - 최대한 빠르게 안정된 상태(테스트가 성공하는)로 돌아가는 것이 중요
    - 우리는 문제를 풀기 전까지는 문제를 정확히 이해하지 못하고, 발견 가능한 이슈를 예상할 수 없다. 그래서 최대한 빨리
      끝까지 풀어봐야 한다.
- 분명한 구현 방법이 있다면 바로 적용
- 빠르게 해결할 수 없다면 fake it. 그리고 테스트가 거짓말을 하지 못하도록 triangulate
- 코드를 작성할 때는 최대한 'general-tdd-rules.md의 <tpp-rule>'을 준수

</make-it-work-rule>

### tpp-rule

<tpp-rule>

```markdown
1. ({} → nil): No code at all → Code that returns or employs nil
    - 코드가 없는 상태에서 null을 반환하거나 사용하는 코드를 작성
    - 예: 빈 메서드에 return null; 추가

2. (nil → constant): Replace nil with a constant value
    - null을 상수값으로 대체
    - 예: return null; → return 0;

3. (constant → constant+): Replace a simple constant with a more complex constant
    - 단순 상수를 더 복잡한 상수로 대체
    - 예: return 0; → return new int[]{0, 0};

4. (constant → scalar): Replace a constant with a variable or argument
    - 상수를 변수나 매개변수로 대체
    - 예: return 0; → return pins;

5. (statement → statements): Add more unconditional statements
    - 더 많은 조건문이 아닌 문장 추가
    - 예: 메서드에 로깅 문장 추가

6. (unconditional → if): Introduce a conditional (split the execution path)
    - 조건문 도입 (실행 경로 분기)
    - 예: return score; → if (isStrike()) return strikeScore(); else return score;

7. (scalar → array): Replace a scalar with an array
    - 스칼라를 배열로 대체
    - 예: int score → int[] scores

8. (array → container): Replace an array with a more complex container
    - 배열을 더 복잡한 컨테이너로 대체
    - 예: int[] scores → List<Score> scores

9. (statement → tail-recursion): Replace a statement with a tail-recursive structure
    - 문장을 꼬리 재귀 구조로 대체
    - 예: for 반복문을 재귀 호출로 변환

10. (if → while): Replace a conditional with a loop
    - 조건문을 반복문으로 대체
    - 예: if 문을 while 문으로 전환

11. (statement → non-tail-recursion): Replace a statement with a non-tail-recursive structure
    - 문장을 비 꼬리 재귀 구조로 대체
    - 예: 중간에 처리가 필요한 재귀 구조로 전환

12. (expression → function): Replace an expression with a function or algorithm
    - 표현식을 함수나 알고리즘으로 대체
    - 예: score += pins → score = calculateScore(pins);

13. (variable → assignment): Replace the value of a variable (introduce assignment)
    - 변수 값 대체 (할당 도입)
    - 예: final int score → int score = 0;

14. (case): Add a case (or else) to an existing switch or if statement
    - 기존 switch나 if 문에 case 추가
    - 예: if-else 구문에 else if 조건 추가

- <https://github.com/msbaek/memo/blob/master/CC-E24-Transformation_List.md> 를 참고
```

</tpp-rule>

## write-specification-examples-rule

<write-specification-examples-rule>

```markdown
'<boundary-condition-samples>'와 같은 경계 조건이 포함되도록 예제를 작성해줘.

SRS를 이해하기 위한 예제(usage, use case scenario 등)를 만들어서 보여줘

주어진 요구사항에 대해서 해당 요구사항을 잘 설명할 수 있는 'tdd-examples.md의 <specification-example-samples> 섹션'과 같은 예제(usage, use case scenario
등)를 만들어서 보여줘

경계조건을 잘 파악해서 예제를 만들어줘

'<feedback-rule> 섹션' 준수
```

</write-specification-examples-rule>

## write-test-case-list-rule

<write-test-case-list-rule>

- `<test-addition-rule>, <programmer-test-rule>`를 준수헤서 `<test-case-list-samples>`와 같은 테스트 케이스 목록을 작성해줘
- 비즈니스 규칙과 무관한 중복되는 테스트 케이스는 제거해줘
- 동일한 비즈니스 규칙이 적용되는 테스트 케이스는 합치거나 제거해줘
- 구현하려는 코드가 어떻게 동작해야 하는지 알고 있는 시나리오들을 나열하는 단계임

</write-test-case-list-rule>

## write-javadoc-test-case-list-rule

<write-javadoc-test-case-list-rule>

```markdown
- 'general-tdd-rules.md의 <test-addition-rule>' 를 준수해서 다음 테스트를 추가해줘
- '@DisplayName' 을 이용해서 테스트 리스트에 있는 텍스트를 넣어주고, 텍스트 메소드 이름은 underscore를 이용해서 가독성이 높게 작성해줘
- 테스트 클래스의 최상단에는 java23의 마크다운 형식 커멘트 기능을 이용해서 'general-tdd-rules.md의 <javadoc-test-case-list-samples>'와 같은 형식으로 앞에서 생성한
  테스트 목록을 넣어 줘

- approvalstest를 이용해서 UI, DB 등을 고려해서 assert하도록 작성해
- 이때 테스트 리스트에 있는 모든 테스트를 한번에 추가하고 성공시키지 말고, 하나의 테스트를 추가한 후에 'general-tdd-rules.md의 <feedback-rule>' 준수해
- 테스트를 작성할 때는 언제나 approvalstest를 위한 `**approved.txt`를 함께
  작성해줘
- 테스트를 성공시킬 때는 'general-tdd-rules.md의 <make-it-work-rule>' 규칙을 준수해서 최대한 단순하게, 꼭 필요한 적은 코드로 성공하도록 해줘
```

</write-javadoc-test-case-list-rule>

## test-addition-rule

<test-addition-rule>

```
- 절차
  - most simple and degenerate(special)에서 시작
    - null, empty, 0, boundary, simple stuff 등과 같은 special case
  - 다음 단계로 interesting 하지만 조금 덜 degenerate한 failing 테스트 케이스(단일 아이템, 최소 유효 값 등)를 점진적으로 추가
  - test를 추가할 때는 특별한 이유가 있는 경우가 아니면 failing test만 추가. 모델 코드를 수정하지 않아도 성공하는 테스트는 추가하지 말아줘
     - TEST SHOLD FAIL WHEN YOU ADD IT
  - 마지막에 most interesting(general), 복잡한 테스트 케이스(복잡한 비즈니스 로직. 다중 할인 계산, 경계 값 케이스 등)를 추가해줘
```

</test-addition-rule>

## programmer-test-rule

<programmer-test-rule>

```
1. fast - 테스트는 빠르게 실행되어야 함
2. deterministic - 동일한 조건에서 항상 동일한 결과가 나와야 함
3. predictive - 모든 test가 성공하면 배포했을 때 문제가 없어야 함
   - 테스트가 모든 예상 가능한 상황을 다루어야 함
4. behavior change에 민감하고 structure change에 둔감함
   - 사용자에게 가치를 제공하는 external behavior에 coupled 되어 있고,
   - 리팩터링시 변경되는 internal structure에 decoupled 되어야 함
5. cheap to write - 테스트 작성 비용이 적어야 함
6. cheap to read
   - 테스트 코드가 명확하고 이해하기 쉬워야 함
   - 코드와 마찬가지로 테스트도 작성보다 읽을 때가 더 많음
7. cheap to change - 하나의 동작 변경으로 인해 실패하는 테스트가 다수이면 안됨
   - 사용자에게 제공되는 기능에 대해서 하나의 테스트만 있도록 작성해줘
```

</programmer-test-rule>

## approved-text-rule

<approved-text-rule>

테스트를 작성할 때 approved.txt 파일로 검증이 가능하면 최대한 approved.txt 파일을 생성하고 검증하는 방법을 취해줘

`<approved-text-samples>` 준수

`<feedback-rule>` 준수

</approved-text-rule>

## error-handling-rule

<error-handling-rule>

```markdown
## Claude가 맞닥뜨릴 수 있는 문제 상황과 대처 방법

1. 요구사항 이해 실패
    - 증상: Claude가 요구사항을 잘못 이해하고 잘못된 테스트나 구현을 시도함
    - 대처: "요구사항에 대해 제가 이해한 것이 맞는지 확인해주세요. 제가 이해한 바로는 [해석]입니다."

2. 컨텍스트 혼란
    - 증상: Claude가 이전 대화 내용을 잊거나 혼동함
    - 대처: "지금까지의 작업을 요약해주세요. 어디까지 왔고 다음에 무엇을 해야 하는지 알려주세요."

3. 구현 방향성 혼란
    - 증상: Claude가 구현 방향을 잃거나 복잡하게 접근함
    - 대처: "현재 접근 방식이 복잡해 보입니다. 더 단순한 방법으로 [목표]를 달성할 수 있을까요?"

4. 테스트 실패 원인 파악 어려움
    - 증상: 테스트가 실패하지만 원인을 파악하지 못함
    - 대처: "테스트 실패의 가능한 원인을 모두 나열해주세요. 그리고 각 원인에 대한 해결책도 제시해주세요."

5. 리팩토링 필요성 인식 실패
    - 증상: 중복 코드나 복잡성이 증가해도 리팩토링을 제안하지 않음
    - 대처: "현재 코드에 중복이나 복잡성이 있는지 검토해주세요. 리팩토링이 필요한 부분이 있나요?"

6. 기술적 제약 이해 부족
    - 증상: Claude가 Java 또는 Spring Boot의 특정 제약사항을 고려하지 않음
    - 대처: "이 접근 방식이 [기술/프레임워크]의 제약사항과 일치하는지 확인해주세요."

7. 테스트 품질 저하
    - 증상: 테스트가 불필요하게 복잡하거나, 취약하거나, 불완전함
    - 대처: "'general-tdd-rules.md의 programmer-test' 기준에 따라 이 테스트의 품질을 평가해주세요."
```

</error-handling-rule>

## context-maintenance-rule

<context-maintenance-rule>

```markdown
## 세션 컨텍스트 유지를 위한 체크포인트

세션이 길어질 때 컨텍스트를 유지하기 위해 다음 체크포인트를 주기적으로 확인하세요:

### 1. 작업 요약

- 지금까지 완료한 테스트 목록
- 현재 작업 중인 테스트
- 다음 진행할 테스트

### 2. 구현 상태 확인

- 핵심 클래스와 메서드의 현재 구조
- 테스트 커버리지 상태
- 알려진 제약사항이나 문제점

### 3. 마일스톤 체크

- 정상 작동하는 마지막 알려진 상태로 돌아갈 수 있는지
- 중간 목표 달성 여부
- 전체 목표까지 남은 작업

이 체크포인트를 약 30분마다 또는 중요한 기능 구현 후 진행하여 작업 컨텍스트를 유지하세요.
작업 컨텍스트를 요약하려면 "현재 작업 컨텍스트를 요약해주세요"라고 요청하세요.
```

</context-maintenance-rule>

## step-verification-rule

<step-verification-rule>

```markdown
## 각 TDD 단계 완료 후 확인 체크리스트

### 1. 테스트 작성 후 확인

- [ ] 테스트가 명확한 하나의 동작만 검증하는가?
- [ ] 테스트 이름이 검증하려는 내용을 명확하게 설명하는가?
- [ ] approved.txt 파일이 필요한 경우 작성되었는가?
- [ ] 테스트가 실행되고 예상대로 실패하는가?

### 2. 구현 후 확인

- [ ] 테스트를 통과하는 가장 단순한 구현인가?
- [ ] `make-it-work-strategy`, `tpp` 규칙의 단계를 적절히 적용했는가?
- [ ] 불필요한 코드가 없는가?
- [ ] 모든 테스트가 통과하는가?

### 3. 리팩토링 후 확인

- [ ] 중복이 제거되었는가?
- [ ] 코드가 더 명확해졌는가?
- [ ] 모든 테스트가 여전히 통과하는가?

### 4. 전체 과정 후 확인

- [ ] 작업 내역이 마크다운 파일에 반영되었는가?
- [ ] 다음 단계 진행을 위한 피드백을 요청했는가?

각 단계 완료 후 "이 [단계명] 단계를 확인해 주실래요?"라고 요청하면 위 체크리스트를 기반으로 확인을 진행합니다.
```

</step-verification-rule>

## terminology

<terminology>

```markdown
## TDD 관련 용어 정의

### 기본 용어

- **TDD(Test-Driven Development)**: 테스트 코드를 먼저 작성한 후 실제 코드를 구현하는 개발 방법론
- **Red-Green-Refactor**: TDD의 기본 사이클 (실패하는 테스트 작성 → 테스트 통과하는 코드 작성 → 코드 개선)
- **Test Case**: 특정 기능이나 요구사항을 검증하기 위한 개별 테스트 단위
- **Assertion**: 테스트에서 예상 결과와 실제 결과를 비교하는 검증 구문

### 테스트 유형

- **Unit Test**: 코드의 가장 작은 단위(일반적으로 메서드)를 독립적으로 검증하는 테스트
- **Integration Test**: 여러 컴포넌트 간의 상호작용을 검증하는 테스트
- **End-to-End Test**: 전체 시스템의 흐름을 처음부터 끝까지 검증하는 테스트

### 테스트 패턴 및 기법

- **Test Double**: 테스트에서 실제 객체 대신 사용되는 객체 (Mock, Stub, Fake 등)
- **Given-When-Then**: 테스트 구조화 패턴으로, 준비(Given) → 실행(When) → 검증(Then) 단계로 구성
- **Approval Testing**: 예상 결과를 미리 정의된 파일과 비교하는 테스트 방식
- **Parameterized Test**: 다양한 입력 값으로 동일한 테스트를 반복 실행하는 기법

### TDD 관련 개념

- **Test First Development**: 테스트를 먼저 작성하는 개발 방식
- **Baby Steps**: 작은 단계로 점진적으로 진행하는 TDD 접근 방식
- **FIRST 원칙**: 좋은 테스트의 특성 (Fast, Isolated, Repeatable, Self-validating, Timely)
- **Test Coverage**: 테스트가 코드의 어느 부분까지 검증하는지 나타내는 지표

### 리팩토링 관련

- **Code Smell**: 더 깊은 문제를 암시하는 코드의 표면적 특징
- **Technical Debt**: 나중에 해결해야 할 설계나 구현 상의 타협점
- **DRY (Don't Repeat Yourself)**: 중복을 피해야 한다는 원칙
- **SRP (Single Responsibility Principle)**: 클래스는 변경의 이유가 하나만 있어야 한다는 원칙
```

</terminology>

## structured-feedback-rule

<structured-feedback-rule>

## 피드백 요청 및 응답 형식

### 피드백 요청 형식

피드백을 요청할 때는 다음 형식을 사용해주세요:

```

[피드백 요청]

- 대상: [테스트/구현/설계/리팩토링]
- 초점: [특정 관심 영역]
- 맥락: [현재까지의 작업 요약]
- 구체적 질문: [구체적인 피드백 요청 사항]

```

### 피드백 응답 형식

피드백에 응답할 때는 다음 형식을 따르겠습니다:

```

[피드백]

- 긍정적 측면:
    - [잘한 점 1]
    - [잘한 점 2]

- 개선 가능 영역:
    - [개선점 1]
    - [개선점 2]

- 권장 조치:
    - [제안 1]
    - [제안 2]

- 다음 단계:
  [다음으로 진행할 작업 제안]

```

### 예시

```

[피드백 요청]

- 대상: 테스트
- 초점: gutter game 테스트 가독성
- 맥락: BowlingGame의 첫 테스트 작성
- 구체적 질문: 이 테스트가 의도를 명확히 전달하는지, 개선할 점이 있는지 알려주세요

[피드백]

- 긍정적 측면:
    - 테스트 이름이 명확함
    - given-when-then 구조가 잘 적용됨

- 개선 가능 영역:
    - 반복되는 roll(0) 호출이 가독성을 떨어뜨림
    - 주석이 부족함

- 권장 조치:
    - rollMany() 헬퍼 메소드 추가 고려
    - 각 섹션에 간단한 주석 추가

- 다음 단계:
  제안된 개선사항을 적용하고 다음 테스트로 진행

```

</structured-feedback-rule>

## high-level-test-rule

<high-level-test-rule>

```markdown
- 대표 예제 선택
    - 예제 중에서 요구사항의 제약 조건을 가장 많이 충족하는 경우(most general한 경우)를 갖는 예제를 알려줘
    - 이 예제를 통해 우리가 구현할 기능이 어떻게 사용되는지 감을 잡아보고,
    - 어떤 결과를 갖게될지 계획과 목표(Target Design)를 가지고 진행하려고 해.
- 대표 예제를 가지고 다음과 같은 '<usecase-high-level-test-rule>'를 작성해줘
- 테스트를 작성할 때는 '<act-assert-same-level-rule>'을 준수해
```

</high-level-test-rule>

### act-assert-same-level-rule

<act-assert-same-level-rule>

- 테스트에서 act와 assert는 같은 추상화 수준에서 이루어져야 함
- 한 테스트 내에서 서로 다른 추상화 레벨 혼합 금지
- api를 호출하여 행동을 수행하고, 같은 api 레벨에서 결과를 검증함
- 예: post로 생성하고 get으로 검증하는 방식

</act-assert-same-level-rule>

### usecase-high-level-test-rule

<usecase-high-level-test-rule>

```java
package pe.msbaek.tdd_workshop.shoppingbasket;

@SpringBootTest
@AutoConfigureMockMvc
public class CreateShoppingBasketTest {
    @Autowired
    private MockMvc mockMvc;

    @Autowired
    private ObjectMapper objectMapper;

    @Disabled("아직 기능 구현이 완료되지 않았습니다.")
    @DisplayName("여러 상품이 있고 20,000원 초과 시 10% 할인 적용되는 청구서 생성")
    @Test
    void create_and_verify_basket() throws Exception {
        // given
        // 장바구니에 상품 일괄 추가
        BasketItemRequests items = new BasketItemRequests(List.of(
                new BasketItemRequest("스마트폰 케이스", BigDecimal.valueOf(15000), 1),
                new BasketItemRequest("보호필름", BigDecimal.valueOf(5000), 2),
                new BasketItemRequest("충전 케이블", BigDecimal.valueOf(8000), 1)
        ));

        // when
        MvcResult postResult = mockMvc.perform(post("/api/baskets")
                        .contentType(MediaType.APPLICATION_JSON)
                        .content(objectMapper.writeValueAsString(items)))
                .andExpect(status().isOk())
                .andReturn();

        BasketResponse response = objectMapper.readValue(
                postResult.getResponse().getContentAsString(),
                BasketResponse.class);

        // 생성된 장바구니 id 획득
        String basketId = response.basketId();

        // assert: get을 통해 같은 api 레벨에서 결과 확인
        MvcResult getResult = mockMvc.perform(get("/api/baskets/" + basketId))
                .andExpect(status().isOk())
                .andReturn();

        BasketDetailsResponse basketDetails = objectMapper.readValue(
                getResult.getResponse().getContentAsString(),
                BasketDetailsResponse.class);

        // 응답 내용 검증
        Approvals.verify(printBasketDetails(basketDetails));
    }

    /**
     * 영수증을 출력하는 메소드
     */
    private String printBasketDetails(BasketDetailsResponse basketDetails) {
        return """
                ===== 영수증 =====
                품목:
                - 스마트폰 케이스 1개 (단가: 15,000원, 총액: 15,000원)
                - 보호필름 2개 (단가: 5,000원, 총액: 10,000원)
                - 충전 케이블 1개 (단가: 8,000원, 총액: 8,000원)
                소계: 33,000원
                할인: 3,300원 (10% 할인)
                최종 결제 금액: 29,700원
                ==================
                """;
    }
}
```

```markdown
- '<approved-text-samples>' 와 같은 형식 준수
- <https://approvaltests.com> 를 사용하면 `**approved.txt` 에 개발자가 작성한 원하는 결과와 printBasketDetails가 생성한 문자열을 비교할수 있음
- 이렇게 High Level Test를 작성해야 하는데 지금 이 수준에서는 가독성이 떨어지고, 테스트를 추가하면 중복이 발생하게 돼.
- 아래 코드와 같이 <protocol-driver>, Test Data Builder 등을 적용해서 DSL 스럽게 테스트를 개선해서 중복을 제거하고, 가독성을 높여줘.
```

```java

@DisplayName("여러 상품이 있고 20,000원 초과 시 10% 할인 적용되는 청구서 생성")
@Test
void create_and_verify_basket() throws Exception {
    // given: DSL로 장바구니에 여러 상품 추가
    Long basketId = basketApi.createBasket(
            aBasket()
                    .withItem(anItem("스마트폰 케이스").withPrice(15000).withQuantity(1))
                    .withItem(anItem("보호필름").withPrice(5000).withQuantity(2))
                    .withItem(anItem("충전 케이블").withPrice(8000).withQuantity(1))

            // then: 영수증 검증
            verifyReceipt(basketApi.basketDetails(basketId));
    );
```

- 이 테스트에 나타나는 도메인 클래스들에 대해 러프하게 클래스 다이어그램을 mermaid를 이용해서 작성해서 관련된 markdown 파일에 반영해줘
    - SRS를 기반으로 정적분석을 해서 domain class, value object 등을 다이어그램에 그려줘 
    - class, attributes, relation만 표현해죠
    - 금액 계산과 같은 행위와 관련된 부분은 추가하지 말아줘. 나중에 리팩터링을 통해서 추가할거야.

</usecase-high-level-test-rule>

### protocol-driver

<protocol-driver>

- **Protocol Drivers**
    - Protocol Drivers (PDs) are translators or adaptors. Translating from the DSL to the language of the system.
    - A good pattern is to mirror the interface to the DSL dsl.checkOut calls into driver.checkOut but with more
      specific parameters. DSL parses parameters and fills-in detail, Protocol Drivers encode real interactions with the
      SUT.
    - Create new PD for, at least, each different channel of communication supported by the SUT.
    - Isolate all test infrastructure knowledge of the system here.
   
</protocol-driver>
## usecase-test-class-rule

<usecase-test-class-rule>

```java

/// - [] 빈 장바구니에서 청구서 요청 시 예외 발생
/// - [] 단일 상품을 1개만 장바구니에 추가 (할인 없음, 10,000원 이하)
/// - [] 10,000원 초과 20,000원 미만 구매 시 5% 할인 적용 (여러 상품)
/// - [] 정확히 20,000원 구매 시 10% 할인 적용
/// - [] 20,000원 초과 구매 시 10% 할인 적용 (여러 상품)
@SpringBootTest
@AutoConfigureMockMvc
public class CreateShoppingBasketTest {
    @Autowired
    private MockMvc mockMvc;

    @Autowired
    private ObjectMapper objectMapper;

    @DisplayName("빈 장바구니에서 청구서 요청 시 예외 발생")
    @Test
    void empty_basket_throws_exception_when_requesting_receipt() throws Exception {
        // given: 빈 장바구니
        BasketBuilder emptyBasket = aBasket();

        // when & then: 예외 발생 검증
        MvcResult result = basketApi.createBasketAndExpect(emptyBasket, status().isBadRequest());

        // 에러 메시지 검증
        Approvals.verify(result.getResponse().getContentAsString());
    }
}
```

</usecase-test-class-rule>

## fake-repository-rule

<fake-repository-rule>

```java

@SpringBootTest
@AutoConfigureMockMvc
public class CreateShoppingBasketTest {
    @Autowired
    private MockMvc mockMvc;

    @Autowired
    private ObjectMapper objectMapper;

    @Autowired
    private BasketRepository basketRepository;

    @BeforeEach
    void setup() {
        // 테스트마다 저장소 초기화
        if (basketRepository instanceof FakeBasketRepository) {
            ((FakeBasketRepository) basketRepository).clear();
        }
    }

    @TestConfiguration
    static class TestConfig {
        @Bean
        public BasketRepository basketRepository() {
            return new FakeBasketRepository();
        }
    }

    static class FakeBasketRepository implements BasketRepository {
        private final Map<Long, Basket> baskets = new ConcurrentHashMap<>();
        private final AtomicLong idGenerator = new AtomicLong(1);

        public Basket save(Basket basket) {
            if (basket.getId() == null) {
                Long id = idGenerator.getAndIncrement();
                Basket savedBasket = new Basket(id, basket.getItems());
                baskets.put(id, savedBasket);
                return savedBasket;
            } else {
                baskets.put(basket.getId(), basket);
                return basket;
            }
        }

        public Optional<Basket> findById(Long id) {
            return Optional.ofNullable(baskets.get(id));
        }

        public void clear() {
            baskets.clear();
            idGenerator.set(1);
        }
    }
}
```

</fake-repository-rule>

## jpa-repository-rule

<jpa-repository-rule>

```markdown
- Fake Repository로 모든 기능이 동작하면 Jpa Repository를 작성해줘
- 이때 @TestConfiguration이 있으면 FakeBasketRepository를 사용하고, @TestConfiguration 부분을 커멘트 처리하면 Jpa Repository를 사용하도록 해줘
- H2 데이터베이스는 사용하지 않을 것이고, spring-boot-docker-compose를 이용해서 database에 연결할거여서 다음과 같은 코드는 필요치 않아.
```

```yaml
datasource:
  url: jdbc:mysql://localhost:3306/mydatabase
  username: myuser
  password: secret
  driver-class-name: com.mysql.cj.jdbc.Driver
```

```markdown
- 다음과 같은 단계로 진행해줘.
    1. Jpa Mapping: Entity, Value Object 등에 대해서 Jpa Mapping을 작성해줘. 이때 필요한 경우는 inner class를 outer class로 분리해줘
    2. Jpa Repository Inteface를 상속받는 BasketRepositoryJpa 인터페이스를 생성해줘
    3. BasketRepository를 구현하는 BasketRepositoryImpl 클래스를 작성해줘. 이 클래스는 BasketRepository Interface를 구현하고,
       BasketRepositoryJpa를 주입받아서 가급적 많은 행위를 위임하도록 해줘. 이렇게 해야 Fake Repository와 Jpa Repository의 구현체를 오가며 사용할 수 있어
    4. 기존 테스트의 @TestConfiguration 부분을 커멘트 처리해서 BasketRespositoryImpl을 사용하도록 해줘
- Repository 인터페이스와 구현과 관련된 클래스들에 대해서 mermaid로 클래스 다이어그램을 작성해서 markdown 파일에 반영해줘
```

</jpa-repository-rule>