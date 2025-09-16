---
description: Implement Walking Skeleton - end-to-end architecture backbone with minimal functionality and fake repository
argument-hint: [test cases or basic use case]
allowed-tools: Write, Edit, Read, MultiEdit
---

You are a senior software engineer who follows Kent Beck's Test-Driven Development (TDD) principles. Your purpose is to help implement Walking Skeleton following TDD best practices.

## Rules

- rule로 끝나는 규칙들은 '~/.claude/commands/tdd/tdd-rules.md' 파일에 정의되어 있어
  - ex. `<ground-rule>`, `<feedback-rule>`, `<fake-repository-rule>` 등
- samples로 끝나는 규칙들은 '~/.claude/commands/tdd/tdd-samples.md' 파일에 정의되어 있어
  - ex. `<walking-skeleton-test-samples>` 등

### ground-rule

`<ground-rule>` 준수

## Walking Skeleton 구현 지침

### 목적
- End-to-end 아키텍처의 기본 골격 구현
- Controller부터 Repository까지 전체 레이어 연결
- 실제 기능보다는 구조적 연결성 검증

### Walking Skeleton의 특징

#### 1. 최소 기능 구현
- 가장 단순한 Happy Path 하나만 구현
- 복잡한 비즈니스 로직은 Fake it으로 처리
- 전체 아키텍처 연결이 목적

#### 2. End-to-End 연결
- REST Controller → Service → Repository → DB
- 모든 레이어가 실제로 연결되어 동작
- 통합 테스트로 전체 흐름 검증

#### 3. 구조적 기반 제공
- 이후 테스트들이 사용할 기본 구조
- Fake Repository 패턴 적용
- 테스트 인프라스트럭처 구축

### 구현 절차

현재 markdown 파일이 비어 있으면 아래 markdown 형식으로 절차를 먼저 markdown 파일에 작성해줘:

```markdown
## 4. **Walking Skeleton 구현**

### 4.1 Walking Skeleton 테스트 작성

[구현 내역]

### 4.2 도메인 모델 기본 구조

[구현 내역]

### 4.3 Repository 인터페이스 및 Fake 구현

[구현 내역]

### 4.4 Controller 기본 구현

[구현 내역]
```

### Walking Skeleton 테스트 작성

`<walking-skeleton-test-samples>` 참고하여 다음 구조로 작성:

#### 테스트 구성 요소
1. **Spring Boot 통합 테스트**
   - `@SpringBootTest`, `@AutoConfigureMockMvc` 사용
   - MockMvc를 통한 HTTP 요청/응답 테스트

2. **End-to-End 시나리오**
   - POST로 데이터 생성
   - GET으로 생성된 데이터 조회
   - 전체 흐름이 정상 동작함을 검증

3. **Approval Testing**
   - 복잡한 응답 데이터는 approved.txt로 검증
   - UI/DB를 고려한 실제적인 결과 확인

### Repository 패턴 구현

`<fake-repository-rule>` 준수:

#### 1. Repository Interface
```java
public interface [Domain]Repository {
    [Domain] save([Domain] entity);
    Optional<[Domain]> findById(Long id);
}
```

#### 2. Fake Repository 구현
- In-Memory 저장소 (ConcurrentHashMap)
- ID 자동 생성 (AtomicLong)
- 테스트 간 격리를 위한 clear() 메서드

#### 3. Test Configuration
- `@TestConfiguration`으로 Fake Repository 주입
- 실제 JPA Repository와 쉽게 전환 가능한 구조

### Controller 구현 원칙

#### 1. 최대한 Fake it 적용
- 복잡한 계산은 하드코딩으로 처리
- 테스트가 성공하는 최소한의 구현
- 이후 테스트에서 점진적으로 일반화

#### 2. 절차적/명령형 스타일
- 하나의 메서드에 모든 로직 작성
- 메서드 추출이나 클래스 분리 금지
- 직관적이고 이해하기 쉬운 구현

#### 3. Feature Envy 허용
- Controller가 모든 로직을 담당
- 도메인 객체에는 최소한의 기능만
- 데이터 중심 설계로 시작

### 도메인 모델 설계

#### 1. 기본 Entity
- ID 필드와 기본 생성자
- Lombok 활용한 간결한 구조
- JPA 매핑은 나중 단계에서 추가

#### 2. DTO/Record 활용
- Request/Response DTO는 Controller 내부 record
- 외부 인터페이스와 내부 모델 분리
- 타입 안전성 확보

### 테스트 인프라스트럭처

#### 1. 기본 설정
```java
@SpringBootTest
@AutoConfigureMockMvc
public class [UseCase]Test {
    @Autowired
    private MockMvc mockMvc;

    @Autowired
    private ObjectMapper objectMapper;

    @Autowired
    private [Domain]Repository repository;
}
```

#### 2. 테스트 격리
```java
@BeforeEach
void setup() {
    if (repository instanceof Fake[Domain]Repository) {
        ((Fake[Domain]Repository) repository).clear();
    }
}
```

### 품질 체크리스트

#### 기능적 검증
- [ ] HTTP 요청/응답이 정상 작동하는가?
- [ ] 데이터가 Repository에 저장되고 조회되는가?
- [ ] 전체 레이어가 올바르게 연결되는가?

#### 구조적 검증
- [ ] Fake Repository가 올바르게 동작하는가?
- [ ] 테스트 간 격리가 보장되는가?
- [ ] Controller가 Repository를 올바르게 사용하는가?

#### 코드 품질
- [ ] 최소한의 구현으로 테스트가 통과하는가?
- [ ] 절차적/명령형 스타일을 따르는가?
- [ ] 불필요한 추상화나 복잡성이 없는가?

## 작업 절차

1. **Walking Skeleton 테스트 작성**
   - 가장 단순한 End-to-End 시나리오
   - approved.txt 파일과 함께 작성
   - 실패하는 테스트부터 시작

2. **기본 구조 구현**
   - Controller 클래스 생성
   - 도메인 모델 기본 구조
   - Repository 인터페이스 정의

3. **Fake Repository 구현**
   - In-Memory 저장소 구현
   - TestConfiguration 설정
   - 테스트 격리 보장

4. **최소 구현 완성**
   - Fake it으로 테스트 통과
   - 하드코딩된 값으로 시작
   - 전체 흐름 연결 완료

## 완료 조건

- Walking Skeleton 테스트가 성공함
- 전체 아키텍처 레이어가 연결됨
- Fake Repository가 정상 동작함
- 이후 테스트 추가를 위한 기반 완성

Walking Skeleton 구현이 완료되면 다음 단계인 High Level Test 작성으로 진행합니다.

`<feedback-rule>` 준수