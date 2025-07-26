---
argument-hint: "[--complete] [--days 숫자] [--filter 키워드] [--tag 태그명]"
description: "Things 메모를 수집하여 소셜 미디어 포스트로 변환하고 Obsidian에 저장"
---

# 주간 소셜 미디어 포스트 생성 $ARGUMENTS

Things에서 최근 메모들을 수집하여 주제별로 분류하고, 소셜 미디어에 올릴 수 있는
포스트로 변환합니다.

## 작업 프로세스

1. **옵션 파싱**
   - $ARGUMENTS에서 플래그와 값 추출
   - 기본값 설정: days=7, complete=false
   - 옵션 검증 및 에러 처리

2. **Things 메모 수집**
   - Things MCP를 사용하여 today와 inbox에서 메모 가져오기
   - `--days` 옵션에 따른 기간 필터링 (기본: 7일)
   - `--filter` 키워드가 있으면 내용 필터링
   - `--tag` 옵션이 있으면 특정 태그 필터링

3. **주제별 분류**

   - TDD, 클린코드, AI 개발, 아키텍처 등 주요 개발 주제별로 자동 분류
   - 관련된 메모들을 그룹핑하여 통합된 인사이트 도출

4. **소셜 미디어 포스트 생성**

   - LinkedIn용 긴 포스트 (인사이트 + 배경 설명)
   - Twitter용 짧은 포스트 (핵심 메시지)
   - 적절한 해시태그 자동 추가

5. **옵시디안 문서 저장**

   - `001-INBOX/social-media-posts/` 디렉토리에 날짜별로 저장
   - 계층적 태그 자동 부여:
     - `social-media/posts`
     - `development/philosophy`
     - `development/tdd`
     - `development/clean-code`
     - `development/ai`
     - `development/architecture`

6. **Things 연동**

   - 각 메모 항목에 대한 Things URL 링크 추가
   - 사용된 항목 완료 처리 옵션 제공

7. **메모 완료 처리**
   - `--complete` 옵션이 있을 때만 실행
   - Things MCP를 통해 사용된 메모들을 완료 처리
   - 처리 결과 보고

## 자동화 기능

- **날짜 자동 생성**: `YYYY-MM-DD-developer-insights.md` 형식
- **중복 확인**: 이미 처리된 메모는 제외
- **원본 보존**: 각 포스트에 원본 메모 내용 포함
- **링크 생성**: Obsidian 내부 링크 및 Things URL 자동 생성

## 사용 예시

### 기본 사용
```
/obsidian:weekly-social-posts
```

### 완료 처리 포함
```
/obsidian:weekly-social-posts --complete
```

### 특정 기간 설정
```
/obsidian:weekly-social-posts --days 14
```

### 특정 태그로 필터링
```
/obsidian:weekly-social-posts --tag tdd
```

### 복합 옵션 사용
```
/obsidian:weekly-social-posts --days 10 --filter "refactoring" --complete
```

이 명령을 실행하면:

1. Things의 최근 메모들을 자동으로 수집
2. 개발 관련 주제별로 분류 및 정리
3. 소셜 미디어 포스트 형식으로 변환
4. 옵시디안에 자동 저장

## 추가 옵션

- `--complete`: 사용된 Things 항목들을 자동으로 완료 처리
- `--days [숫자]`: 며칠 전까지의 메모를 수집할지 지정 (기본값: 7일)
- `--filter [키워드]`: 특정 키워드가 포함된 메모만 필터링
- `--tag [태그명]`: 특정 태그가 포함된 메모만 필터링

## 출력 예시

문서는 다음과 같은 구조로 생성됩니다:

```markdown
---
title: 개발자 인사이트 - 소셜 미디어 포스트 모음
date: YYYY-MM-DD
tags:
  - social-media/posts
  - development/philosophy
  - development/tdd
  - ...
---

# 개발자 인사이트 - 소셜 미디어 포스트 모음

## 📑 목차

[자동 생성된 목차]

## 🔬 [주제 1]

### LinkedIn 버전

[긴 포스트]

### Twitter 버전

[짧은 포스트]

### 원본 메모

[Things에서 가져온 원본 내용]

...

## 📱 Things 원본 항목 링크

[각 항목으로 바로 이동할 수 있는 링크들]
```

## 주의사항

- Things MCP 서버가 활성화되어 있어야 합니다
- 개발 관련 메모가 아닌 개인적인 내용은 자동으로 필터링됩니다
- 생성된 포스트는 검토 후 수정하여 사용하세요
