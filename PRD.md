이 repo 에서 나는 claude와 함께 TDD를 진행했어.

하나의 유스케이스 단위로 TDD를 진행하려고 하고, 하나의 유스케이스는 5~8개 정도의 테스트가 있을 수 있어.

1. SRS 작성
2. SRS를 잘 설명할 수 있는 예제 목록 작성
3. High Level Test 작성
4. 테스트 케이스 목록 작성
5. Walking Skeleton 구현
6. 테스트 리스트에서 테스트 선택해서 테스트 추가하기(더 이상
   추가할 테스트가 없을때까지)
7. High Level Test 활성화
8. Jpa Repository 구현
9. 테스트 코드 DSL 개선
10. JPA Repository 구현

이런 단계로 진행을 했어.

1~5까지는 claude와 내가 의견을 주고 받으며 의미있게 진행을 했어.

그런데 6번은 매우 짧은 주기로

- failing test 추가
- make it pass
- refactor

의 과정을 진행했는데. 이 과정에서 내가 너무 많이 대기를 하고, claude가 너무 많은 구현을 한번에 하는 것 같아.

어떻게 하면 짧은 단위로 진행을 하면서 내가 피드백을 느끼며 점진, 반복적으로 TDD를 진행할 수 있을지 매우 많이 고민해서 의견을 줘.

의견을 줄 때는 git commit log와 CreateShoppingBasketTest.md 문서,
그리고 관련 구현물인 CreateShoppingBasket.java, CreateShoppingBasketTest.java 등을 자세히 조사해서 의견을 줘

claude code 의 sub-agent를 활용해서 병렬로 처리하는 방법을 포함해서 의견을 줘

/Users/msbaek/git/LLM/prompts/claude/commands/tdd 폴더의 다음 파일들을 참고해서 계획을 개선하고 작성한 문서에 반영해줘

general-tdd.md: 알고리즘 구현과 관련된 TDD 절차가 있는 문서
web-usecase-tdd.md: web application으로 구현할 use case를 위한 TDD 절차가 있는 문서
tdd-rules.md: 위 2개의 절차에서 언급되는 TDD 관련된 규칙들이 정의된 문서
tdd-samples.md: 위 2개의 절차에서 언급되는 TDD 관련된 예제들이 정의된 문서

sub agent나 slash command를 만들 때는 claude code의
https://docs.anthropic.com/en/docs/claude-code/sub-agents
https://docs.anthropic.com/en/docs/claude-code/slash-commands
를 조사해서 답변을 작성해줘
이 두가지 기법을 활용하는 개선안을 구체적으로 제시해줘.

4번에서 얻은 테스트 리스트가 있을 때

- 어떻게 claude가 최대한 작은 단위로 작업하고
- 나는 대기를 적게하면서, 빠르게 검토할 수 있는지
- 어떻게 incremental, iterative 하게 TDD를 진행할 수 있을지

의견을 줘

ultrathink
