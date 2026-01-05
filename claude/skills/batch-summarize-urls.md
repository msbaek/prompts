---
argument-hint: "[url1 url2 url3 ...]"
description: "URL 목록을 받아 각 URL에 대해 서브 에이전트를 병렬로 실행하여 obsidian 문서 생성"
---

# Batch Summarize URLs - $ARGUMENTS

여러 URL을 병렬로 처리하여 각각 Obsidian 문서를 생성합니다.

## 입력 형식

$ARGUMENTS로 전달되는 URL들은 다음 형식 중 하나로 구분:
- 공백으로 구분: `url1 url2 url3`
- 줄바꿈으로 구분

## 처리 프로세스

### Step 1: URL 목록 파싱
$ARGUMENTS에서 URL 목록을 추출합니다. `https://` 또는 `http://`로 시작하는 문자열을 URL로 인식합니다.

### Step 2: 병렬 서브 에이전트 실행

**중요: 반드시 단일 메시지에서 모든 Task tool 호출을 수행해야 합니다.**

각 URL에 대해 Task tool을 호출합니다:

```
Task tool 호출:
- subagent_type: "general-purpose"
- description: "Summarize article: [URL 도메인/경로 일부]"
- prompt: |
    다음 URL에 대해 Skill tool을 사용하여 /obsidian:summarize-article 스킬을 실행해주세요.

    URL: [해당 URL]

    Skill tool 호출 방법:
    - skill: "obsidian:summarize-article"
    - args: "[해당 URL]"
```

### Step 3: 결과 대기 및 수집

모든 서브 에이전트가 완료될 때까지 대기합니다. TaskOutput tool을 사용하여 각 에이전트의 결과를 수집합니다.

### Step 4: 결과 요약

처리 완료 후 다음 정보를 출력합니다:
- 처리된 URL 수
- 생성된 Obsidian 문서 목록 (파일 경로)
- 실패한 URL (있는 경우)

## 예시 실행

입력:
```
/obsidian:batch-summarize-urls https://medium.com/article1 https://medium.com/article2 https://medium.com/article3
```

Claude의 동작:
```
# 단일 메시지에서 3개의 Task tool 동시 호출

Task 1: subagent_type="general-purpose", description="Summarize: medium article1"
Task 2: subagent_type="general-purpose", description="Summarize: medium article2"
Task 3: subagent_type="general-purpose", description="Summarize: medium article3"
```

## 주의사항

1. **병렬 실행 필수**: 순차적으로 하나씩 처리하지 말고, 모든 URL을 동시에 처리
2. **서브 에이전트 독립성**: 각 서브 에이전트는 독립적으로 작업 수행
3. **에러 처리**: 일부 URL 실패 시에도 다른 URL 처리는 계속 진행
4. **결과 보고**: 모든 작업 완료 후 전체 결과 요약 제공

## 관련 스킬

- `/obsidian:summarize-article`: 단일 URL에 대한 문서 요약 (이 스킬이 내부적으로 호출하는 스킬)
