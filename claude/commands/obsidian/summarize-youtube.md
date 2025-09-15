---
argument-hint: "[transcript or YouTube URL]"
description: "Youtube URL 또는 트랜스크립트를 입력받아 번역, 정리해서 obsidian 문서로 저장"
color: yellow
---

# article summarize - $ARGUMENTS

제공되는 YouTube URL 또는 트랜스크립트를 번역/정리해서 obsidian 문서를 생성합니다.

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

3. **번역 및 요약**
   - 아래 규칙(`## 문서 번역 및 요약 규칙`)에 따라 내용을 정리해서 yaml frontmatter를 포함한 obsidian file로 저장

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

## 문서 번역 및 요약 규칙

```
Target Audience:
- Obtained a Computer Science degree and a master's degree in Korea
- Has worked as a software developer for over 25 years, developing and maintaining various services and products
- Cannot quickly read or watch content in English
- Interested in sustainable software system development, OOP, developer capability enhancement, Java, TDD, Design Patterns, Refactoring, DDD, Clean Code, Architecture (MSA, Modulith, Layered, Hexagonal, vertical slicing), Code Review, Agile (Lean) Development, Spring Boot, building development organizations and improving development culture, developer growth, and coaching
- Enjoys studying and organizing related topics for use in work and lectures

Translation Guidelines:
- Translate the input text to Korean
- For technical terms and programming-related concepts, include the original English term in parentheses when first mentioned
- Include as many original English terms as possible
- Prioritize literal translation over free translation, but use natural Korean expressions
- Use technical terminology and include code examples or diagrams when necessary
- Explicitly mark any uncertain parts

Summarization Structure:
1. Highlights/Summary: Summarize the entire content in 2-3 paragraphs
2. Detailed Summary: Divide the content into sections of about 5 minutes each, and summarize each section in 2-3 detailed paragraphs
3. Conclusion and Personal Views: Summarize the entire content in 5-10 statements and provide insights on why this information is important

Precautions:
- Explicitly mark any uncertainties in the translation and summarization process
- Use accurate and professional terminology as much as possible
- Balance the content of each section to avoid being too short or too long
- Include actual code examples or pseudocode to make explanations more concrete
- Explain complex concepts using analogies or examples for easier understanding
- Clearly state when you don't know certain information
- Self-verify the final information before responding
- Include all example codes in the document without omission

When you have completed the translation and summarization, present your work in the following artifact style format:

<translation_and_summary>
<highlights>
[Insert 2-3 paragraphs summarizing the entire content]
</highlights>

<detailed_summary>
[Insert detailed summary divided into sections, with 2-3 paragraphs for each section]
</detailed_summary>

<conclusion_and_views>
[Insert 5-10 summary statements and insights on the importance of the information]
</conclusion_and_views>
</translation_and_summary>

Remember to adhere to all the guidelines and precautions mentioned above throughout your translation and summarization
process.
```
