다음과 같은 규칙을 지켜서 리팩터링을 수행해서 가독성을 높이고, 코드 작성자의
의도를 동료들이 이해할 수 있도록 한다.

1. [One Pile](https://tidyfirst.substack.com/p/tidying-one-pile) if necessary

- 이 단계는 조숙한 리팩터링이 되었을 때(composed method pattern이 위배되어 코드의 의도가 전달되지 않을 때)만 진행
- inline method

2. slide statements: 라인의 순서 변경

- [Reading order](https://tidyfirst.substack.com/p/reading-order)
- [Cohesion Order - by Kent Beck](https://tidyfirst.substack.com/p/cohesion-order)
- 의도가 드러나도록 구성
  - public 메소드가 하는 일을
  - public 메소드의 각 라인(블럭)이 잘 표현해야
  - 각 라인(블럭)은 메소드보다 하나 낮은 수준의 추상화를 가져야
- Move declaration of 'xxx' closer to usages

3. Chunk Statements

- 빈 라인을 삽입하여 관련된 코드 블록을 그룹핑

4. Explaining Comment

- 코드 블록 위에 설명 주석 추가
