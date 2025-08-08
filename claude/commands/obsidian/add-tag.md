---
argument-hint: "[파일명] [--recursive] [--dry-run]"
description: "Obsidian 파일의 내용을 분석하여 적절한 hierarchical tag를 부여하거나 개선"
---

# Obsidian 태그 추가 및 개선 - $ARGUMENTS

지정된 파일의 내용을 분석하여 적절한 hierarchical tag를 부여하거나 기존 태그를 개선합니다.

$ARGUMENTS가 제공되지 않은 경우, 이 도움말을 표시합니다.

## 작업 프로세스

1. **파일 검증**
   - 지정된 파일(@$ARGUMENTS)의 존재 여부 확인
   - 파일이 없으면 에러 메시지와 함께 종료
   - Markdown 파일인지 확인
2. **파일 분석**
   - 파일의 내용을 읽고 주요 주제와 내용을 파악
3. **Hierarchical Tag 부여**
   - 내용에 맞는 hierarchical tag 구조 설계
   - 내용을 잘 표현하고, Obsidian의 graph view와 검색 기능을 최대한 활용할 수 있도록 구성
   - 기존 태그는 삭제하고 새 태그를 부여
   - 핵심 규칙
     - 계층 구분은 '/' 사용
     - tag 명은 소문자 사용
     - 공백은 허용되지 않음 (대신 '-' 사용)
     - 태그의 갯수는 최대 6개로 제한
   - **태그 설계 원칙**:
     - 디렉토리 기반 태그(resources/, slipbox/) 사용 금지
     - 개념 중심 태그 사용 (git/features/worktree)
     - development/ prefix 제거 (대부분 개발 관련이므로 불필요)
     - 5가지 카테고리 기준 적용:
       - Topic (주제): git, architecture, tdd, refactoring, oop, ddd 등
       - Document Type (문서 유형): guide, tutorial, reference 등
       - Source (출처): book, article, video, conference 등
   - 예시:
     - `git/features/worktree` (Topic)
     - `patterns/singleton` (development/ 제거)
     - `architecture/microservices` (개념 중심)
     - `AI/tools/claude` (도구별 구분)
4. '~/.claude/commands/obsidian/tagging-example.md' 파일에서 실제 문서에 대해서 태그를 부여하는 예시 참고
5. **태그 적용**
   - `--dry-run` 옵션 사용 시 변경사항만 표시
   - YAML front matter에 태그 추가/수정
   - 본문 내 인라인 태그도 함께 관리
6. author
   - author는 "Ian Cooper"의 경우 "ian-cooper" 형식으로 변환해줘

## 옵션 설명

- `--recursive`: 디렉토리 지정 시 하위 모든 .md 파일 처리
- `--dry-run`: 실제 변경 없이 수행될 작업 미리보기

## 태그 구조 원칙

1. **계층적 구조 사용**

   - 대분류/중분류/소분류 형태
   - 예: `#development/tdd/unit-testing`

2. **일관성 유지**

   - 동일한 주제는 동일한 태그 구조 사용
   - 단수/복수 형태 통일

3. **Graph View 최적화**
   - 연결성을 고려한 태그 설계
   - 너무 세분화된 태그 지양

## 사용 예시

### 기본 사용

```
/obsidian:add-tag my-note.md
```

### 드라이런 모드

```
/obsidian:add-tag my-note.md --dry-run
```

### 디렉토리 전체 처리

```
/obsidian:add-tag 003-RESOURCES/ --recursive
```

### 인자 없이 실행

```
/obsidian:add-tag
→ 사용법 안내 표시
```

## 작업 결과 형식

```
📄 파일 분석: my-note.md
🏷️  기존 태그: #development, #tdd
✨ 제안된 태그:
  추가: #development/tdd/best-practices, #testing/unit-testing
  수정: #development → #development/practices
  제거: (없음)
✅ 태그 업데이트 완료
```

## 주요 태그 카테고리

- `#development/*`: 개발 방법론 및 실습
- `#architecture/*`: 시스템 설계 및 패턴
- `#testing/*`: 테스트 관련
- `#ai/*`: AI 도구 및 기법
- `#tools/*`: 개발 도구
- `#learning/*`: 학습 자료
- `#project/*`: 프로젝트 관련

## 주의사항

- 기존 태그를 무작정 삭제하지 않고 개선 제안
- 파일 내용과 직접적으로 관련된 태그만 추가
- 너무 많은 태그는 오히려 검색과 관리를 어렵게 함
