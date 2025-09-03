---
argument-hint: "[code block]"
description: "code block에 대해서 composed method pattern을 준수하도록 리팩터링"
---

# Composed Method Pattern을 적용하여 가독성 개선 - $ARGUMENTS

- [Impureim sandwich](https://blog.ploeh.dk/2020/03/02/impureim-sandwich/)를 준수하여 REST, Persistence 로직 등과 도메인 로직이 섞이지 않도록
- Extract Variable, Extract Method 등을 수행해서 Composed Method Pattern을 준수
  - 좋은 이름을 붙일 수 있는 경우만 수행
  - Single Level of Abstraction Principle, Composed Method Pattern 등을 준수
