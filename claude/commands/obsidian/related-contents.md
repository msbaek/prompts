---
argument-hint: "[파일명]"
description: "Obsidian 파일의 내용을 분석하여 적절한 관련 노트 섹션 생성"
---

# Obsidian 문서의 관련 문서 추가 및 개선 - $ARGUMENTS

지정된 파일의 내용을 분석하여 적절한 문서의 제일 마지막 부분(Uncertainty Map 섹션이 있다면 이 섹션 바로 앞)에 "관련 문서" 섹션을 추가

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
     - 의미 중심 태그 사용 (git/features/worktree)
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

- Generate appropriate internal links ([[link]]) for related concepts

## 4. 관련 링크 및 참고사항 (Related Links and Notes)

- [[관련 노트 1]]
- [[관련 노트 2]]
