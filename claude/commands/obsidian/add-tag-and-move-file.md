---
argument-hint: "[파일명] [--dry-run] [--preserve-tags]"
description: "Obsidian 파일을 분석하여 태그 부여 및 적절한 디렉토리로 이동"
---

# Obsidian 파일 정리 - $ARGUMENTS

주어진 파일을 분석하여 적절한 태그를 부여하고 vault 내의 적합한 디렉토리로 이동시켜주세요.

$ARGUMENTS가 제공되지 않은 경우, 이 도움말을 표시합니다.

## 작업 프로세스

1. tag를 부여하는 것은 './add-tag.md' 파일을 참고해서 진행하세요.
2. **적절한 디렉토리 결정**
   - vault의 폴더 구조 분석
   - 파일 내용에 가장 적합한 디렉토리 선택
   - 필요한 경우 새 디렉토리 생성 제안
   - 주요 디렉토리:
     - `000-SLIPBOX/`: 정리된 생각과 통찰
     - `001-INBOX/`: 새로운 정보 수집함
     - `002-PROJECTS/`: 진행 중인 프로젝트
     - `003-RESOURCES/`: 기술 문서 및 참고 자료
     - `004-ARCHIVE/`: 보관된 콘텐츠
     - `997-BOOKS/`: 책 요약 및 노트
     - `998-TEMPLATES/`: 템플릿 파일
   - 세부 카테고리는 vault 구조에 따라 결정
3. **파일 이동 실행**
   - `--dry-run` 옵션 사용 시 실제 이동 없이 결과만 표시
   - 선택된 디렉토리로 파일 이동
   - 이동 후 확인 및 결과 보고

## 옵션 설명

- `--dry-run`: 실제 파일 이동 없이 수행될 작업을 미리보기
- `--preserve-tags`: 기존 태그를 유지하면서 새로운 태그 추가

## 사용 예시

### 기본 사용

```
/obsidian:organize-file git-worktree.md
```

### 드라이런 모드

```
/obsidian:organize-file git-worktree.md --dry-run
```

### 기존 태그 보존

```
/obsidian:organize-file git-worktree.md --preserve-tags
```

### 인자 없이 실행

```
/obsidian:organize-file
→ 사용법 안내 표시
```

## 작업 결과 형식

```
✅ 파일 분석 완료: git-worktree.md
📋 부여된 태그: #git/features/worktree #guide #complete
📁 이동: 001-INBOX/ → 003-RESOURCES/TOOLS/
```

## 특수 케이스 처리

- **Canvas 파일(.canvas)**: 태그 부여 대상에서 제외
- **이미지 파일**: 태그 부여 대상에서 제외
- **읽기 오류 파일**: UNPROCESSED-FILES.md에 기록
- **중복 파일 ("사본" 포함)**: 별도 확인 및 처리

