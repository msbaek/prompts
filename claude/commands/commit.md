---
argument-hint: "[--amend] [--push] [--no-verify]"
description: "`### 메시지 구조` 에 정의된 규칙에 따라 자동으로 커밋 메시지를 생성하고 커밋 실행"
---

# Git 커밋 자동화 - $ARGUMENTS

현재 변경사항을 분석하여 아래 정의된 규칙(`### 메시지 구조`)에 따라
커밋 메시지를 자동으로 생성하고 커밋을 실행합니다.

## 작업 프로세스

1. **변경사항 분석**

   - `git status`로 변경된 파일 확인
   - `git diff --cached`로 스테이징된 변경사항 분석
   - 변경 내용의 성격과 범위 파악

2. **커밋 메시지 생성**

   - `### 메시지 구조`에 정의된 규칙에 따라 메시지 작성
   - Conventional Commits 형식 준수
   - 타입, 범위, 제목, 본문 자동 생성
   - 한글 메시지는 반드시 임시 파일 방식으로 커밋 (하단 '한글 커밋 메시지 깨짐 방지' 섹션 참조)

3. **커밋 실행**

   - **중요**: 한글 메시지 깨짐 방지를 위해 반드시 임시 파일 사용
   - 커밋 메시지를 임시 파일에 저장 후 `git commit -F` 옵션으로 커밋
   - HEREDOC 방식은 한글이 유니코드 이스케이프로 깨질 수 있으므로 사용 금지
   - 커밋 후 결과 확인 및 보고
   - 커밋 실패 시 에러 메시지와 원인 표시

4. **결과 출력**
   - 커밋된 메시지 전체 내용 표시
   - 커밋 해시(SHA) 정보 제공
   - 변경된 파일 목록과 변경 통계 표시
   - `--push` 옵션 사용 시 push 결과도 함께 출력

## 옵션 설명

- `--amend`: 이전 커밋을 수정
- `--push`: 커밋 후 자동으로 push 실행
- `--no-verify`: pre-commit 훅 건너뛰기

## 사용 예시

### 기본 사용

```
/commit
```

### 이전 커밋 수정

```
/commit --amend
```

### 커밋 후 자동 push

```
/commit --push
```

### 훅 건너뛰고 커밋

```
/commit --no-verify
```

## 커밋 메시지 규칙 요약

### 타입 종류

- `feat`: 새로운 기능 추가
- `fix`: 버그 수정
- `docs`: 문서 수정
- `style`: 코드 포맷팅, 세미콜론 누락 등
- `refactor`: 코드 리팩토링
- `test`: 테스트 추가 또는 수정
- `chore`: 빌드 작업, 패키지 매니저 설정 등

### 메시지 구조

```
type(scope): subject (50자 이내)

본문: 72자로 줄바꿈. 최대 3개의 항목만 기술
- 변경사항의 이유와 영향 설명
- 비즈니스 맥락 중심으로 작성
- 한글로 의도가 드러나게 기술 (임시 파일 방식 필수)
```

## 실행 예시

```bash
# 현재 변경사항
- claude/commands/organize-file.md 수정
- claude/commands/add-tag.md 추가

# 생성될 커밋 메시지
feat(claude): add dynamic argument support to slash commands

- organize-file과 add-tag 명령어에 $ARGUMENTS 변수 추가하여 동적 파일명
  처리 가능하도록 개선
- YAML front matter로 자동완성 힌트와 설명 메타데이터 추가
- 드라이런 모드와 옵션 플래그 지원으로 사용성 향상
```

## 결과 출력 예시

```
✅ 커밋 성공!

커밋 해시: a1b2c3d
브랜치: main

📝 커밋 메시지:
feat(claude): add dynamic argument support to slash commands

- organize-file과 add-tag 명령어에 $ARGUMENTS 변수 추가하여 동적 파일명
  처리 가능하도록 개선
- YAML front matter로 자동완성 힌트와 설명 메타데이터 추가
- 드라이런 모드와 옵션 플래그 지원으로 사용성 향상

📊 변경 통계:
 2 files changed, 45 insertions(+), 10 deletions(-)
 - claude/commands/organize-file.md
 - claude/commands/add-tag.md
```

## 주의사항

- 스테이징된 파일이 없으면 에러 발생
- 커밋 메시지는 자동 생성되지만 검토 후 수정 가능
- `--push` 옵션 사용 시 원격 브랜치 설정 확인 필요

## ⚠️ 한글 커밋 메시지 깨짐 방지 (필수)

**HEREDOC 방식 사용 금지** - `cat <<'EOF'` 방식은 한글이 `\u{xxxx}` 유니코드 이스케이프로 깨집니다.

### 올바른 커밋 방법

```bash
# 1. Write 도구로 임시 파일에 커밋 메시지 저장
# /tmp/commit_msg.txt 파일에 메시지 작성

# 2. git commit -F 옵션으로 파일에서 메시지 읽기
git commit -F /tmp/commit_msg.txt

# 3. 커밋 후 임시 파일 삭제
rm /tmp/commit_msg.txt
```

### 임시 파일 내용 예시

```
feat(scope): 한글 제목 예시

- 한글 본문 첫 번째 항목
- 한글 본문 두 번째 항목

🤖 Generated with [Claude Code](https://claude.com/claude-code)

Co-Authored-By: Claude Opus 4.5 <noreply@anthropic.com>
```

### 금지된 방법

```bash
# ❌ 이 방식은 한글이 깨짐
git commit -m "$(cat <<'EOF'
한글 메시지
EOF
)"
```
