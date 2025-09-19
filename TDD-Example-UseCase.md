# TDD 프롬프트 테스트용 예제 UseCase

이 문서는 TDD 관련 프롬프트들을 체계적으로 테스트할 수 있는 두 가지 예제를 제공합니다.

## 📚 예제 1: 문자열 계산기 (general-tdd.md 테스트용)

### 테스트 방법
```bash
# 1. 템플릿 생성
/general-tdd src/test/java/pe/msbaek/tddworkshop/stringcalculator/StringCalculator.md

# 2. TDD 사이클 진행
- /tdd-red: 실패하는 테스트 작성
- /tdd-green: 최소 구현으로 통과
- /tdd-blue: 코드 정리 및 리팩토링
```

### SRS (소프트웨어 요구사항 명세서)
문자열로 입력받은 숫자들을 더하는 계산기를 만든다.

#### 기본 요구사항
1. 빈 문자열은 0을 반환한다
2. 쉼표(,)로 구분된 숫자들의 합을 반환한다
3. 줄바꿈(\n)도 구분자로 사용할 수 있다
4. 커스텀 구분자를 지원한다: "//[구분자]\n[숫자들]" 형태
5. 음수가 포함된 경우 예외를 발생시킨다

### 예제 목록
- `""` → 0
- `"1"` → 1
- `"1,2"` → 3
- `"1,2,3"` → 6
- `"1\n2,3"` → 6
- `"//;\n1;2"` → 3
- `"//*\n1*2*3"` → 6
- `"1,-2,3"` → RuntimeException("음수는 허용되지 않습니다: -2")

### 테스트 케이스 목록 (degenerate → general 순서)
- [ ] 빈 문자열: `""` → 0 (degenerate case)
- [ ] 숫자 하나: `"1"` → 1 (단순 case)
- [ ] 두 숫자: `"1,2"` → 3 (기본 case)
- [ ] 세 숫자: `"1,2,3"` → 6 (일반 case)
- [ ] 줄바꿈 구분자: `"1\n2,3"` → 6 (복합 구분자)
- [ ] 커스텀 구분자: `"//;\n1;2"` → 3 (고급 case)
- [ ] 음수 처리: `"1,-2,3"` → 예외 발생 (예외 case)

---

## 🏛️ 예제 2: 도서 대여 시스템 (web-usecase-tdd.md 테스트용)

### 테스트 방법
```bash
# 1. 웹 usecase 템플릿 생성
/web-usecase-tdd src/test/java/pe/msbaek/library/rental/BookRental.md

# 2. 9단계 TDD 프로세스 진행
/tdd-1-srs      # SRS 작성
/tdd-2-examples # 예제 목록 작성
/tdd-3-testlist # 테스트 케이스 목록
/tdd-4-skeleton # Walking Skeleton 구현
/tdd-5-highlevel # High Level Test 작성
# Red-Green-Blue 사이클 반복
# JPA Repository 구현
# DSL 개선
```

### SRS (소프트웨어 요구사항 명세서)
도서관에서 회원이 도서를 대여하고 반납할 수 있는 시스템을 만든다.

#### 핵심 기능
1. **도서 대여**: 회원이 이용 가능한 도서를 대여할 수 있다
2. **도서 반납**: 대여한 도서를 반납할 수 있다
3. **대여 현황 조회**: 회원의 대여 중인 도서 목록을 조회할 수 있다
4. **대여 이력 조회**: 회원의 전체 대여 이력을 조회할 수 있다

#### 비즈니스 규칙
- 회원은 최대 3권까지 동시 대여 가능
- 이미 대여 중인 도서는 대여할 수 없음
- 존재하지 않는 도서는 대여할 수 없음
- 대여 기간은 14일
- 연체된 도서가 있으면 새로운 대여 불가

### API 예제
```java
// 도서 대여
POST /api/rentals
{
  "memberId": "member123",
  "bookId": "book456"
}

// 도서 반납
DELETE /api/rentals/{rentalId}

// 대여 현황 조회
GET /api/members/{memberId}/current-rentals

// 대여 이력 조회
GET /api/members/{memberId}/rental-history
```

### 테스트 케이스 목록
- [ ] 이용 가능한 도서 대여 성공 (degenerate case)
- [ ] 존재하지 않는 도서 대여 실패 (예외 case)
- [ ] 이미 대여 중인 도서 대여 실패 (예외 case)
- [ ] 대여 한도 초과 시 대여 실패 (비즈니스 규칙)
- [ ] 도서 반납 성공 (기본 case)
- [ ] 대여 현황 조회 (조회 case)
- [ ] 대여 이력 조회 (조회 case)
- [ ] 연체 도서가 있을 때 새 대여 실패 (복합 비즈니스 규칙)

### Entity 설계 (참고용)
```java
// Book Entity
@Entity
public class Book {
    @Id private String id;
    private String title;
    private String author;
    private BookStatus status; // AVAILABLE, RENTED
}

// Member Entity
@Entity
public class Member {
    @Id private String id;
    private String name;
    private String email;
}

// Rental Entity
@Entity
public class Rental {
    @Id private String id;
    @ManyToOne private Member member;
    @ManyToOne private Book book;
    private LocalDateTime rentedAt;
    private LocalDateTime returnedAt;
    private LocalDateTime dueDate;
}
```

### Walking Skeleton 목표
- Spring Boot 애플리케이션 기본 설정
- 간단한 REST Controller 생성
- H2 데이터베이스 연결
- 기본적인 도서 대여 API 하나 작동

---

## 🔄 TDD 사이클 진행 가이드

### Red Phase (tdd-red-agent)
1. 문서에서 다음 체크되지 않은 테스트 케이스 선택
2. 실패하는 테스트 작성 (컴파일 에러도 실패)
3. 테스트 실행하여 예상한 이유로 실패하는지 확인
4. 문서에 테스트 케이스 완료 표시: `- [x]`

### Green Phase (tdd-green-agent)
1. 실패한 테스트를 통과시키는 최소한의 코드 작성
2. TPP(Transformation Priority Premise) 적용
3. 하드코딩이라도 테스트 통과가 우선
4. 모든 기존 테스트가 여전히 통과하는지 확인

### Blue Phase (tdd-blue-agent)
1. 코드 냄새 식별 (중복, 복잡한 조건문, 긴 메서드)
2. Kent Beck의 Tidy First 접근법 적용:
   - Guard Clauses (가드 절)
   - Dead Code Elimination (죽은 코드 제거)
   - Normalize Symmetries (대칭성 정규화)
   - New Interface, Old Implementation
3. 테스트가 깨지지 않는 안전한 리팩토링만

---

## 📝 테스트 시나리오

### 시나리오 1: 문자열 계산기로 기본 TDD 익히기
1. `/general-tdd` 명령으로 템플릿 생성
2. 첫 번째 테스트부터 순서대로 Red-Green-Blue 사이클 진행
3. TPP 원칙 적용하며 점진적 구현
4. Tidy First로 코드 개선

### 시나리오 2: 웹 애플리케이션으로 고급 TDD 연습
1. `/web-usecase-tdd` 명령으로 9단계 템플릿 생성
2. SRS 작성부터 차근차근 진행
3. Walking Skeleton으로 전체 아키텍처 검증
4. JPA, REST API 통합하며 실전 TDD 경험

### 추천 진행 순서
1. **문자열 계산기**로 TDD 기본기 익히기
2. **도서 대여 시스템**으로 실전 웹 TDD 경험하기
3. 각 단계에서 agent들의 동작 확인 및 피드백

이 예제들을 통해 TDD 프롬프트들이 제대로 동작하는지, 그리고 Kent Beck의 TDD 원칙들이 잘 적용되는지 확인할 수 있습니다.