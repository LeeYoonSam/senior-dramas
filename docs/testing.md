# 테스트 가이드

Senior Dramas 프롬프트 테스트 시스템에 대한 상세 가이드입니다.

## 테스트 시스템 개요

프롬프트와 생성된 콘텐츠의 품질을 검증하기 위한 체계적인 테스트 도구를 제공합니다.

### 테스트의 필요성

1. **품질 보장**: 일관된 품질의 콘텐츠 생성
2. **타겟 적합성**: 50-70대 여성 시청자에 최적화
3. **일관성 유지**: 캐릭터, 설정의 일관성 검증
4. **오류 방지**: 설정 오류, 모순 검출

---

## 테스트 실행

### 기본 실행

```
/drama:test
```

### 특정 테스트만 실행

```
# 프롬프트 품질 테스트
/drama:test --type prompt-quality

# 일관성 테스트
/drama:test --type consistency

# 테마 적합성 테스트
/drama:test --type theme-adherence
```

### 특정 프로젝트 테스트

```
/drama:test --project "시어머니의마음"
```

---

## 3가지 테스트 모드

### 1. 프롬프트 품질 테스트 (prompt-quality)

생성된 프롬프트의 문장 품질과 타겟 적합성을 검증합니다.

#### 검증 항목

| 항목 | 기준 | 점수 |
|------|------|------|
| 문장 구조 | 자연스러운 한국어 | 0-20 |
| 어휘 선택 | 시니어 친화적 어휘 | 0-20 |
| 감정 표현 | 적절한 감정 묘사 | 0-20 |
| 대화 자연스러움 | 세대별 말투 반영 | 0-20 |
| 내레이션 품질 | 몰입감 있는 서술 | 0-20 |

#### 출력 예시

```yaml
test_type: prompt-quality
score: 85

details:
  sentence_structure: 18
  vocabulary: 17
  emotion_expression: 16
  dialogue_naturalness: 17
  narration_quality: 17

issues:
  - location: "3장 씬2"
    issue: "현대 신조어 사용"
    suggestion: "'갓생'을 '열심히 사는'으로 수정"

  - location: "5장 대화"
    issue: "순자 말투 불일치"
    suggestion: "경상도 사투리 일관성 유지 필요"
```

### 2. 일관성 테스트 (consistency)

캐릭터, 설정, 시간 순서의 일관성을 검증합니다.

#### 검증 항목

| 항목 | 설명 |
|------|------|
| 캐릭터 말투 | 각 캐릭터의 말투가 일관적인가 |
| 캐릭터 성격 | 성격 묘사가 일관적인가 |
| 설정 일치 | 나이, 관계, 배경이 일치하는가 |
| 시간 순서 | 사건 순서에 모순이 없는가 |
| 장소 연속성 | 장소 이동이 논리적인가 |

#### 출력 예시

```yaml
test_type: consistency
score: 90

character_consistency:
  김순자:
    speech_pattern: "일관"
    personality: "일관"
    issues: []

  박민지:
    speech_pattern: "불일치 발견"
    personality: "일관"
    issues:
      - chapter: 4
        issue: "존댓말→반말 전환 근거 부족"

setting_consistency:
  timeline: "일관"
  locations: "일관"
  relationships: "일관"

errors:
  - type: "시간 모순"
    location: "6장"
    description: "순자 나이 67세→70세 불일치"
    severity: "medium"
```

### 3. 테마 적합성 테스트 (theme-adherence)

선택한 테마와의 정합성을 검증합니다.

#### 검증 항목

| 항목 | 설명 |
|------|------|
| 테마 표현 | 선택한 테마가 충분히 표현되는가 |
| 감정 곡선 | 테마에 맞는 감정 흐름인가 |
| 메시지 전달 | 의도한 메시지가 전달되는가 |
| 결말 적합성 | 테마에 맞는 결말인가 |

#### 출력 예시

```yaml
test_type: theme-adherence
selected_theme: reconciliation
score: 86

theme_expression:
  score: 85
  strengths:
    - "화해 과정이 자연스럽게 묘사됨"
    - "용서의 순간이 감동적"
  weaknesses:
    - "초반 갈등 원인이 약간 모호함"

emotional_arc:
  expected: [긴장, 분노, 희망, 시도, 절망, 깨달음, 화해, 평화]
  actual: [긴장, 분노, 희망, 시도, 슬픔, 깨달음, 화해, 평화]
  match: 87%
  note: "5장 '슬픔'이 '절망'보다 약함"

message_delivery:
  intended: "용서는 자신을 위한 것"
  clarity: 80%
  suggestions:
    - "6장에서 메시지를 더 명확히"
```

---

## 테스트 케이스 작성법

### 테스트 케이스 위치

```
_bmad/drama/testing/
├── test-runner.md
├── templates/
│   ├── quality-test.yaml
│   ├── consistency-test.yaml
│   └── theme-test.yaml
└── fixtures/
    └── sample-data/
```

### 커스텀 테스트 케이스

새로운 테스트 케이스를 작성할 수 있습니다:

```yaml
# my-custom-test.yaml

name: "사투리 일관성 테스트"
description: "경상도 사투리가 일관적으로 사용되는지 검증"

criteria:
  - name: "어미 일관성"
    patterns:
      - "~했다"  # 표준어
      - "~했다카이"  # 경상도
    rule: "캐릭터별 일관성 유지"

  - name: "특수 어휘"
    allowed_for:
      김순자: ["와", "니", "카이", "싶다"]
    disallowed_for:
      박민지: ["카이", "마"]  # 서울 출신

scoring:
  pass_threshold: 80
  weight: 1.0
```

### 테스트 케이스 실행

```bash
/drama:test --custom my-custom-test.yaml
```

---

## 품질 평가 기준

### 종합 점수 체계

| 등급 | 점수 | 설명 |
|------|------|------|
| A | 90-100 | 출시 가능 품질 |
| B | 80-89 | 소폭 수정 필요 |
| C | 70-79 | 수정 필요 |
| D | 60-69 | 대폭 수정 필요 |
| F | 0-59 | 재작성 권장 |

### 각 테스트별 가중치

```yaml
weights:
  prompt-quality: 0.4    # 40%
  consistency: 0.35      # 35%
  theme-adherence: 0.25  # 25%

final_score = (prompt * 0.4) + (consistency * 0.35) + (theme * 0.25)
```

### 자동 권장 사항

점수에 따라 자동으로 권장 사항이 생성됩니다:

```yaml
recommendations:
  high_priority:
    - "3장 순자 말투 수정 필요"
    - "5장 감정 표현 강화 필요"

  medium_priority:
    - "1장 배경 설명 보강"
    - "7장 대화 속도 조절"

  low_priority:
    - "4장 내레이션 다듬기"
```

---

## 테스트 결과 활용

### 결과 파일 위치

```
output/dramas/{project}/test-results/
├── prompt-quality.json
├── consistency.json
├── theme-adherence.json
└── summary.json
```

### 결과 기반 수정

테스트 결과를 바탕으로 특정 챕터만 재생성할 수 있습니다:

```bash
# 문제있는 챕터만 재생성
/drama:script --chapter 3

# 특정 씬만 수정
/drama:script --chapter 5 --scene 2
```

### 반복 테스트

수정 후 재테스트:

```bash
# 수정 → 테스트 반복
/drama:script --chapter 3
/drama:test --type consistency --chapter 3
```

---

## 테스트 자동화

### 전체 워크플로우에 테스트 포함

대본 생성 후 자동으로 테스트를 실행하도록 설정할 수 있습니다:

```bash
# 대본 생성 + 테스트
/drama:script
/drama:test

# 결과 확인 후 내보내기
/drama:export
```

### 품질 게이트

특정 점수 이하면 경고를 표시합니다:

```yaml
quality_gate:
  minimum_score: 75
  action_on_fail: "warn"  # warn, block, or ignore

  rules:
    - test: prompt-quality
      minimum: 70
    - test: consistency
      minimum: 80
    - test: theme-adherence
      minimum: 70
```

---

## 테스트 팁

### 효과적인 테스트 순서

1. **consistency** 먼저 - 설정 오류 조기 발견
2. **prompt-quality** - 문장 품질 검증
3. **theme-adherence** - 전체 방향성 확인

### 자주 발견되는 문제

| 문제 유형 | 원인 | 해결책 |
|----------|------|--------|
| 말투 불일치 | 챕터별 생성 시 불일치 | 스타일 가이드 강화 |
| 나이 오류 | 계산 실수 | story-concept 재확인 |
| 감정 곡선 이탈 | 블루프린트 미준수 | 블루프린트 재확인 |
| 신조어 사용 | AI 기본 성향 | 어휘 제한 설정 |

### 테스트 건너뛰기

급할 때는 테스트를 건너뛸 수 있지만 권장하지 않습니다:

```bash
# 내보내기만 실행 (테스트 없이)
/drama:export --skip-test
```
