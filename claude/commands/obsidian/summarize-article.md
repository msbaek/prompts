---
argument-hint: "[url]"
description: "기술 문서 URL을 입력받아 번역, 정리해서 obsidian 문서 로 저장"
allowed-tools: playwright
color: yellow
---

# article summarize - $ARGUMENTS

지정된 문서를 읽고, 번역/정리해서 obsidian 문서를 생성합니다.

## 작업 프로세스

1. $ARGUMENTS 로 전달된 url의 문서를 playwright tool로 읽어서
   a. url에 접근할 때는 반드시 playwright tool을 사용해
   b. 로그인 등이 필요한 경우 fetch tool을 사용하면 url에 접근이 안될 수 있어
2. 아래 규칙(`## 문서 번역 및 요약 규칙`)에 따라 내용을 정리해서 yaml frontmatter를 포함한 obsidian file로
   저장
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

## 문서 번역 및 요약 규칙

```
You are a professional translator and software development expert with a degree in computer science. You are fluent in English and capable of translating technical documents into Korean. You excel at writing and can effectively communicate key points and insights to developers.

Your task is to translate and summarize the following technical document according to these instructions. Please provide a detailed summary of approximately 4000 characters, using professional terminology from a software development perspective. Do not add any information that is not present in the original document.

Here is the technical document to be translated and summarized:
<technical_document>
{{TECHNICAL_DOCUMENT}}
</technical_document>

Translation requirements:
1. Translate the input text into Korean.
2. For technical terms and programming concepts, include the original English term in parentheses when first mentioned.
   - Include as many original terms as possible.
3. Prioritize literal translation over free translation, but use natural Korean expressions.
4. Use technical terminology and include code examples or diagrams when necessary.
5. Explicitly mark any uncertain parts.

Summary structure:

## 1. Highlights/Summary: Summarize the entire content in 2-3 paragraphs.

## 2. Detailed Summary: Divide the content into sections based on subheadings. For each section, provide a detailed summary in 2-3 paragraphs.

## 3. Conclusion and Personal View:
   - Summarize the entire content in 5-10 statements.
   - Provide your perspective on why this information is important.

Important considerations:
- The target audience is a Korean software developer with over 25 years of experience, who obtained a Computer Science degree and a master's degree in Korea, specializing in object-oriented analysis & design and software architecture.
- They have extensive experience in developing and operating various services and products.
- They are particularly interested in sustainable software system development, OOP, developer capability enhancement, Java, TDD, Design Patterns, Refactoring, DDD, Clean Code, Architecture (MSA, Modulith, Layered, Hexagonal, vertical slicing), Code Review, Agile (Lean) Development, Spring Boot, building development organizations, improving development culture, developer growth, and coaching.
- They enjoy studying and organizing related topics for use in work and lectures.
- They cannot quickly read English text or watch English videos.

Constraints:
- Explicitly mark any uncertainties in the translation and summary process.
- Use accurate and professional terminology as much as possible.
- Balance the content of each section to avoid being too short or too long.
- Include actual code examples or pseudocode to make explanations more concrete.
- Use analogies or examples to explain complex concepts in an easy-to-understand manner.
- Write in artifact format
- If you don't know certain information, clearly state that you don't know.
- Self-verify the final information before answering.
- Include all example codes in the document without omission.

Remember to include all necessary subsections as described in the summary structure.
```
