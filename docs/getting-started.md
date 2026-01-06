# 시작 가이드

Senior Dramas 프로젝트를 시작하기 위한 설치 및 환경 설정 가이드입니다.

## 필수 요구사항

### Claude Code
- Claude Code CLI가 설치되어 있어야 합니다
- Anthropic API 키가 설정되어 있어야 합니다

```bash
# Claude Code 설치 확인
claude --version
```

## 프로젝트 설정

### 1. 프로젝트 클론

```bash
git clone <repository-url>
cd senior-dramas
```

### 2. Claude Code 실행

```bash
claude
```

### 3. 첫 실행 확인

```
/drama:agent
```

미영 작가 에이전트가 인사말과 함께 메뉴를 표시하면 정상적으로 설정된 것입니다.

## 폴더 구조 설명

```
senior-dramas/
├── _bmad/
│   └── drama/                    # 핵심 시스템 폴더
│       ├── config.yaml           # 전체 설정
│       ├── agents/
│       │   └── drama-writer.md   # 미영 에이전트 정의
│       ├── data/
│       │   ├── themes/           # 드라마 테마 데이터
│       │   │   ├── family-conflict.yaml
│       │   │   ├── reconciliation.yaml
│       │   │   ├── generational-love.yaml
│       │   │   └── sacrifice.yaml
│       │   ├── styles/           # 스타일 가이드
│       │   │   ├── narration.md
│       │   │   ├── dialogue.md
│       │   │   └── emotion-expressions.md
│       │   └── prompts/          # 시스템 프롬프트
│       │       ├── system-prompt.md
│       │       ├── script-generation.md
│       │       └── image-prompt-guide.md
│       ├── workflows/            # 워크플로우
│       │   ├── 1-concept/story-concept/
│       │   ├── 2-blueprint/chapter-blueprint/
│       │   ├── 3-script/generate-script/
│       │   ├── 4-prompts/image-prompts/
│       │   └── 5-export/export-workflow/
│       └── testing/              # 테스트 시스템
│           ├── test-runner.md
│           ├── templates/
│           └── fixtures/
├── .claude/
│   └── commands/
│       └── drama/                # 슬래시 커맨드
│           ├── agent.md
│           ├── story.md
│           ├── blueprint.md
│           ├── script.md
│           ├── image-prompt.md
│           ├── export.md
│           └── test.md
├── docs/                         # 문서
└── output/
    └── dramas/                   # 생성된 결과물 저장
```

## 설정 파일

### config.yaml

`_bmad/drama/config.yaml` 파일에서 기본 설정을 확인할 수 있습니다:

```yaml
# 대상 시청자
target_audience:
  age_range: "50-70대"
  gender: "여성"

# 스토리 구조
story_structure:
  total_chapters: 8

# 출력 설정
output:
  base_path: "{project-root}/output/dramas"
```

## 문제 해결 (Troubleshooting)

### 커맨드가 인식되지 않는 경우

1. `.claude/commands/drama/` 폴더에 커맨드 파일이 있는지 확인
2. Claude Code를 재시작

```bash
# Claude Code 종료 후 재시작
exit
claude
```

### 에이전트가 동작하지 않는 경우

1. `_bmad/drama/agents/drama-writer.md` 파일 존재 확인
2. 파일 권한 확인

### 워크플로우 오류

워크플로우 실행 중 오류가 발생하면:

1. `_bmad/drama/workflows/` 해당 워크플로우 폴더 확인
2. 필요한 입력 파일이 있는지 확인
3. 이전 단계가 완료되었는지 확인

## 다음 단계

설정이 완료되면 다음 문서를 참고하세요:

- [커맨드 레퍼런스](commands.md) - 사용 가능한 커맨드 확인
- [워크플로우 가이드](workflows.md) - 전체 작업 흐름 이해
- [전체 워크플로우 예시](examples/full-workflow.md) - 실제 사용 예시
