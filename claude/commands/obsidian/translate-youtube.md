---
argument-hint: "[transcript or YouTube URL]"
description: "Youtube URL 또는 트랜스크립트를 입력받아 번역해서 obsidian 문서로 저장"
color: yellow
---

# translate youtube - $ARGUMENTS

제공되는 YouTube URL 또는 트랜스크립트를 요약하지 말고 한글로 번역해서 원문과 동일한 문서 구조를 갖는 obsidian 문서로 작성해줘.

먼저 입력 데이터 타입을 확인하겠습니다:

```bash
# YouTube URL 패턴 확인
if [[ "$ARGUMENTS" == *"youtube.com/watch?v="* ]] || [[ "$ARGUMENTS" == *"youtu.be/"* ]]; then
    echo "YouTube URL이 감지되었습니다. 메타데이터와 트랜스크립트를 다운로드합니다."

    # yt 명령어로 JSON 형식 데이터 추출
    cd ~/git/lib/download-youtube-transcript
    YOUTUBE_DATA=$(yt "$ARGUMENTS" -f json -l ko 2>/dev/null || yt "$ARGUMENTS" -f json -l en)

    if [ $? -eq 0 ]; then
        echo "YouTube 데이터 추출 완료."
        echo "$YOUTUBE_DATA" > /tmp/youtube_data.json
    else
        echo "YouTube 데이터 추출 실패. 트랜스크립트로 처리합니다."
        TRANSCRIPT="$ARGUMENTS"
    fi
else
    echo "트랜스크립트 데이터로 처리합니다."
    TRANSCRIPT="$ARGUMENTS"
fi
```

## 작업 프로세스

1. **입력 데이터 분석 및 처리**
   - $ARGUMENTS가 YouTube URL인지 확인 (youtube.com/watch?v=, youtu.be/ 패턴)
   - URL인 경우:
     - `~/git/lib/download-youtube-transcript`의 `yt` 명령어를 사용하여 JSON 형식으로 메타데이터와 트랜스크립트 추출
     - `yt "$URL" -f json`로 실행하여 제목, 채널, 업로드 날짜 등의 메타데이터 확보
   - 트랜스크립트인 경우: 기존 방식대로 직접 처리

2. **메타데이터 자동 생성** (URL인 경우)
   - id: 동영상 제목
   - aliases: 동영상 제목의 한국어 번역 (번역 필요한 경우)
   - author: 채널명 (소문자, 공백은 '-'로 변경)
   - created_at: 현재 obsidian 파일 생성 시점
   - source: 원본 YouTube URL

3. **번역**
   - 아래 규칙(`## 문서 번역 규칙`)에 따라 내용을 정리해서 yaml frontmatter를 포함한 obsidian file로 저장

4. **태그 부여**
   - hierarchical tagging 규칙은 `~/.claude/commands/obsidian/add-tag.md` 에 정의된 규칙을 준수

## yaml frontmatter 예시

### YouTube URL인 경우 자동 생성되는 frontmatter:

```yaml
id: How to Implement Clean Architecture in Spring Boot
aliases: Spring Boot에서 Clean Architecture 구현 방법
tags:
  - architecture/clean-architecture/spring-implementation
  - architecture/hexagonal/ports-adapters
  - frameworks/spring-boot/architecture
  - development/practices/clean-code
author: coding-with-john
created_at: 2025-09-15 16:30
related: []
source: https://www.youtube.com/watch?v=lqQ_NL4y5Qg
```

### 트랜스크립트인 경우 수동 입력 필요한 frontmatter:

```yaml
id: 10 Essential Software Design Patterns used in Java Core Libraries
aliases: Java 코어 라이브러리에서 사용되는 10가지 필수 소프트웨어 디자인 패턴
tags:
  - patterns/design-patterns/java-implementation
  - patterns/creational/factory-singleton-builder
  - patterns/structural/adapter-facade-proxy
  - patterns/behavioral/observer-strategy-template
  - java/core-libraries/design-patterns
  - frameworks/java/standard-library
  - development/practices/object-oriented-design
  - architecture/patterns/gof-patterns
author: ali-zeynalli
created_at: 2025-09-04 11:39
related: []
source: https://azeynalli1990.medium.com/10-essential-software-design-patterns-used-in-java-core-libraries-bb8156ae279b
```

### Frontmatter 필드 설명:

- **id**: YouTube 제목 (자동 추출) 또는 문서에서 발견한 제목
- **aliases**: YouTube 제목의 한국어 번역 (번역 필요 시) 또는 문서 제목의 한국어 번역
- **author**: YouTube 채널명 (자동 추출, 소문자, 공백은 '-'로 변경) 또는 문서 작성자
- **created_at**: obsidian 파일 생성 시점 (자동 생성)
- **source**: YouTube URL (자동 추출) 또는 문서 URL

## 문서 번역 규칙

```
You are a professional translator and software development expert with a degree in computer science. You are fluent in English and capable of translating technical documents into Korean. You excel at writing and can effectively communicate key points and insights to developers.

Your task is to translate the following YouTube transcript according to these instructions.
Never summarize the original transcript, but translate it exactly, using professional terminology from a software development perspective. Do not add any information that is not present in the original transcript.

Here is the YouTube transcript to be translated: <youtube_transcript> {{YOUTUBE_TRANSCRIPT}} </youtube_transcript>

Translation requirements:

1. Translate the input text into Korean.
2. **MANDATORY: Include original English terms in parentheses for ALL important terms:**
   - **Technical terms and programming concepts**: Include original English term in parentheses when first mentioned
   - **Key business/domain terms**: Include original terms for important concepts
   - **Important phrases**: Include original terms for key phrases that might be referenced later
   - Include as many original terms as possible to aid understanding
3. Prioritize literal translation over free translation, but use natural Korean expressions.
4. Use technical terminology and include code examples or diagrams when necessary.
5. Explicitly mark any uncertain parts.
6. **CRITICAL: Preserve the natural flow and structure of spoken content:**
   - Maintain the conversational tone of the original transcript
   - Keep the logical flow of ideas as presented in the video
   - Preserve speaker's emphasis and important points
   - Maintain any examples, analogies, or explanations in their original order
   - Do NOT reorganize content or create artificial structure
   - Keep the natural progression of the speaker's thoughts

Maintain the structure of the original transcript, but provide a summary of the content of the entire transcript at the beginning.

Document structure:

## 1. Highlights/Summary: Summarize the entire content in 2-3 paragraphs.

## 2. Complete translation with natural flow preservation:
- Translate the entire transcript maintaining the natural spoken flow
- Preserve the speaker's progression of ideas and explanations
- Keep all examples, code snippets, and demonstrations in their original context
- Maintain conversational tone while using professional Korean
- If the speaker references previous points, maintain those references
- Keep any logical groupings or sections as they naturally occur in speech
- Preserve emphasis, repetition, and clarification patterns from the original
- Never reorganize content into artificial sections unless they exist in the original
- The translation should read like a natural Korean conversation about technical topics

Important considerations:

- The target audience is particularly interested in sustainable software system development, OOP, developer capability enhancement, Java, TDD, Design Patterns, Refactoring, DDD, Clean Code, Architecture (MSA, Modulith, Layered, Hexagonal, vertical slicing), Code Review, Agile (Lean) Development, Spring Boot, building development organizations, improving development culture, developer growth, and coaching.
- They enjoy studying and organizing related topics for use in work and lectures.
- They cannot quickly read English text or watch English videos.

Constraints:

- Explicitly mark any uncertainties in the translation process.
- Use accurate and professional terminology as much as possible.
- Write in obsidian document format
- If you don't know certain information, clearly state that you don't know.
- Include all example codes in the document without omission.
- Never summarize, but translate faithfully
- **Natural flow preservation is MANDATORY:**
  - Original spoken structure violations are NOT acceptable
  - Conversational flow must be maintained
  - Do NOT create artificial sections or reorganize content
  - Preserve the speaker's natural progression of ideas
  - Maintain timing and context of examples and explanations
  - Do NOT force structure that doesn't exist in the original speech
- **Original term inclusion is MANDATORY:**
  - Technical terms must include original English when first mentioned
  - Key concepts must include original English for reference
  - This helps Korean viewers understand and reference original sources
  - Do NOT skip original terms even if they seem obvious
- **YouTube processing requirements:**
  - If transcript contains time stamps, preserve them for reference
  - Maintain any speaker identification if multiple speakers
  - Keep natural speech patterns and conversational elements
  - Preserve any live coding or demonstration sequences in their original order

## Natural Flow Preservation Examples

### ✅ CORRECT Translation Example

**Original transcript segment:**
```
So today we're going to talk about Clean Architecture. Before we dive into the implementation, let me explain what Clean Architecture actually is. It's a software design philosophy that... Actually, let me show you a quick example first, and then we'll get into the theory.
```

**Correct Translation (preserving natural speech flow):**
```
오늘은 Clean Architecture에 대해 이야기해보겠습니다. 구현에 들어가기 전에, Clean Architecture가 실제로 무엇인지 설명해드리겠습니다. 이것은 소프트웨어 설계 철학(Software Design Philosophy)인데... 사실, 먼저 간단한 예시를 보여드리고, 그다음에 이론을 살펴보겠습니다.
```

### ❌ INCORRECT Translation Examples

**Wrong (artificially restructured):**
```
## Clean Architecture 개요
Clean Architecture는 소프트웨어 설계 철학입니다.

## 예시
다음 예시를 살펴보겠습니다...

## 이론적 배경
이제 이론을 설명하겠습니다...
```

## YouTube Processing Benefits

- **Complete transcript handling**: Processes full video content for comprehensive translation
- **Metadata integration**: Automatically extracts video title, channel, and URL information
- **Context preservation**: Maintains video's educational flow and demonstration sequences
- **Reference support**: Includes original terms for viewers to reference source material
- **Natural learning flow**: Preserves instructor's teaching progression and emphasis
```