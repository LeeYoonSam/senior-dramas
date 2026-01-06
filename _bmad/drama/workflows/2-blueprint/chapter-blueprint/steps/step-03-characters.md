# Step 3: 등장인물 프로필

## 목표
3차원적인 등장인물 프로필을 생성합니다.

## 등장인물 구성

### 필수 인물
1. **주인공** (50-70대 여성)
2. **핵심 갈등 상대** (시어머니/며느리/남편/자녀 등)
3. **조력자** (예상치 못한 편)

### 선택 인물
4. 기타 가족 구성원
5. 외부 인물 (친구, 이웃 등)

## 캐릭터 프로필 구성 요소

각 인물에 대해 다음을 정의:

### 기본 정보
- 이름, 나이, 관계
- 외모 특징 (이미지 프롬프트용)

### 성격과 특성
- 표면적 성격
- 숨겨진 내면
- 말버릇, 행동 습관

### 배경 스토리
- 숨겨진 과거
- 가족에 대한 진심
- 상호 오해의 근원

### 상처와 욕망
- 개인적 상처
- 진정으로 원하는 것

## 수행 작업

### 1. 핵심 인물 정의

주인공부터 상세 프로필 작성:

> **주인공 프로필을 만들어볼게요.**
>
> 이미 정한 정보:
> - 이름: {protagonist_name}
> - 나이: {protagonist_age}세
>
> 추가로 필요한 정보:
> 1. 외모 특징 (머리 스타일, 인상 등)
> 2. 성격 한 줄 요약
> 3. 숨기고 있는 상처나 비밀
> 4. 가장 원하는 것

### 2. 관계 지도 작성

인물 간 관계를 정리:

```
주인공 ──(시월드 30년)── 시어머니
   │
   ├──(권태기)── 남편
   │
   ├──(세대 갈등)── 며느리/아들
   │
   └──(우정)── 친구
```

### 3. 영문 이미지 프롬프트 생성

각 인물의 외모를 영문 프롬프트로:

```
"Korean woman in her 60s, warm gentle face, slightly graying hair
pulled back, wearing simple comfortable clothes, kind eyes with
hidden sadness, soft wrinkles around eyes from years of smiling
through hardship"
```

### 4. JSON 형식 저장

```json
{
  "characters": {
    "김순자": {
      "name": "김순자",
      "age": 65,
      "role": "주인공",
      "relationship": "며느리/어머니",
      "detail": "40년 주부 경력, 시어머니와 30년 갈등...",
      "englishImagePrompt": "Korean woman in her 60s..."
    },
    "박영희": {
      "name": "박영희",
      "age": 88,
      "role": "시어머니",
      ...
    }
  }
}
```

## 다음 단계
→ step-04-outline.md (챕터별 아웃라인)
