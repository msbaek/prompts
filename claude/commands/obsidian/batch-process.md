---
argument-hint: "--task [retag|summarize|analyze] --source [files/directory/pattern] [options]"
description: "Obsidian vault 파일들을 대량으로 처리하는 통합 명령어 (Tmux Orchestrator 활용)"
---

# Obsidian Batch Process - $ARGUMENTS

대량의 Obsidian 파일에 대해 다양한 작업을 병렬로 수행합니다.
Tmux Orchestrator를 활용하여 여러 Claude Agent를 동시에 운영합니다.

## 사용법

### 기본 구조
```bash
/obsidian:batch-process --task [작업유형] --source [파일소스] [옵션]
```

### 작업 유형 (--task)
- `retag`: 파일 재태깅 (hierarchical tag 재부여)
- `summarize`: 파일 요약 생성
- `analyze`: 파일 분석 (통계, 복잡도, 주제 등)

### 파일 소스 (--source)
- 파일 목록: `"file1.md file2.md file3.md"`
- 디렉토리: `003-RESOURCES/Tidying/`
- 패턴: `"**/*Kent*.md"`
- 파일 리스트: `target-files.txt`

### 옵션
- `--agents N`: Agent 수 지정 (기본: 자동 계산)
- `--config FILE`: 설정 파일 경로
- `--preset NAME`: 프리셋 사용
- `--keep-session`: 완료 후 tmux 세션 유지
- `--dry-run`: 실제 실행 없이 계획만 표시

## 사용 예시

### 1. 특정 파일들 재태깅
```bash
/obsidian:batch-process --task retag --source "file1.md file2.md"
```

### 2. 디렉토리 전체 요약
```bash
/obsidian:batch-process --task summarize --source 003-RESOURCES/Tidying/
```

### 3. 파일 리스트 사용
```bash
# target-files.txt 파일에 목록 작성 후
/obsidian:batch-process --task retag --source target-files.txt
```

### 4. 프리셋 사용
```bash
/obsidian:batch-process --preset kent-beck-retag
```

### 5. Agent 수 지정
```bash
/obsidian:batch-process --task analyze --source "**/*.md" --agents 6
```

## 작업별 상세 설명

### Retag (재태깅)
- 기존 YAML frontmatter의 tags 섹션을 새로운 hierarchical tag로 교체
- 최대 6개 태그 부여
- 디렉토리 기반 태그 제거, 개념 중심 태그 적용
- author 형식 통일 (예: "Kent Beck" → "kent-beck")

### Summarize (요약)
- 각 파일의 핵심 내용을 500자 이내로 요약
- 주요 포인트 3-5개 추출
- 키워드 및 실무 적용 방안 포함
- Markdown 형식으로 저장

### Analyze (분석)
- 단어 수, 읽기 시간 계산
- 복잡도 점수 측정
- 주요 주제 추출
- 참조 및 링크 분석

## 실행 프로세스

1. **파일 수집**: 지정된 소스에서 파일 목록 생성
2. **Agent 배치**: 파일 수에 따라 최적 Agent 수 결정
3. **Tmux 세션 생성**: 각 Agent를 위한 window 생성
4. **작업 분배**: 파일을 Agent들에게 균등 분배
5. **병렬 처리**: 모든 Agent가 동시에 작업 수행
6. **모니터링**: 실시간 진행 상황 추적
7. **결과 수집**: 완료된 작업 결과 통합
8. **보고서 생성**: 최종 통계 및 결과 보고서

## 모니터링

작업 진행 중 다음 명령으로 상태 확인:
```bash
# Tmux 세션 접속
tmux attach -t [session-name]

# 특정 Agent 확인
tmux attach -t [session-name]:[window-number]
```

## 결과 확인

작업 완료 후:
- 작업 디렉토리: `/Users/msbaek/git/lib/Tmux-Orchestrator/[session-name]/`
- 최종 보고서: `final_report.md`
- Agent 로그: `logs/agent_[N]_log.txt`
- 처리 결과: `results/` 디렉토리

## 프리셋 생성

자주 사용하는 설정을 프리셋으로 저장:

```yaml
# ~/.claude/obsidian-presets/my-preset.yaml
name: "My Custom Preset"
task: retag
source_pattern: "003-RESOURCES/**/*.md"
agents: 4
options:
  max_tags: 5
  exclude_patterns:
    - "**/drafts/**"
```

## 고급 설정

전역 설정 파일 수정:
`~/.claude/obsidian-batch-config.yaml`

- Agent 수 제한
- 최대 실행 시간
- 모니터링 간격
- 로그 레벨

## 주의사항

1. **대량 파일 처리**: 100개 이상 파일 처리 시 충분한 시간 확보
2. **Tmux 세션**: 기존 세션과 이름 충돌 주의
3. **파일 백업**: 중요 파일은 사전 백업 권장
4. **리소스 사용**: 여러 Claude Agent 동시 실행으로 시스템 리소스 사용량 증가

## 문제 해결

### Agent가 응답하지 않을 때
```bash
# 특정 Agent 재시작
tmux send-keys -t [session]:[window] C-c
tmux send-keys -t [session]:[window] "claude --dangerously-skip-permissions" Enter
```

### 세션 강제 종료
```bash
tmux kill-session -t [session-name]
```

## 관련 파일

- 메인 스크립트: `/Users/msbaek/git/lib/Tmux-Orchestrator/orchestrate.py`
- 템플릿: `/Users/msbaek/git/lib/Tmux-Orchestrator/templates/`
- 설정: `~/.claude/obsidian-batch-config.yaml`
- 프리셋: `~/.claude/obsidian-presets/`