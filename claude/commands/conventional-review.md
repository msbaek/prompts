---
description: Convert review comments to Conventional Comments format
argument-hint: <review comment>
---

# Conventional Review Comment Formatter

Transform code review comments into structured Conventional Comments format for clearer, more actionable feedback.

## Task

Analyze the user's review comment ($ARGUMENTS) and convert it to Conventional Comments format:

**Format**: `<label> [decorations]: <subject>`

### Step 1: Comment Analysis
Analyze the intent and tone of the provided review comment to understand:
- What the reviewer is trying to communicate
- The severity/priority of the feedback
- Whether it requires immediate action

### Step 2: Label Classification

Choose the most appropriate label based on these criteria:

- **praise**: Positive feedback, compliments, acknowledgment of good work
  - Keywords: "좋다", "잘했다", "훌륭하다", "깔끔하다", "great", "nice", "excellent"
  
- **suggestion**: Improvement proposals, optional recommendations
  - Keywords: "~하면 좋겠다", "~는 어떨까요?", "consider", "maybe", "could", "suggest"
  
- **issue**: Clear problems, bugs, errors that need fixing
  - Keywords: "문제", "버그", "오류", "잘못", "틀렸다", "bug", "error", "problem", "broken"
  
- **question**: Seeking clarification or understanding
  - Keywords: "왜", "어떻게", "이해가 안됨", "why", "how", "what", "clarify", "?"
  
- **nitpick**: Minor style or preference issues
  - Keywords: "스타일", "들여쓰기", "네이밍", "formatting", "style", "naming", "spacing"
  
- **todo**: Must-do items, required changes
  - Keywords: "해야 함", "필수", "반드시", "must", "need to", "required", "should"
  
- **thought**: Ideas, brainstorming, non-actionable insights
  - Keywords: "생각해보니", "아이디어", "혹시", "idea", "thought", "thinking"
  
- **chore**: Simple tasks, administrative changes
  - Keywords: "주석", "문서", "정리", "comment", "documentation", "cleanup"
  
- **note**: Information sharing, context providing
  - Keywords: "참고", "알아두면", "FYI", "note", "information", "context"

### Step 3: Decoration Decision

Add appropriate decorations:

- **(blocking)**: Use when the issue prevents merge/approval
  - Critical bugs, security issues, functionality problems
  
- **(non-blocking)**: Use for suggestions, minor improvements, questions
  - Style preferences, optional optimizations, clarifications
  
- **(if-minor)**: Use when resolution depends on effort required
  - Improvements that are only worth doing if easy to implement

### Step 4: Subject Generation

Create a concise, descriptive subject line (max 50 characters) that:
- Summarizes the main point
- Uses imperative mood when suggesting actions
- Avoids unnecessary words

### Step 5: Output Format

Provide the analysis in this structure:

```
## Analysis

**Original Comment**: [원본 댓글]

**Intent**: [의도 분석]
**Severity**: [심각도 평가]

## Recommended Format

**Primary Option**:
```
<label> [decoration]: <subject>

[optional discussion if needed]
```

**Alternative Options**:
- `<alternative-label>`: [이유]
- `<alternative-label>`: [이유]

## Usage Tips
- [상황에 맞는 사용 팁]
```

### Step 6: Korean Language Support

When input is in Korean:
- Maintain Korean in the discussion section if it's more natural
- Use English labels and decorations (standard format)
- Consider cultural context in severity assessment

## Examples

**Input**: "이 함수가 너무 복잡해 보입니다. 더 작은 함수로 나누면 어떨까요?"

**Output**:
```
## Analysis

**Original Comment**: 이 함수가 너무 복잡해 보입니다. 더 작은 함수로 나누면 어떨까요?

**Intent**: 함수의 복잡성을 지적하고 리팩토링을 제안
**Severity**: 중간 (개선 제안이지만 즉시 수정 필요하지 않음)

## Recommended Format

**Primary Option**:
```
suggestion (non-blocking): 함수 복잡도 개선

이 함수를 더 작은 단위로 분리하면 가독성과 유지보수성이 향상될 것 같습니다.
```

**Alternative Options**:
- `thought`: 리팩토링에 대한 아이디어 공유
- `issue (if-minor)`: 복잡성을 문제로 보는 경우

## Usage Tips
- 비blocking으로 설정하여 강압적이지 않은 제안으로 전달
- 구체적인 분리 방법을 제시하면 더 도움이 될 것
```

Now analyze the provided comment: $ARGUMENTS