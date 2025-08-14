## approved-text

<approved-text-samples>

```
예. BolwingGameTest.complex_case.approved.txt
프레임:   | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10  |
투구:     |X  |9,0|X  |2,8|7,0|X  |X  |9,0|X  |8,2,9|
프레임점수|19 | 9 |20 |17 | 7 |29 |19 | 9 |20 |19  |
누적점수: |19 |28 |48 |65 |72 |101|120|129|149|168 |

예. CreateShoppingBasketTest.create_and_verify_basket.approved.txt
===== 영수증 =====
품목:
- 스마트폰 케이스 1개 (단가: 15,000원, 총액: 15,000원)
- 보호필름 2개 (단가: 5,000원, 총액: 10,000원)
- 충전 케이블 1개 (단가: 8,000원, 총액: 8,000원)
소계: 33,000원
할인: 3,300원 (10% 할인)
최종 결제 금액: 29,700원
==================
```

- 위 예제와 같이 최대한 UI, DB 등을 고려해서 실제 점수판, 영수증 형태로 작성해줘
- 이 파일은 테스트 클래스와 동일한 디렉토리에 작성해줘
- timestamp와 같이 non-deterministic한 요소가 포함되면 항상 테스트가 실패해.
  이러한 non-deterministic한 요소는 사용하지 말아줘. 꼭 포함해야 한다면
  scrubbing해줘(test desiderata)
- '~/.claude/commands/tdd/tdd-rules.md의 <test-desiderta-rule> 섹션' 준수

</approved-text-samples>

## srs-example

<srs-samples>

```markdown
## BowlingGame 규칙 및 요구사항 예

- 규칙
    - 기본 규칙
        - 단일 플레이어가 10개의 프레임으로 구성된 1개의 게임을 진행
        - 각 프레임에서 플레이어는 최대 2번의 투구 기회를 가짐
        - 첫 투구에서 10개 핀을 모두 쓰러뜨리면 스트라이크(X)로 기록하고, 해당 프레임에서는 더 이상 투구하지 않음
        - 두 번의 투구로 10개 핀을 모두 쓰러뜨리면 스페어(/)로 기록
    - 마지막 프레임 특별 규칙
        - 10번째 프레임에서 스트라이크를 기록하면 추가로 2번의 투구 기회를 얻음
        - 10번째 프레임에서 스페어를 기록하면 추가로 1번의 투구 기회를 얻음
        - 10번째 프레임에서 오픈 프레임(스트라이크나 스페어가 아닌 경우)이면 추가 투구 없음
- 점수 계산 요구사항
    - 기본 점수 계산
        - 시스템은 각 투구마다 쓰러뜨린 핀 수를 입력받아 기록해야 함
        - 각 프레임의 기본 점수는 해당 프레임에서 쓰러뜨린 핀의 총 개수
    - 보너스 점수 계산
        - 스트라이크의 경우, 기본 10점에 다음 2번의 투구에서 쓰러뜨린 핀 수를 보너스로 추가
        - 스페어의 경우, 기본 10점에 다음 1번의 투구에서 쓰러뜨린 핀 수를 보너스로 추가
        - 오픈 프레임의 경우, 해당 프레임에서 쓰러뜨린 핀 수만 점수로 계산 (보너스 없음)
    - 총점 계산
        - 게임의 총점은 각 프레임 점수의 합계로 계산
        - 최대 가능 점수는 300점 (모든 프레임에서 스트라이크를 기록한 경우)
        - 시스템은 현재까지의 누적 점수를 각 프레임마다 계산하고 표시해야 함

## CreateShoppingBasket 요구사항 예

- 장바구니가 비어 있으면 청구서를 사용할 수 없습니다.
- 총 가격은 `단가 * 수량`의 합계입니다.
- 청구서에 장바구니의 모든 품목이 나열됩니다.
- 총 금액이 10,000 초과 시 5% 할인 제공
- 총 금액이 20,000 이상이면 10% 할인을 제공합니다.
```

</srs-samples>

## boundary-conditions

<boundary-condition-samples>

- BowlingGame 예: gutter game, spare, strike, perfect game 등을 고려
- CreateShoppingBasket: 2만원 이상, 2만원 미만 1만원 초과, 1만원 이하, 하나의 상품이 1개만 담겨서 단가가 총계이면서 할인이 적용 안된 경우, 빈장바구니인 경우 등을 고려

</boundary-condition-samples>

## examples

<specification-example-samples>

- 시나리오 목록 작성: 코드가 어떻게 동작해야 하는지에 대한 시나리오를 아래 예제와 같이 나열(canon tdd)

```markdown
## BowlingGame 예

- 거터 게임 (모든 투구에서 0점)
    - 예시: 20번의 투구에서 모두 0개의 핀을 쓰러뜨린 경우
    - 기대 결과: 모든 프레임의 점수는 0점, 최종 점수도 0점

- 스페어 예제:
    - 예시: 첫 프레임에서 5, 5로 스페어, 다음 투구에서 8점, 이후 모두 0점
    - 기대 결과: 첫 프레임 점수는 18점(10+8), 두 번째 프레임은 8점, 최종 점수 26점

- 스트라이크 예제:
    - 예시: 첫 프레임에서 스트라이크, 다음 투구들이 3점, 4점, 이후 모두 0점
    - 기대 결과: 첫 프레임 점수는 17점(10+3+4), 두 번째 프레임은 7점, 최종 점수 24점

- 퍼펙트 게임:
    - 예시: 모든 프레임에서 스트라이크(12번의 투구)
    - 기대 결과: 모든 프레임 점수는 30점, 최종 점수 300점

- 복합 예제:
    - 예시: X, 9/0, X, 2/8, 7/0, X, X, 9/0, X, 8/2/9
    - 기대 결과: 각 프레임 점수 19,9,20,17,7,29,19,9,20,19, 총점 168점

## CreateShoppingBasket 예

- 예제1: 정확히 20,000원 - 10% 할인 적용
    - 스마트폰 케이스 1개 (단가: 15,000원, 총액: 15,000원)
    - 보호필름 1개 (단가: 5,000원, 총액: 5,000원)
    - 소계: 20,000원
    - 할인: 2,000원 (10% 할인)
    - 최종 결제 금액: 18,000원

- 예제2: 10,000원 초과 20,000원 미만 - 5% 할인 적용
    - 스마트폰 케이스 1개 (단가: 12,000원, 총액: 12,000원)
    - 보호필름 1개 (단가: 5,000원, 총액: 5,000원)
    - 소계: 17,000원
    - 할인: 850원 (5% 할인)
    - 최종 결제 금액: 16,150원

- 예제3: 10,000원 이하 - 할인 없음
    - 보호필름 2개 (단가: 5,000원, 총액: 10,000원)
    - 소계: 10,000원
    - 할인: 0원 (할인 없음)
    - 최종 결제 금액: 10,000원
    - (참고: 10,000원 미만인 경우도 동일하게 할인 없음)

- 예제4: 빈 장바구니 - 청구서 발행 불가
    - 청구서를 생성할 수 없습니다.
    - 시스템은 적절한 오류 메시지와 함께 예외를 발생시켜야 합니다.
```

- 이 예제들 중에 구현할 로직과 무관한, 중복되는 예제들이 있다면 제거해줘. 최대한 간결하게 했으면 해.

</specification-example-samples>

## incremental-test-cases-example

<test-case-list-samples>

```markdown
## Bowling Game을 위한 테스트 리스트

- 가장 단순한 특수 케이스(degenerate)에서 일반적인 케이스(general)로 진행하는
  테스트 리스트:
- [ ] gutter game
- [ ] all ones(모든 프레임에서 핀을 한개만 쓰러뜨린 경우)
- [ ] one spare(하나의 프레임만 스페어 처리하고, 다른 프레임은 open인 경우)
- [ ] one strike(하나의 프레임만 스트라이크 처리하고, 다른 프레임은 open인 경우)
- [ ] perfect game

## 쇼핑 카트 테스트 케이스 리스트

- 가장 단순한 특수 케이스(degenerate)에서 일반적인 케이스(general)로 진행하는
  테스트 리스트:
- [ ] 빈 장바구니에서 청구서 요청 시 예외 발생
- [ ] 단일 상품을 1개만 장바구니에 추가 (할인 없음, 10,000원 이하)
- [ ] 10,000원 초과 20,000원 미만 구매 시 5% 할인 적용 (여러 상품)
- [ ] 정확히 20,000원 구매 시 10% 할인 적용
- [ ] 20,000원 초과 구매 시 10% 할인 적용 (여러 상품)
```

</test-case-list-samples>

## marktdown-comment

<javadoc-test-case-list-samples>

```mark
. BowlingGame 예
/// - [ ] gutter game
/// - [ ] all ones(모든 프레임에서 핀을 한개만 쓰러뜨린 경우)
/// - [ ] one spare(하나의 프레임만 스페어 처리하고, 다른 프레임은 open인 경우)
/// - [ ] one strike(하나의 프레임만 스트라이크 처리하고, 다른 프레임은 open인 경우)
/// - [ ] perfect game

. CreateShoppingBasket 예
/// - [] 빈 장바구니에서 청구서 요청 시 예외 발생
/// - [] 단일 상품을 1개만 장바구니에 추가 (할인 없음, 10,000원 이하)
/// - [] 10,000원 초과 20,000원 미만 구매 시 5% 할인 적용 (여러 상품)
/// - [] 정확히 20,000원 구매 시 10% 할인 적용
/// - [] 20,000원 초과 구매 시 10% 할인 적용 (여러 상품)
```

</javadoc-test-case-list-samples>

## walking-skeleton-test-samples

<walking-skeleton-test-samples>

예. shopping basket sample

```java

@DisplayName("엔드-투-엔드 기능 구현: UI부터 데이터베이스까지 전체 시스템을 관통하는 기본적인 흐름 포함")
@Test
void walking_skeleton_shopping_basket() throws Exception {
    // given
    BasketItemRequests items = new BasketItemRequests(List.of(
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
```

</walking-skeleton-test-samples>

## external-behavior-test-case-list-samples

<external-behavior-test-case-list-samples>

Kent Beck의 TDD 접근법에 따르면:
    - 가장 간단한 케이스부터 시작
    - 점진적으로 복잡성 증가
    - 사용자 관점에서의 행동 검증
하는 순서를 따라 테스트를 추가해줘 

ex. 테니스 게임 External Behavior 테스트 케이스

1단계: 기본 점수 시스템
- 게임 시작: "0-0" (Love-Love)
- 첫 번째 득점: "15-0" 또는 "0-15"
- 두 번째 득점: "30-0", "15-15", "0-30"
- 세 번째 득점: "40-0", "30-15", "15-30", "0-40"

2단계: 게임 승리 조건
- 40-0에서 한 점 더: "Player1 wins"
- 40-15에서 한 점 더: "Player1 wins"
- 40-30에서 한 점 더: "Player1 wins"

3단계: Deuce 상황
- 40-40: "Deuce"
- Deuce에서 한 점: "Advantage Player1" 또는 "Advantage Player2"
- Advantage에서 같은 선수가 득점: "Player1 wins"
- Advantage에서 상대가 득점: "Deuce"로 복귀

4단계: 엣지 케이스
- 여러 번의 Deuce 반복
- Advantage 상태에서의 연속 득점

추천하는 테스트 순서
- Kent Beck의 원칙에 따라 다음 순서로 진행

newGame_ShowsLoveLove() - 가장 단순한 케이스
playerOneScoresOnce_Shows15Love() - 첫 번째 변화
bothPlayersScoreOnce_Shows15All() - 대칭성 확인
playerOneWins_ShowsWinMessage() - 게임 종료 조건
deuce_ShowsDeuce() - 특별한 규칙
advantage_ShowsAdvantage() - Deuce 이후 상황

</external-behavior-test-case-list-samples>
