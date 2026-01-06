# Step 2: 챕터 선택

## 목표
생성할 챕터를 선택합니다.

## 수행 작업

### 1. 생성 모드 선택

> **대본 생성 모드를 선택해주세요:**
>
> 1. **순차 생성** - 1장부터 차례로 (권장)
>    각 챕터 완성 후 확인하며 진행
>
> 2. **특정 챕터 선택** - 원하는 챕터만
>    이미 작성된 챕터 수정 또는 건너뛰기
>
> 3. **전체 생성** - 8챕터 한번에
>    빠르지만 중간 확인 불가

### 2. 순차 생성 시

다음 생성할 챕터 확인:

> **챕터 {N}: {chapter_title}**
>
> 청사진 요약:
> {chapter_summary}
>
> 핵심 장면:
> 1. {scene_1_description}
> 2. {scene_2_description}
> 3. {scene_3_description}
>
> 감정 곡선:
> {emotional_start} → {turning_point} → {emotional_end}
>
> 이 챕터 대본을 생성할까요?

### 3. 특정 챕터 선택 시

> 어떤 챕터를 생성/수정할까요?
>
> 1. 챕터 1 - {title} {status}
> 2. 챕터 2 - {title} {status}
> 3. 챕터 3 - {title} {status}
> ...

### 4. 이전 챕터 컨텍스트 로드

2챕터 이상 생성 시, 이전 챕터 요약 로드:

```
previous_chapters = []
for i in range(1, current_chapter):
    summary = load_summary(chapter_i)
    previous_chapters.append(summary)
```

## 다음 단계
→ step-03-write.md (대본 작성)
