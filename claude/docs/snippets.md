# Snippets for Developing Web Application with TDD

## build.gradle dependencies section

- {APPROPRIATE_LATEST_VERSION}으로 표현한 버전은 https://mvnrepository.com/ 에서
  조사하거나 context7 mcp tool을 사용해서 해당 라이브러리의 최신 버전을 구해서
  사용해줘

```
annotationProcessor 'org.projectlombok:lombok'
annotationProcessor 'org.springframework.boot:spring-boot-configuration-processor'
compileOnly 'org.projectlombok:lombok'
developmentOnly 'org.springframework.boot:spring-boot-devtools'
developmentOnly 'org.springframework.boot:spring-boot-docker-compose'
implementation 'com.github.gavlyukovskiy:p6spy-spring-boot-starter:{APPROPRIATE_LATEST_VERSION}'
implementation 'org.flywaydb:flyway-core'
implementation 'org.flywaydb:flyway-mysql'
implementation 'org.jspecify:jspecify:{APPROPRIATE_LATEST_VERSION}'
implementation 'org.mybatis.spring.boot:mybatis-spring-boot-starter:{APPROPRIATE_LATEST_VERSION}'
implementation 'org.springframework.boot:spring-boot-starter-data-jpa'
implementation 'org.springframework.boot:spring-boot-starter-web'
implementation 'org.springframework.modulith:spring-modulith-starter-core'
implementation 'org.springframework.modulith:spring-modulith-starter-jpa'
runtimeOnly 'com.mysql:mysql-connector-j'
testImplementation 'com.approvaltests:approvaltests:{APPROPRIATE_LATEST_VERSION}'
testImplementation 'org.mybatis.spring.boot:mybatis-spring-boot-starter-test:{APPROPRIATE_LATEST_VERSION}'
testImplementation 'org.springframework.boot:spring-boot-starter-test'
testImplementation 'org.springframework.modulith:spring-modulith-starter-test'
testRuntimeOnly 'org.junit.platform:junit-platform-launcher'
```

## application.yaml

```yaml
spring:
  docker:
    compose:
      lifecycle-management: start_only
      skip:
        in-tests: false
  jpa:
    hibernate:
      ddl-auto: update
decorator:
  datasource:
    p6spy:
      enable-logging: true
```

## compose.yaml

```yaml
services:
  mysql:
    image: "mysql:latest"
    environment:
      - "MYSQL_DATABASE=mydatabase"
      - "MYSQL_PASSWORD=secret"
      - "MYSQL_ROOT_PASSWORD=verysecret"
      - "MYSQL_USER=myuser"
    ports:
      - "3306:3306"
```

## approved text

```text
===== 영수증 =====
품목:
- 스마트폰 케이스 1개 (단가: 15,000원, 총액: 15,000원)
- 보호필름 1개 (단가: 5,000원, 총액: 5,000원)
소계: 20,000원
할인: 2,000원 (10% 할인)
최종 결제 금액: 18,000원
==================
```

## High Level Test

```java
@DisplayName("정확히 20,000원으로 10% 할인이 적용되는 장바구니 생성 및 검증")
@Test
void create_and_verify_basket_with_10_percent_discount() throws Exception {
    // given
    BasketItemRequests items = new BasketItemRequests(List.of(
            new BasketItemRequest("스마트폰 케이스", BigDecimal.valueOf(15000), 1),
            new BasketItemRequest("보호필름", BigDecimal.valueOf(5000), 1)
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
            - 보호필름 1개 (단가: 5,000원, 총액: 5,000원)
            소계: 20,000원
            할인: 2,000원 (10% 할인)
            최종 결제 금액: 18,000원
            ==================
            """;
}
```

## walking skeleton

- 테스트

```java
@DisplayName("장바구니 생성하고 조회할 수 있다")
@Test
void can_create_and_get_basket() throws Exception {
    // given
    BasketItemRequests items = new BasketItemRequests(List.of(
            new BasketItemRequest("사과", BigDecimal.valueOf(1000), 1)
    ));

    // when - 장바구니 생성
    MvcResult postResult = mockMvc.perform(post("/api/baskets")
                    .contentType(MediaType.APPLICATION_JSON)
                    .content(objectMapper.writeValueAsString(items)))
            .andExpect(status().isOk())
            .andReturn();

    BasketResponse response = objectMapper.readValue(
            postResult.getResponse().getContentAsString(),
            BasketResponse.class);

    String basketId = response.basketId();

    // then - 조회가 성공한다 (내용은 나중에 검증)
    mockMvc.perform(get("/api/baskets/" + basketId))
            .andExpect(status().isOk());
}
```

- 최소 구현

```java
@RestController
@RequestMapping("/api/baskets")
public class BasketController {

    @PostMapping
    public ResponseEntity<BasketResponse> createBasket(@RequestBody BasketItemRequests
request) {
        return ResponseEntity.ok(new BasketResponse("any-id"));
    }

    @GetMapping("/{basketId}")
    public ResponseEntity<String> getBasket(@PathVariable String basketId) {
        return ResponseEntity.ok("{}"); // 빈 JSON이라도 200 OK
    }
}
```

## exception handling

## protocol driver

- 아래 코드와 같이 <protocol-driver>, Test Data Builder 등을 적용해서 DSL 스럽게 테스트를 개선해서 중복을 제거하고, 가독성을 높여줘.

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
}
```

<protocol-driver>
Protocol Drivers (PDs) are translators or adaptors. Translating from the DSL to the language of the system.
A good pattern is to mirror the interface to the DSL dsl.checkOut calls into driver.checkOut but with more specific parameters. DSL parses parameters and fills-in detail, Protocol Drivers encode real interactions with the SUT.
Create new PD for, at least, each different channel of communication supported by the SUT.
Isolate all test infrastructure knowledge of the system here.
</protocol-driver>

## Fake Repository

```java
@SpringBootTest
@AutoConfigureMockMvc
public class CreateShoppingBasketTest {
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

## implement jpa repository

- Fake Repository로 모든 기능이 동작하면 Jpa Repository를 작성해줘
- 이때 @TestConfiguration이 있으면 FakeBasketRepository를 사용하고, @TestConfiguration 부분을 커멘트 처리하면 Jpa Repository를 사용하도록 해줘
- H2 데이터베이스는 사용하지 않을 것이고, spring-boot-docker-compose를 이용해서 database에 연결할거여서 다음과 같은 코드는 필요치 않아.
  ```yaml
  datasource:
  url: jdbc:mysql://localhost:3306/mydatabase
  username: myuser
  password: secret
  driver-class-name: com.mysql.cj.jdbc.Driver
  ```
- 다음과 같은 단계로 진행해줘.
  1. Jpa Mapping: Entity, Value Object 등에 대해서 Jpa Mapping을 작성해줘. 이때 필요한 경우는 inner class를 outer class로 분리해줘
  2. Jpa Repository Inteface를 상속받는 BasketRepositoryJpa 인터페이스를 생성해줘
  3. BasketRepository를 구현하는 BasketRepositoryImpl 클래스를 작성해줘. 이 클래스는 BasketRepository Interface를 구현하고, BasketRepositoryJpa를 주입받아서 가급적 많은 행위를 위임하도록 해줘. 이렇게 해야 Fake Repository와 Jpa Repository의 구현체를 오가며 사용할 수 있어
  4. 기존 테스트의 @TestConfiguration 부분을 커멘트 처리해서 BasketRespositoryImpl을 사용하도록 해줘
- Repository 인터페이스와 구현과 관련된 클래스들에 대해서 mermaid로 클래스 다이어그램을 작성해서 markdown 파일에 반영해줘
