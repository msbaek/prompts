---
description: Analyze current session for CLAUDE.md improvements and apply them interactively
allowed-tools: [Read, Write, Edit, Bash]
argument-hint: (no arguments needed)
---

# Analyze Current Session for CLAUDE.md Improvements

## Phase 1: Session Analysis
현재 대화를 분석하여 다음 패턴을 찾아주세요:
- 반복된 요청이나 선호사항
- "다음부터는", "앞으로는", "항상", "매번" 같은 표현
- 자주 사용한 도구나 명령어
- 언어 선호도나 커뮤니케이션 스타일
- 에러 해결 패턴

## Phase 2: Suggestion Generation
발견한 패턴을 다음 형식으로 정리해주세요:

```markdown
## CLAUDE.md 업데이트 제안

### Ground Rule 추가 제안
1. **[카테고리]**: [구체적인 제안]
   - **이유**: [왜 이것을 발견했는지]
   - **제안 문구**: `- [정확한 추가 문구]`

### LEARNING 섹션 추가 제안
1. **[주제]**: [구체적인 학습 내용]
   - **상황**: [언제/왜 유용한지]
   - **제안 문구**: `[정확한 추가 문구]`
```

만약 개선사항이 없다면 "현재 세션에서 CLAUDE.md에 추가할 만한 패턴을 찾지 못했습니다"라고 알려주세요.

## Phase 3: Interactive Review
제안사항이 있다면 사용자에게 다음을 물어보세요:
- 이 제안사항들을 적용하시겠습니까? (yes/no)
- 수정하고 싶은 부분이 있나요?

## Phase 4: Application
사용자가 승인하면:
1. 현재 CLAUDE.md 백업: `~/.claude/backups/CLAUDE.md.[timestamp]`
2. 선택된 변경사항 적용
3. diff 보여주기
4. 성공 확인 메시지

기억하세요: 의미 있는 패턴이 3개 미만이면 건너뛰는 것이 좋습니다.