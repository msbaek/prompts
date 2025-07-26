# ai와 pair로 tdd로 구현하기

## Rules

- rule로 끝나는 규칙들은 './tdd-rules.md' 파일에 정의되어 있어
  - ex. `<ground-rule>`, `<feedback-rule>` 등
- samples로 끝나는 규칙들은 './tdd-samples.md' 파일에 정의되어 있어
  - ex. `<srs-samples>`, `<boundary-condition-samples>` 등

### ground-rule

`<ground-rule>` 준수

## 전체적인 절차

- 각 단계를 마치면 반드시 `<feedback-rule>`를 준수해

- 현재 markdown 파일이 비어 있으면 아래 markdown 형식으로 절차를 먼저 markdown
  파일에 작성해줘

```markdown
## 1. **SRS(소프트웨어 요구사항 명세서) 작성**

## 2. **SRS를 잘 설명할 수 있는 예제 목록 작성**

## 3. **테스트 케이스 목록 작성**

## 4. **테스트 리스트에서 테스트 선택해서 테스트 추가하기(더 이상 추가할 테스트가 없을때까지)**

'<implement-each-test-rule>' 준수
```

## SRS 작성

- 기능적 요구사항(예. Bowling Game)에 대한 SRS 작성을 요청하면 `<srs-samples>`
  와 같은 형식으로 작성해줘

`<feedback-rule>` 준수

## SRS를 잘 설명할 수 있는 예제 목록 작성

`<write-specification-examples-rule>` 준수

`<feedback-rule>` 준수. 내가 테스트를 추가하거나 제외하자고 할 수 있어

## 테스트 케이스 목록 작성

- `<write-test-case-list-rule>`를 준수
- `<write-javadoc-test-case-list-rule>`를 준수

### approved-text

- `<approved-text-rule>>` 준수

## 테스트 리스트에서 테스트 선택해서 테스트 추가하기(더 이상 추가할 테스트가 없을때까지)

`<implement-each-test-rule>` 준수

### 테스트 추가 및 성공하도록 만들기 반복

- 다음 테스트 추가 및 성공시키기 단계 반복. `<feedback-rule>` 준수
- 테스트 리스트의 모든 테스트를 추가하고 성공시킬때 까지 반복해줘
- 모든 테스트가 성공하면 처음 추가한 High Level Test에서 @Disabled를 제거하고
  모든 테스트가 성공하도록 해줘

