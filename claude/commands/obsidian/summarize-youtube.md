---
argument-hint: "[transcript]"
description: "Youtube 영상의 트랜스크립트를 입력받아 번역, 정리해서 obsidian 문서로 저장"
color: yellow
---

# article summarize - $ARGUMENTS

제공되는 트랜스크립트를 번역/정리해서 obsidian 문서를 생성합니다.

## 작업 프로세스

1. $ARGUMENTS 로 전달된 트랜스크립트를 읽어서
2. 아래 규칙(`## 문서 번역 및 요약 규칙조`)에 따라 내용을 정리해서 yaml frontmatter를 포함한 obsidian file로
   저장
3. hierarchical tagging 규칙은 `~/.claude/commands/obsidian/add-tag.md` 에 정의된 규칙을 준수

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
