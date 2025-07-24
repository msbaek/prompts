# Obsidian 파일 정리 자동화

주어진 파일을 분석하여 적절한 태그를 부여하고 vault 내의 적합한 디렉토리로 이동시켜주세요.

## 작업 프로세스

1. **파일 분석**
   - 파일의 내용을 읽고 주요 주제와 내용을 파악
   - 파일의 현재 위치와 태그 상태 확인

2. **Hierarchical Tag 부여**
   - 내용에 맞는 hierarchical tag 구조 설계
   - Obsidian의 graph view와 검색 기능을 최대한 활용할 수 있도록 구성
   - 기존 태그가 있다면 검토하고 개선
   - 예시:
     - `git/features/worktree`
     - `development/productivity/tool-name`
     - `architecture/patterns/pattern-name`
     - `AI/tools/tool-name`

3. **적절한 디렉토리 결정**
   - vault의 폴더 구조 분석
   - 파일 내용에 가장 적합한 디렉토리 선택
   - 필요한 경우 새 디렉토리 생성 제안
   - 주요 디렉토리:
     - `000-SLIPBOX/`: 정리된 생각과 통찰
     - `001-INBOX/`: 새로운 정보 수집함
     - `003-RESOURCES/`: 기술 문서 및 참고 자료
       - `/AI/`: AI 관련 도구 및 기법
       - `/ARCHITECTURE/`: 아키텍처 패턴 및 설계
       - `/CLEAN_CODE/`: 클린 코드 및 리팩토링
       - `/DDD/`: 도메인 주도 설계
       - `/DEVELOPMENT/`: 개발 방법론 및 기술
       - `/TDD/`: 테스트 주도 개발
       - `/TOOLS/`: 개발 도구 및 유틸리티
     - `997-BOOKS/`: 책 요약 및 노트

4. **파일 이동 실행**
   - 선택된 디렉토리로 파일 이동
   - 이동 후 확인

## 사용 예시

```
/obsidian:organize-file @git-worktree.md
```

이 명령은:
1. git-worktree.md 파일의 내용을 분석
2. Git 관련 hierarchical tag 부여
3. 003-RESOURCES/TOOLS/ 디렉토리로 이동