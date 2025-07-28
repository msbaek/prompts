---
argument-hint: "[파일명] [--dry-run] [--preserve-tags]"
description: "Obsidian 파일을 분석하여 태그 부여 및 적절한 디렉토리로 이동"
---

# Obsidian 파일 정리 - $ARGUMENTS

주어진 파일을 분석하여 적절한 태그를 부여하고 vault 내의 적합한 디렉토리로 이동시켜주세요.

$ARGUMENTS가 제공되지 않은 경우, 이 도움말을 표시합니다.

## 작업 프로세스

1. **파일 검증**
   - 지정된 파일(@$ARGUMENTS)의 존재 여부 확인
   - 파일이 없으면 에러 메시지와 함께 종료
   - 이미 정리된 파일인지 확인 (태그와 위치 검토)

2. **파일 분석**
   - 파일의 내용을 읽고 주요 주제와 내용을 파악
   - 파일의 현재 위치와 태그 상태 확인
   - 파일이 지정되지 않았을 때는 사용법 안내 표시

3. **Hierarchical Tag 부여**
   - 내용에 맞는 hierarchical tag 구조 설계
   - Obsidian의 graph view와 검색 기능을 최대한 활용할 수 있도록 구성
   - 기존 태그가 있다면 검토하고 개선
   - 모든 태그는 `#` 접두사로 시작
   - `--preserve-tags` 옵션 사용 시 기존 태그 유지
   - **태그 설계 원칙**:
     - 디렉토리 기반 태그(#resources/, #slipbox/) 사용 금지
     - 개념 중심 태그 사용 (#git/features/worktree)
     - development/ prefix 제거 (대부분 개발 관련이므로 불필요)
     - 5가지 카테고리 기준 적용:
       - Topic (주제): #git, #architecture, #testing 등
       - Document Type (문서 유형): #guide, #tutorial, #reference 등
       - Source (출처): #book, #article, #video 등
       - Status (상태): #draft, #review, #complete 등
       - Project (프로젝트): #project-name 등
   - 예시:
     - `#git/features/worktree` (Topic)
     - `#patterns/singleton` (development/ 제거)
     - `#architecture/microservices` (개념 중심)
     - `#AI/tools/claude` (도구별 구분)

4. **적절한 디렉토리 결정**
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

5. **파일 이동 실행**
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