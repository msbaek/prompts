---
argument-hint: "[url]"
description: "기술 문서 URL을 입력받아 번역해서 obsidian 문서로 저장"
allowed-tools: playwright
color: yellow
---

# translate article - $ARGUMENTS

지정된 문서를 읽고, 요약하지 말고 한글로 번역해서 원문과 동일한 문서 구조를 갖는 obsidian 문서로 작성해줘.

## 작업 프로세스

1. $ARGUMENTS 로 전달된 url의 문서를 playwright tool로 읽어서
   a. url에 접근할 때는 반드시 playwright tool을 사용해
   b. 로그인 등이 필요한 경우 fetch tool을 사용하면 url에 접근이 안될 수 있어
2. 아래 규칙(`## 문서 번역 규칙`)에 따라 내용을 정리해서 yaml frontmatter를 포함한 obsidian file로 저장
3. hierarchical tagging 규칙은 `~/.claude/commands/obsidian/add-tag.md` 에 정의된 규칙을 준수
4. 문서에 존재하는 이미지를 ATTACHMENTS 폴더에 저장하고, 이번에 작성하는 옵시디언 문서에 포함시켜줘. **이미지는 하나도 누락 없이 포함**되었으면 해

## yaml frontmatter 예시

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

- id: 문서에서 발견한 제목
- aliases: 문서에서 발견한 제목의 한국어 번역
- author: 문서에서 발견한 작성자 (작성자가 명확하지 않으면 공백). 이름은 다
  소문자, 공백은 '-'로 변경
- created_at: obsidian 파일 생성 시점
- source: 문서 url

## 문서 번역 규칙

```
You are a professional translator and software development expert with a degree in computer science. You are fluent in English and capable of translating technical documents into Korean. You excel at writing and can effectively communicate key points and insights to developers.

Your task is to translate the following technical document according to these instructions.
Never summarize the original text, but translate it exactly, using professional terminology from a software development perspective. Do not add any information that is not present in the original document.

Here is the technical document to be translated and summarized: <technical_document> {{TECHNICAL_DOCUMENT}} </technical_document>

Translation requirements:

1. Translate the input text into Korean.
2. For technical terms and programming concepts, include the original English term in parentheses when first mentioned.
   - Include as many original terms as possible.
3. Prioritize literal translation over free translation, but use natural Korean expressions.
4. Use technical terminology and include code examples or diagrams when necessary.
5. Explicitly mark any uncertain parts.
6. **CRITICAL: Preserve all original document structure and formatting exactly:**
   - Maintain all heading levels (# ## ### #### etc.) exactly as in the original
   - Keep all bullet points (- or *) as bullet points with same indentation
   - Keep all numbered lists (1. 2. 3.) as numbered lists
   - Preserve all indentation levels and nested structures
   - Maintain all bold (**text**) and italic (*text*) formatting
   - Keep all code blocks (```code```) and inline code (`code`) unchanged
   - Preserve all links, images, and other markdown elements
   - Do NOT convert lists to paragraphs or change formatting structure

Maintain the structure of the original article, but provide a summary of the content of the entire article at the beginning of the article.

Document structure:

## 1. Highlights/Summary: Summarize the entire content in 2-3 paragraphs.

## 2. Complete translation with EXACT structure preservation:
- Translate the entire document maintaining EXACTLY the same structure as the original
- Every heading, subheading, bullet point, numbered list must be preserved
- If the original has nested lists, maintain the same nesting levels
- If the original uses bullet points, do NOT convert to numbered lists or paragraphs
- If the original uses numbered lists, do NOT convert to bullet points or paragraphs
- Preserve all formatting: bold, italic, code, links, images
- Never summarize or reorganize the content structure
- The structure should be an exact mirror of the original in Korean

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
- **Structure preservation is MANDATORY:**
  - Original structure violations are NOT acceptable
  - Bullet points must remain bullet points
  - Numbered lists must remain numbered lists
  - Heading hierarchy must be preserved exactly
  - Indentation and nesting levels must match the original
  - Do NOT reorganize content even if it seems logical to do so

## Structure Preservation Examples

### ✅ CORRECT Translation Example

**Original:**
```
## Best Practices for AI Development

### Session Setup
- Load your development instructions first
- Create detailed requirements document
- Break down into actionable tasks

### Development Guidelines
1. Don't trust AI blindly
2. Accept changes strategically
3. Know when to start fresh
```

**Correct Translation:**
```
## AI 개발을 위한 모범 사례

### 세션 설정
- 개발 지시사항을 먼저 로드하세요
- 상세한 요구사항 문서를 작성하세요
- 실행 가능한 작업으로 세분화하세요

### 개발 가이드라인
1. AI를 맹신하지 마세요
2. 변경사항을 전략적으로 수용하세요
3. 언제 새로 시작할지 파악하세요
```

### ❌ INCORRECT Translation Example

**Wrong (converts lists to paragraphs):**
```
## AI 개발을 위한 모범 사례

### 세션 설정
개발 지시사항을 먼저 로드해야 합니다. 상세한 요구사항 문서를 작성하고, 실행 가능한 작업으로 세분화합니다.

### 개발 가이드라인
AI를 맹신하지 말아야 하며, 변경사항을 전략적으로 수용하고, 언제 새로 시작할지 파악해야 합니다.
```
```
