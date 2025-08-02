```

### 타입 지정

```

/make-commit-message --type feat

```

### 타입과 범위 지정

```

/make-commit-message --type fix --scope auth

```

### 영어 본문으로 작성

```

/make-commit-message --lang en

```

## 생성 예시

### Feature 추가

```

feat(order): add bulk order processing for k-pop merchandise

- 한정판 출시 시 대량 주문을 처리할 수 있는 일괄 처리 기능 구현. 이렇게 하면
  트래픽이 집중되는 기간 동안 데이터베이스 부하가 줄어들고 응답 시간이 향상됨
- 배치 크기를 구성할 수 있는 OrderBatchProcessor 추가. 이벤트 중심 아키텍처로
  비동기 처리 구현 배치 작업 실패에 대한 모니터링 및 알림 추가

```

### Bug 수정

```

fix(payment): resolve duplicate charge issue in retry logic

- 결제 재시도 로직에서 중복 과금이 발생하는 문제 해결. 트랜잭션 ID를 사용한
  멱등성 검증 추가로 동일한 결제가 여러 번 처리되는 것을 방지
- 재시도 전 기존 결제 상태를 확인하는 로직 추가. 이미 성공한 결제는 재시도
  하지 않도록 개선

```

### 문서 업데이트

```

docs(api): update authentication flow documentation

- OAuth 2.0 플로우 변경사항을 반영하여 API 문서 업데이트. 새로운 리프레시
  토큰 처리 방식과 에러 응답 형식 추가
- 실제 구현과 일치하도록 예제 코드 수정. 개발자들이 쉽게 이해할 수 있도록
  시퀀스 다이어그램 추가

```

## 작성 팁

1. **제목은 명령조로**: "Added" ❌ → "Add" ✅
2. **본문은 "왜"에 집중**: 코드를 보면 "어떻게"는 알 수 있음
3. **비즈니스 가치 강조**: 기술적 세부사항보다 영향과 이유
4. **구체적으로 작성**: "여러 버그 수정" ❌ → "결제 중복 처리 버그 수정" ✅

## 주의사항

- 한 커밋에는 한 가지 목적만 포함
- 제목만으로도 변경사항을 이해할 수 있어야 함
- 본문은 미래의 자신과 동료를 위한 설명
```

