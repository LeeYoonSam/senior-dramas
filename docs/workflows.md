# 워크플로우 가이드

Senior Dramas 시스템의 5개 워크플로우에 대한 상세 설명입니다.

## 워크플로우 개요

```
┌─────────────┐     ┌─────────────┐     ┌─────────────┐
│ 1. Story    │────▶│ 2. Blueprint│────▶│ 3. Script   │
│    Concept  │     │              │     │              │
└─────────────┘     └─────────────┘     └──────┬──────┘
                                               │
                    ┌─────────────┐            │
                    │ 5. Export   │◀───────────┤
                    │              │            │
                    └─────────────┘     ┌──────▼──────┐
                                        │ 4. Image    │
                                        │    Prompts  │
                                        └─────────────┘
```

---

## 1. Story Concept (스토리 컨셉)

### 목적
드라마의 핵심 설정을 정의합니다. 원라인, 테마, 캐릭터, 갈등 구조를 확립합니다.

### 위치
`_bmad/drama/workflows/1-concept/story-concept/`

### 파일 구조
```
story-concept/
├── workflow.md           # 워크플로우 정의
├── steps/
│   ├── 01-gather-idea.md    # 아이디어 수집
│   ├── 02-select-theme.md   # 테마 선택
│   ├── 03-design-characters.md  # 캐릭터 설계
│   └── 04-define-conflict.md    # 갈등 정의
└── templates/
    └── story-concept-template.yaml
```

### 입력
- 사용자의 스토리 아이디어 (자유 형식)
- 또는 테마 선택으로 시작

### 출력
`output/dramas/{project}/story-concept.yaml`

### 단계별 설명

#### Step 1: 아이디어 수집
- 사용자의 초기 아이디어 청취
- 키워드, 감정, 상황 추출
- 타겟 시청자 적합성 검토

#### Step 2: 테마 선택
- 4가지 테마 중 선택
- 테마별 특성 설명
- 아이디어와 테마 매칭

#### Step 3: 캐릭터 설계
- 주요 캐릭터 2-4명 정의
- 나이, 성격, 관계, 갈등 역할
- 캐릭터 간 관계도

#### Step 4: 갈등 정의
- 메인 갈등 설정
- 서브 갈등 1-2개
- 해결 방향 스케치

### 예시 출력

```yaml
project_name: "시어머니의 마음"
created: "2026-01-06"

one_liner: "30년 갈등 끝에 진심을 마주한 시어머니와 며느리"

theme:
  id: reconciliation
  name: "화해"

characters:
  - name: "김순자"
    role: protagonist
    age: 68
    personality: "완고하지만 속 깊은"
    relationship: "시어머니"
    conflict_role: "갈등의 한 축"

  - name: "박민지"
    role: deuteragonist
    age: 42
    personality: "참을성 있지만 지친"
    relationship: "며느리"
    conflict_role: "갈등의 다른 축"

conflicts:
  main:
    description: "오해로 시작된 30년 시월드 갈등"
    trigger: "결혼 초기 사소한 오해"
    resolution_hint: "손녀를 통한 진심 전달"

  sub:
    - "며느리의 직장 생활과 육아 갈등"
```

---

## 2. Chapter Blueprint (챕터 블루프린트)

### 목적
8장 구조의 상세 설계를 작성합니다. 각 챕터의 장면, 감정 흐름, 전환점을 정의합니다.

### 위치
`_bmad/drama/workflows/2-blueprint/chapter-blueprint/`

### 파일 구조
```
chapter-blueprint/
├── workflow.md
├── steps/
│   ├── 01-load-concept.md     # 컨셉 로드
│   ├── 02-design-arc.md       # 감정 곡선 설계
│   ├── 03-plan-chapters.md    # 챕터 계획
│   ├── 04-detail-scenes.md    # 씬 상세화
│   └── 05-review-blueprint.md # 검토
└── templates/
    ├── chapter-blueprint-template.yaml
    └── eight-chapter-structure.md
```

### 입력
- `story-concept.yaml`

### 출력
- `chapter-blueprint.yaml`

### 8장 구조 상세

| 챕터 | 이름 | 목적 | 감정 |
|------|------|------|------|
| 1 | 도입 | 상황 소개, 갈등 암시 | 긴장, 불안 |
| 2 | 갈등 심화 | 문제 본격화 | 답답함, 좌절 |
| 3 | 전환점 1 | 작은 희망 발견 | 희망 |
| 4 | 시도 | 변화 노력 | 기대, 불안 |
| 5 | 위기 | 최대 갈등, 절망 | 슬픔, 절망 |
| 6 | 깨달음 | 진실 발견 | 각성, 후회 |
| 7 | 화해 | 관계 회복 시작 | 감동, 위로 |
| 8 | 결말 | 새로운 시작 | 희망, 평화 |

### 단계별 설명

#### Step 1: 컨셉 로드
- story-concept.yaml 로드
- 핵심 요소 추출
- 검증 및 확인

#### Step 2: 감정 곡선 설계
- 8장 감정 흐름 설계
- 클라이맥스 위치 확인
- 전환점 배치

#### Step 3: 챕터 계획
- 각 챕터 제목 및 핵심 내용
- 등장 캐릭터 배치
- 주요 이벤트 정의

#### Step 4: 씬 상세화
- 챕터당 2-4개 씬
- 장소, 시간, 인물
- 핵심 액션 및 대사 방향

#### Step 5: 검토
- 전체 흐름 검토
- 일관성 체크
- 누락 요소 확인

---

## 3. Generate Script (대본 생성)

### 목적
블루프린트를 바탕으로 완성된 대본을 생성합니다.

### 위치
`_bmad/drama/workflows/3-script/generate-script/`

### 파일 구조
```
generate-script/
├── workflow.md
├── steps/
│   ├── 01-load-blueprint.md
│   ├── 02-load-styles.md
│   ├── 03-generate-chapter.md
│   ├── 04-apply-narration.md
│   └── 05-review-script.md
└── templates/
    └── script-template.md
```

### 입력
- `chapter-blueprint.yaml`
- 스타일 가이드 (자동 로드)

### 출력
- `script-full.md` (전체)
- `scripts/chapter-{n}.md` (챕터별)

### 3가지 서술 도구

#### 내레이션 (Narration)
- 상황 설명
- 시간 경과 표현
- 배경 묘사

```markdown
**[내레이션]**
10년이 지났다. 순자의 머리카락은 하얗게 세었지만,
며느리를 향한 마음은 여전히 얼어붙어 있었다.
```

#### 대화 (Dialogue)
- 캐릭터 간 대화
- 감정 지문 포함
- 방언/말투 반영

```markdown
**[대화]**
순자: (망설이며) "민지야... 저녁은 먹었니?"

민지: (놀라며) "어머니가... 저한테요?"
```

#### 내면 독백 (Inner Monologue)
- 캐릭터의 속마음
- 과거 회상
- 감정 심화

```markdown
**[내면 독백 - 순자]**
'내가 왜 이 말을 못하고 살았을까...'
순자는 지난 30년의 후회가 밀려왔다.
```

### 스타일 가이드 적용

대본 생성 시 자동으로 로드되는 스타일 가이드:
- `data/styles/narration.md` - 내레이션 스타일
- `data/styles/dialogue.md` - 대화 스타일
- `data/styles/emotion-expressions.md` - 감정 표현

---

## 4. Image Prompts (이미지 프롬프트)

### 목적
각 씬에 맞는 AI 이미지 생성용 프롬프트를 만듭니다.

### 위치
`_bmad/drama/workflows/4-prompts/image-prompts/`

### 파일 구조
```
image-prompts/
├── workflow.md
├── steps/
│   ├── 01-analyze-scenes.md
│   ├── 02-define-visual.md
│   ├── 03-generate-prompts.md
│   └── 04-optimize-prompts.md
└── templates/
    └── image-prompt-template.yaml
```

### 입력
- 대본 파일
- `data/prompts/image-prompt-guide.md`

### 출력
- `image-prompts.yaml`

### 프롬프트 구성 요소

```yaml
prompt:
  scene_id: "ch1_s1"

  # 필수 요소
  subject: "elderly Korean woman"
  setting: "modern apartment living room"
  time: "evening, golden hour"

  # 감정/분위기
  mood: "tense, cautious"
  atmosphere: "warm but uneasy"

  # 스타일
  style: "realistic photograph"
  lighting: "soft natural light from window"

  # 추가 디테일
  details:
    - "traditional Korean elements"
    - "family photos on wall"
```

### 스타일 옵션

| 스타일 | 설명 | 사용 상황 |
|--------|------|----------|
| realistic | 사진 같은 현실적 | 일반 씬 |
| cinematic | 영화적 연출 | 클라이맥스 |
| illustration | 부드러운 일러스트 | 회상 씬 |
| dramatic | 강렬한 조명 | 갈등 씬 |

---

## 5. Export Workflow (내보내기)

### 목적
완성된 결과물을 다양한 형식으로 내보냅니다.

### 위치
`_bmad/drama/workflows/5-export/export-workflow/`

### 파일 구조
```
export-workflow/
├── workflow.md
├── steps/
│   ├── 01-gather-assets.md
│   ├── 02-format-output.md
│   └── 03-generate-export.md
└── templates/
    └── n8n-workflow.json
```

### 입력
- 모든 생성된 결과물
- 내보내기 형식 선택

### 출력 형식

#### n8n JSON
자동화 워크플로우 파일

```json
{
  "name": "Senior Drama Automation",
  "nodes": [
    {
      "name": "Google Sheets Trigger",
      "type": "n8n-nodes-base.googleSheetsTrigger"
    },
    {
      "name": "AI Script Generator",
      "type": "n8n-nodes-base.httpRequest"
    },
    {
      "name": "Image Generator",
      "type": "n8n-nodes-base.httpRequest"
    }
  ]
}
```

#### PDF
인쇄용 문서
- 표지
- 캐릭터 소개
- 전체 대본
- 이미지 프롬프트 목록

#### Markdown
단일 마크다운 파일
- 전체 내용 통합
- GitHub/노션 호환

---

## 워크플로우 실행 순서

### 표준 순서 (권장)
```
1. /drama:story      → story-concept.yaml
2. /drama:blueprint  → chapter-blueprint.yaml
3. /drama:script     → script-full.md
4. /drama:image-prompt → image-prompts.yaml
5. /drama:export     → 원하는 형식
```

### 부분 실행
기존 결과물이 있으면 중간부터 시작 가능:

```
# 블루프린트만 다시 생성
/drama:blueprint

# 특정 챕터 대본만 재생성
/drama:script --chapter 5

# 이미지 프롬프트부터 시작
/drama:image-prompt
```

### 병렬 실행
대본 생성과 이미지 프롬프트는 독립적으로 실행 가능:

```
# 대본 수정 중에 이미지 프롬프트 생성 가능
/drama:image-prompt --chapter 1-4
```
