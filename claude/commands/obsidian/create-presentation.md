---
argument-hint: "[파일명 또는 경로]"
description: "Obsidian 문서를 Advanced Slides 프리젠테이션으로 변환"
color: purple
---

# Obsidian 문서를 프리젠테이션 슬라이드로 변환 - $ARGUMENTS

지정된 Obsidian 문서를 읽고 Advanced Slides 형식의 프리젠테이션 슬라이드로 변환합니다.

$ARGUMENTS가 제공되지 않은 경우, 이 도움말을 표시합니다.

## 작업 프로세스

1. **파일 검색 및 검증**
   - $ARGUMENTS로 전달된 값 처리:
     - 전체 경로인 경우: 해당 경로의 파일 사용
     - 파일명만 입력한 경우: vault 내에서 파일 검색
   - vault 기본 경로: `~/DocumentsLocal/msbaek_vault/`
   - 파일 검색 방법:
     ```bash
     fd -e md "^파일명$" ~/DocumentsLocal/msbaek_vault/
     ```
   - 검색 결과 처리:
     - 파일이 없으면 에러 메시지와 함께 종료
     - 단일 파일 발견: 해당 파일 사용
     - 복수 파일 발견: 사용자에게 선택 요청 (경로 목록 표시)
   - Markdown 파일(.md)인지 확인
2. **문서 내용 분석 및 슬라이드 구조 설계**
   - 파일의 내용을 읽고 주요 섹션과 구조 파악
3. **Advanced Slides 형식으로 변환**
   - 아래 규칙에 따라 슬라이드 생성
4. **발표자 메모 추가**
   - 각 슬라이드에 실용적인 발표자 메모 작성
5. **파일 저장**
   - 원본과 동일한 디렉토리에 저장
   - 파일명: 원본 파일명에 `-slides.md` 접미사 추가

## Advanced Slides 문법 규칙

### 슬라이드 구분자

- **수평 슬라이드 구분**: `---` (앞뒤로 빈 줄 필수)
  - 같은 레벨의 새로운 슬라이드로 이동
- **수직 슬라이드 구분**: `--` (앞뒤로 빈 줄 필수)
  - 이전 슬라이드 아래에 세부 내용 슬라이드 생성
  - 깊이 있는 설명이나 예제에 사용

### YAML Frontmatter

프리젠테이션 설정을 위한 frontmatter 예시:

```yaml
---
theme: black
transition: slide
enableMenu: false
enableChalkboard: false
enableTimeBar: true
timeBarThickness: 5
---
```

**주요 설정:**
- `theme`: 테마 (black, white, league, beige, sky, night, serif, simple, solarized)
- `transition`: 전환 효과 (none, fade, slide, convex, concave, zoom)
- `enableMenu`: 메뉴 표시 여부
- `enableChalkboard`: 칠판 기능 활성화
- `enableTimeBar`: 시간 바 표시

### 발표자 메모 (Speaker Notes)

각 슬라이드 하단에 `note:` 키워드로 발표자 메모 추가:

```markdown
## 슬라이드 제목

슬라이드 내용

note:
- 이 부분에서 강조할 핵심 포인트
- 예시나 일화 추가
- 질문이 예상되는 부분에 대한 답변 준비
```

**발표자 메모 작성 원칙:**
- 청중에게는 보이지 않고 발표자만 볼 수 있음
- 웹브라우저에서 'S' 키를 누르면 Speaker View 활성화
- 다음 슬라이드 미리보기 제공
- 타이밍 가이드, 강조점, 예상 질문 등 포함

### 조각(Fragments) - 점진적 공개

내용을 순차적으로 공개하려면 `<!-- element class="fragment" -->` 사용:

```markdown
- 첫 번째 포인트 <!-- element class="fragment" -->
- 두 번째 포인트 <!-- element class="fragment" -->
- 세 번째 포인트 <!-- element class="fragment" -->
```

### 레이아웃

**Split 레이아웃:**
```markdown
<split even>
왼쪽 내용
</split>

<split even>
오른쪽 내용
</split>
```

**Grid 레이아웃:**
```markdown
<grid>
셀 1 내용
</grid>

<grid>
셀 2 내용
</grid>
```

## 슬라이드 변환 가이드라인

### 1. 구조 설계

- **타이틀 슬라이드**: 첫 슬라이드에 제목, 부제, 발표자 정보
- **목차**: 두 번째 슬라이드에 주요 섹션 개요
- **섹션 구분**: 원본 문서의 헤딩 레벨을 기준으로 섹션 나누기
  - H1, H2: 수평 슬라이드 (`---`)
  - H3, H4: 수직 슬라이드 (`--`)
- **요약/결론**: 마지막 슬라이드에 핵심 요약

### 2. 내용 조정

- **간결성**: 각 슬라이드는 3-5개의 bullet points로 제한
- **시각적 계층**: 중요도에 따라 글자 크기와 강조 조절
- **코드 블록**: 긴 코드는 핵심 부분만 발췌하고 나머지는 발표자 메모에 기록
- **이미지/다이어그램**: 원본 문서의 이미지 경로 유지

### 3. 발표자 메모 작성

각 슬라이드마다 다음 항목을 포함:

```markdown
note:
**핵심 메시지**: 이 슬라이드의 가장 중요한 포인트

**설명 가이드**:
- 첫 번째 bullet에 대한 상세 설명
- 두 번째 bullet에 대한 상세 설명

**예시/일화**: 청중의 이해를 돕는 구체적 사례

**예상 질문**:
Q: 발생 가능한 질문
A: 준비된 답변

**전환**: 다음 슬라이드로 넘어가는 멘트
```

### 4. 프리젠테이션 흐름

- **도입부**: 문제 제기, 배경 설명
- **본론**: 핵심 개념, 방법론, 예제
- **심화**: 세부 사항 (수직 슬라이드 활용)
- **결론**: 요약, 행동 유도, Q&A

## 출력 파일 구조 예시

```markdown
---
theme: black
transition: slide
enableMenu: false
enableTimeBar: true
---

# 제목
## 부제

발표자: 이름

note:
**도입 멘트**: 청중의 관심을 끄는 질문이나 사실
**발표 시간**: 약 30분 예상
**목표**: 이 프리젠테이션을 통해 청중이 얻을 인사이트

---

## 목차

1. 배경
2. 핵심 개념
3. 실전 예제
4. 결론

note:
**흐름 설명**: 각 섹션의 소요 시간과 주요 내용 미리보기

---

## 섹션 1: 배경

- 포인트 1 <!-- element class="fragment" -->
- 포인트 2 <!-- element class="fragment" -->
- 포인트 3 <!-- element class="fragment" -->

note:
**핵심 메시지**: 왜 이 주제가 중요한가

**설명 가이드**:
- 포인트 1: 구체적 맥락 설명
- 포인트 2: 데이터나 통계 인용

**전환**: "이제 구체적인 개념을 살펴보겠습니다"

--

### 세부 사항 1

상세 내용...

note:
**강조점**: 이 부분에서 꼭 전달해야 할 메시지
**시간 배분**: 2-3분

---

## 결론

### 핵심 요약

1. 첫 번째 핵심
2. 두 번째 핵심
3. 세 번째 핵심

note:
**마무리 멘트**: 강력한 closing statement
**행동 유도**: 청중이 다음에 해야 할 것
**Q&A 준비**: 예상되는 주요 질문들
```

## 사용 예시

### 파일명만 입력 (권장)

```
/obsidian:create-presentation TDD-Best-Practices.md
```

### 전체 경로 입력

```
/obsidian:create-presentation ~/DocumentsLocal/msbaek_vault/003-RESOURCES/TDD-Best-Practices.md
```

### 인자 없이 실행

```
/obsidian:create-presentation
→ 사용법 안내 표시
```

### 복수 파일 발견 시

파일명이 중복될 경우:
```
🔍 "TDD-Best-Practices.md" 파일이 여러 개 발견되었습니다:
1. ~/DocumentsLocal/msbaek_vault/003-RESOURCES/TDD-Best-Practices.md
2. ~/DocumentsLocal/msbaek_vault/001-INBOX/TDD-Best-Practices.md

어느 파일을 변환하시겠습니까? (번호 입력)
```

## 실행 지침

1. 원본 문서의 구조와 맥락을 최대한 보존
2. 각 슬라이드는 30초~1분 내에 설명 가능한 분량으로 조정
3. 전문 용어는 첫 사용 시 설명 추가 (본문 또는 발표자 메모)
4. 시각적 요소(이미지, 다이어그램, 코드)를 적극 활용
5. 발표자 메모는 발표자가 실제로 참고할 수 있도록 구체적이고 실용적으로 작성
6. 전체 프리젠테이션의 일관된 흐름 유지

## 품질 체크리스트

- [ ] 모든 슬라이드에 발표자 메모가 있는가?
- [ ] 슬라이드 간 논리적 흐름이 자연스러운가?
- [ ] 각 슬라이드의 내용량이 적절한가? (너무 많지 않은가?)
- [ ] 핵심 메시지가 명확한가?
- [ ] 시각적 계층이 잘 구성되어 있는가?
- [ ] 원본 문서의 중요한 내용이 누락되지 않았는가?
- [ ] 발표자 메모에 예상 질문과 답변이 포함되어 있는가?

이제 $ARGUMENTS로 지정된 파일을 읽고 위 규칙에 따라 프리젠테이션 슬라이드로 변환하세요.
