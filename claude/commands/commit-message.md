당신은 숙련된 소프트웨어 개발자입니다. 다음 변경사항에 대해 conventional commits
스타일의 multiline git commit message를 작성해주세요.

## 커밋 메시지 작성 규칙

1. **첫 번째 줄**: 50자 이내의 간결한 요약 (type(scope): subject 형식)

   - type: feat, fix, docs, style, refactor, test, chore 등
   - scope: 변경된 모듈/컴포넌트 (선택사항)
   - subject: 동사원형으로 시작, 첫 글자 소문자
   - 이해하기 쉬운 영어로 작성

2. **두 번째 줄**: 빈 줄

3. **본문**: 72자로 줄바꿈하여 작성
   - 무엇을, 왜 변경했는지 설명
   - 어떻게 구현했는지보다는 비즈니스 맥락과 이유에 집중
   - 간결한 한글로 작성

## 예시

```commit-message-example
feat(order): add bulk order processing for k-pop merchandise

- 한정판 출시 시 대량 주문을 처리할 수 있는 일괄 처리 기능 구현. 이렇게 하면
  트래픽이 집중되는 기간 동안 데이터베이스 부하가 줄어들고 응답 시간이 향상됨
- 배치 크기를 구성할 수 있는 OrderBatchProcessor 추가. 이벤트 중심 아키텍처로
  비동기 처리 구현 배치 작업 실패에 대한 모니터링 및 알림 추가
```
