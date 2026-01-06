# 커맨드 레퍼런스

Senior Dramas 시스템에서 사용할 수 있는 7개의 슬래시 커맨드 상세 설명입니다.

## 커맨드 개요

| 커맨드 | 목적 | 입력 | 출력 |
|--------|------|------|------|
| `/drama:agent` | 대화형 에이전트 | 없음 | 메뉴 기반 대화 |
| `/drama:story` | 스토리 컨셉 | 아이디어 | story-concept.yaml |
| `/drama:blueprint` | 챕터 설계 | story-concept | chapter-blueprint.yaml |
| `/drama:script` | 대본 생성 | blueprint | script-*.md |
| `/drama:image-prompt` | 이미지 프롬프트 | script | image-prompts.yaml |
| `/drama:export` | 내보내기 | 모든 결과물 | n8n/PDF/Markdown |
| `/drama:test` | 테스트 | 테스트 케이스 | 검증 보고서 |

---

## /drama:agent

드라마 작가 "미영" 에이전트를 시작합니다.

### 설명
대화형 메뉴를 통해 전체 워크플로우를 안내받을 수 있습니다. 처음 사용자에게 권장됩니다.

### 사용법
```
/drama:agent
```

### 실행 결과
- 미영 작가의 인사말 표시
- 대화형 메뉴 제공
- TTS 음성 안내 (AgentVibes 설정 시)

### 메뉴 옵션
1. 새 스토리 시작
2. 기존 스토리 이어서 작업
3. 대본 생성
4. 이미지 프롬프트 생성
5. 내보내기
6. 프롬프트 테스트

---

## /drama:story

스토리 컨셉을 생성합니다.

### 설명
드라마의 기본 설정(원라인, 테마, 캐릭터, 갈등 구조)을 정의합니다.

### 사용법
```
/drama:story

# 또는 아이디어와 함께
/drama:story "시어머니와 며느리의 화해 이야기"
```

### 입력 요소
- **원라인**: 한 줄로 표현한 스토리
- **테마**: family-conflict, reconciliation, generational-love, sacrifice 중 선택
- **주요 캐릭터**: 2-4명의 핵심 인물
- **갈등 구조**: 메인/서브 갈등 정의

### 출력
`output/dramas/{project}/story-concept.yaml`

```yaml
project_name: "시어머니의 마음"
one_liner: "30년 갈등 끝에 진심을 마주한 시어머니와 며느리"
theme: reconciliation
main_conflict: "오해로 시작된 시월드 갈등"
characters:
  - name: "김순자"
    role: "시어머니"
    age: 68
    ...
```

### 워크플로우 단계
1. 아이디어 수집
2. 테마 선택
3. 캐릭터 설계
4. 갈등 구조 정의
5. 컨셉 문서 생성

---

## /drama:blueprint

8장 구조의 챕터 블루프린트를 생성합니다.

### 설명
story-concept을 바탕으로 각 챕터의 내용, 장면, 감정 흐름을 설계합니다.

### 사용법
```
/drama:blueprint

# 특정 프로젝트 지정
/drama:blueprint --project "시어머니의마음"
```

### 선행 조건
- `/drama:story`로 생성된 `story-concept.yaml` 필요

### 출력
`output/dramas/{project}/chapter-blueprint.yaml`

```yaml
chapters:
  - chapter: 1
    title: "낯선 만남"
    theme: "갈등의 시작"
    scenes:
      - id: 1
        location: "아파트 거실"
        time: "저녁"
        characters: ["김순자", "박민지"]
        action: "첫 만남의 어색함"
        emotion: "긴장, 경계"
    ...
```

### 8장 구조
| 챕터 | 역할 | 감정 곡선 |
|------|------|----------|
| 1장 | 도입, 갈등 소개 | 긴장 |
| 2장 | 갈등 심화 | 불안 |
| 3장 | 전환점 1 | 희망 |
| 4장 | 새로운 시도 | 기대 |
| 5장 | 위기 | 절망 |
| 6장 | 깨달음 | 각성 |
| 7장 | 화해 시작 | 감동 |
| 8장 | 결말, 새로운 시작 | 희망, 위로 |

---

## /drama:script

대본을 생성합니다.

### 설명
블루프린트를 바탕으로 완성된 대본을 생성합니다. 전체 또는 특정 챕터만 생성 가능합니다.

### 사용법
```
# 전체 대본 생성
/drama:script

# 특정 챕터만 생성
/drama:script --chapter 3

# 챕터 범위 지정
/drama:script --chapters 1-4
```

### 선행 조건
- `chapter-blueprint.yaml` 필요

### 출력
- 전체: `output/dramas/{project}/script-full.md`
- 챕터별: `output/dramas/{project}/scripts/chapter-{n}.md`

### 대본 형식

```markdown
# 3장: 첫 번째 변화

## 씬 1: 병원 로비

**[내레이션]**
순자는 병원 복도에서 혼자 앉아 있었다.
지난 30년의 세월이 주마등처럼 스쳐 지나갔다.

**[대화]**
순자: (조용히) "민지야... 오래 기다렸니?"

민지: (놀라며) "어머니... 여기 왜..."

**[내면 독백 - 순자]**
'말 한마디가 이렇게 어려울 줄이야...'
```

### 3가지 서술 도구
1. **내레이션**: 상황 설명, 배경 묘사
2. **대화**: 캐릭터 간 대화
3. **내면 독백**: 캐릭터의 속마음

---

## /drama:image-prompt

이미지 프롬프트를 생성합니다.

### 설명
각 씬에 맞는 AI 이미지 생성용 프롬프트를 만듭니다.

### 사용법
```
/drama:image-prompt

# 특정 챕터만
/drama:image-prompt --chapter 1
```

### 선행 조건
- 대본 파일 필요

### 출력
`output/dramas/{project}/image-prompts.yaml`

```yaml
prompts:
  - scene_id: "ch1_s1"
    chapter: 1
    scene: 1
    description: "아파트 거실에서 처음 마주한 시어머니와 며느리"
    prompt: |
      Korean grandmother in her late 60s, modern apartment living room,
      evening light through window, tension in the air, warm but uneasy
      atmosphere, realistic style, soft lighting
    style: "realistic photograph"
    mood: "tense, cautious"
    elements:
      - "modern Korean apartment"
      - "evening lighting"
      - "two women facing each other"
```

### 프롬프트 스타일 옵션
- `realistic`: 사진 같은 현실적 이미지
- `illustration`: 일러스트 스타일
- `cinematic`: 영화 같은 연출

---

## /drama:export

생성된 결과물을 다양한 형식으로 내보냅니다.

### 설명
완성된 드라마를 n8n 워크플로우, PDF, Markdown 형식으로 내보냅니다.

### 사용법
```
# 모든 형식으로 내보내기
/drama:export

# 특정 형식 지정
/drama:export --format n8n
/drama:export --format pdf
/drama:export --format markdown
```

### 출력 형식

#### n8n JSON
```
output/dramas/{project}/exports/n8n-workflow.json
```
- Google Sheets 트리거 포함
- AI 대본 생성 노드
- 이미지 생성 노드 (Replicate/DALL-E)

#### PDF
```
output/dramas/{project}/exports/{project}.pdf
```
- 표지
- 캐릭터 소개
- 전체 대본
- 이미지 프롬프트 목록

#### Markdown
```
output/dramas/{project}/exports/{project}.md
```
- 모든 내용 통합된 단일 마크다운 파일

---

## /drama:test

프롬프트와 워크플로우를 테스트합니다.

### 설명
생성된 프롬프트의 품질을 검증하고 일관성을 체크합니다.

### 사용법
```
# 전체 테스트
/drama:test

# 특정 테스트만 실행
/drama:test --type prompt-quality
/drama:test --type consistency
/drama:test --type theme-adherence
```

### 테스트 유형

#### 1. 프롬프트 품질 테스트
- 문장 구조 검증
- 타겟 시청자 적합성
- 감정 표현 밀도

#### 2. 일관성 테스트
- 캐릭터 말투 일관성
- 설정 오류 검출
- 시간순 검증

#### 3. 테마 적합성 테스트
- 선택한 테마와의 정합성
- 메시지 전달 효과

### 출력
```
output/dramas/{project}/test-results/
├── prompt-quality.json
├── consistency.json
└── theme-adherence.json
```

### 품질 점수
```yaml
overall_score: 87
details:
  prompt_quality: 85
  consistency: 90
  theme_adherence: 86
recommendations:
  - "3장의 순자 말투를 더 부드럽게 조정 필요"
  - "5장 감정 표현 강화 권장"
```

---

## 커맨드 조합 예시

### 전체 워크플로우
```
/drama:story
/drama:blueprint
/drama:script
/drama:image-prompt
/drama:export --format all
```

### 빠른 대본 생성 (기존 컨셉 활용)
```
/drama:script --project "시어머니의마음"
```

### 테스트 후 수정
```
/drama:test
# 결과 확인 후
/drama:script --chapter 3  # 문제있는 챕터만 재생성
```
