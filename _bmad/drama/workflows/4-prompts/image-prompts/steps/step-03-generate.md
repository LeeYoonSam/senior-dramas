# Step 3: 프롬프트 생성

## 목표
분석된 장면에 대한 상세 이미지 프롬프트를 생성합니다.

## 프롬프트 생성 규칙

### 포함할 요소
1. **상황 설명** (Situation)
2. **등장인물 정보** (Characters)
3. **시선 처리** (Gaze) - 카메라 직시 금지
4. **장면 묘사** (Scene Description)
   - 자세와 행동
   - 표정
   - 배경과 소품
   - 상호작용

### 제외할 요소
- 아트 스타일
- 아티스트 이름
- 조명 설정
- 카메라 앵글/렌즈

## 수행 작업

### 1. 프롬프트 템플릿 적용

```
[Chapter {N} - Scene {M}]
*Location:* {chapter_location}
*Situation:* {situation_summary}
*Characters:*
  * {character_A}: {name}, {age}, {relationship}
  * {character_B}: {name}, {age}, {relationship}
*Scene Description:*
  * *Character A:*
    * *Posture and Action:* {detailed_posture}
    * *Expression:* {detailed_expression}
    * *Gaze:* {gaze_target}
  * *Character B:*
    * *Posture and Action:* {detailed_posture}
    * *Expression:* {detailed_expression}
    * *Gaze:* {gaze_target}
  * *Background and Objects:* {background_description}
  * *Interaction:* {interaction_description}
```

### 2. 영문 프롬프트 변환

한글 장면 묘사를 영문 이미지 프롬프트로:

```
Korean family drama scene, realistic style.

A woman in her 60s with graying hair sits at a traditional
Korean dining table. She is looking down at an old photo album
with misty eyes. Slight tears forming at the corners of her eyes.
Soft afternoon light through the window. Traditional Korean home
interior with wooden furniture. Empty chairs around the table
suggesting absence of family members.
```

### 3. 캐릭터 일관성 체크

characters.json의 englishImagePrompt와 일치 확인:

> **캐릭터 외모 일관성 확인:**
>
> 김순자 (주인공):
> - 기본 설정: "60s, graying hair, warm face..."
> - Scene 3 프롬프트: ✅ 일치
> - Scene 7 프롬프트: ⚠️ 머리 색상 불일치 → 수정

### 4. 프롬프트 미리보기

> **생성된 프롬프트 미리보기**
>
> **Chapter 1 - Scene 1**
> ```
> {english_prompt}
> ```
>
> 수정이 필요하신가요?

## 다음 단계
→ step-04-complete.md (완료)
