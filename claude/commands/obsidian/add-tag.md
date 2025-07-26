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

2. **태그 분석**
   - 파일의 기존 태그 추출 및 검토
   - 파일 내용 전체를 분석하여 주제 파악
   - Obsidian graph view 활용도 평가

3. **태그 개선 제안**
   - 내용을 반영한 hierarchical tag 구조 설계
   - 기존 태그의 적절성 평가
   - 누락된 중요 키워드 기반 태그 추가
   - 중복되거나 불필요한 태그 제거 제안

4. **태그 적용**
   - `--dry-run` 옵션 사용 시 변경사항만 표시
   - YAML front matter에 태그 추가/수정
   - 본문 내 인라인 태그도 함께 관리

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