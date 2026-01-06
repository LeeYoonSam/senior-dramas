# Senior Dramas

50-70대 여성 시청자를 위한 유튜브 드라마 대본 자동 생성 시스템

Claude Code 기반의 프롬프트 시스템으로, 스토리 컨셉부터 대본, 이미지 프롬프트까지 전체 제작 파이프라인을 자동화합니다.

## 주요 기능

- **스토리 컨셉 → 대본 자동 생성**: 8장 구조의 완성된 드라마 대본 생성
- **50-70대 여성 타겟 최적화**: 가족 관계, 세대 갈등, 화해 테마 특화
- **이미지 프롬프트 자동 생성**: 각 씬에 맞는 AI 이미지 프롬프트 생성
- **n8n 워크플로우 내보내기**: Google Sheets 연동 자동화 워크플로우 제공
- **프롬프트 테스트 시스템**: 품질 검증을 위한 체계적인 테스트 도구

## 빠른 시작

### Step 1: Claude Code에서 프로젝트 열기
```bash
cd senior-dramas
claude
```

### Step 2: 드라마 작가 에이전트 시작
```
/drama:agent
```

### Step 3: 메뉴에서 원하는 작업 선택
미영 작가가 안내하는 대화형 메뉴에서 작업을 선택하세요.

## 커맨드 요약

| 커맨드 | 설명 | 주요 기능 |
|--------|------|----------|
| `/drama:agent` | 드라마 작가 미영 에이전트 시작 | 대화형 메뉴, 전체 워크플로우 안내 |
| `/drama:story` | 스토리 컨셉 생성 | 원라인/테마/캐릭터/갈등구조 정의 |
| `/drama:blueprint` | 챕터 블루프린트 생성 | 8장 구조 설계, 장면 배치 |
| `/drama:script` | 대본 생성 | 전체 대본 또는 개별 챕터 |
| `/drama:image-prompt` | 이미지 프롬프트 생성 | AI 이미지 생성용 프롬프트 |
| `/drama:export` | 결과물 내보내기 | n8n JSON, PDF, Markdown |
| `/drama:test` | 프롬프트 테스트 | 품질 검증, 일관성 체크 |

## 프로젝트 구조

```
senior-dramas/
├── _bmad/drama/              # 드라마 시스템 핵심
│   ├── config.yaml           # 설정 파일
│   ├── agents/               # 미영 에이전트
│   ├── data/                 # 테마, 스타일, 프롬프트
│   │   ├── themes/           # 4가지 드라마 테마
│   │   ├── styles/           # 내레이션/대화 스타일
│   │   └── prompts/          # 시스템 프롬프트
│   ├── workflows/            # 5개 워크플로우
│   └── testing/              # 테스트 시스템
├── .claude/commands/drama/   # 7개 슬래시 커맨드
├── docs/                     # 상세 문서
└── output/dramas/            # 생성된 결과물
```

## 상세 문서

| 문서 | 설명 |
|------|------|
| [시작 가이드](docs/getting-started.md) | 설치 및 환경 설정 |
| [커맨드 레퍼런스](docs/commands.md) | 7개 커맨드 상세 설명 |
| [워크플로우 가이드](docs/workflows.md) | 5개 워크플로우 상세 설명 |
| [테마 가이드](docs/themes.md) | 4가지 드라마 테마 안내 |
| [에이전트 사용법](docs/agent.md) | 미영 에이전트 상세 안내 |
| [테스트 가이드](docs/testing.md) | 프롬프트 테스트 방법 |
| [내보내기 가이드](docs/export.md) | n8n/PDF/Markdown 내보내기 |

## 사용 예시

### 예시 1: 전체 워크플로우
[전체 워크플로우 예시 보기](docs/examples/full-workflow.md)

### 예시 2: 빠른 대본 생성
[빠른 대본 생성 예시 보기](docs/examples/quick-script.md)

### 예시 3: n8n 연동
[n8n 연동 예시 보기](docs/examples/n8n-integration.md)

### 예시 4: 프롬프트 테스트
[프롬프트 테스트 예시 보기](docs/examples/prompt-testing.md)

## 대상 시청자 특성

- **연령대**: 50-70대 여성
- **관심사**: 가족 관계, 세대 간 이해, 인생 성찰
- **선호 테마**: 화해, 용서, 사랑, 희생
- **감정적 니즈**: 공감, 위로, 희망

## 기술 스택

- **Claude Code**: AI 기반 대화형 개발 환경
- **BMAD Framework**: 워크플로우 및 에이전트 관리
- **n8n**: 자동화 워크플로우 (선택사항)
- **Google Sheets**: 데이터 입출력 (n8n 연동 시)

## 라이선스

MIT License
