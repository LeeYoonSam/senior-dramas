# Step 4: 완료

## 목표
이미지 프롬프트를 정리하고 저장합니다.

## 수행 작업

### 1. 파일 저장

```
{output_folder}/{project_name}/image-prompts/
├── all-prompts.md          # 전체 프롬프트 문서
├── prompts-for-api.json    # API 호출용 JSON
├── thumbnail-prompts.md    # 썸네일용 프롬프트
└── character-reference.md  # 캐릭터 외모 참조
```

### 2. API용 JSON 형식

```json
{
  "projectName": "{project_name}",
  "totalPrompts": 24,
  "prompts": [
    {
      "id": "ch1-scene1",
      "chapter": 1,
      "scene": 1,
      "location": "챕터 도입부",
      "prompt": "Korean family drama scene...",
      "characters": ["김순자", "박영희"],
      "emotion": "tension",
      "priority": "high"
    }
  ]
}
```

### 3. 완료 요약

```
┌──────────────────────────────────────────┐
│ 🖼️ 이미지 프롬프트 완성!                   │
├──────────────────────────────────────────┤
│ 총 프롬프트: {total_count}개               │
│ 썸네일용: {thumbnail_count}개              │
│                                          │
│ 저장 위치:                                 │
│ {output_folder}/{project_name}/           │
│ └── image-prompts/                        │
├──────────────────────────────────────────┤
│ 다음 단계:                                 │
│ 1. 내보내기 (/drama:export)               │
│ 2. 이미지 생성 테스트                      │
│ 3. 메뉴로 돌아가기                         │
└──────────────────────────────────────────┘
```

### 4. 이미지 생성 서비스 안내

> **이미지 생성 옵션:**
>
> 생성된 프롬프트로 다음 서비스에서 이미지를 생성할 수 있습니다:
>
> - **Gemini Imagen** (n8n 워크플로우에 포함)
> - **DALL-E 3**
> - **Midjourney**
> - **Stable Diffusion**
>
> n8n 워크플로우로 내보내기하면 자동 이미지 생성 파이프라인이
> 포함됩니다.

## 워크플로우 완료

이미지 프롬프트 워크플로우가 종료되었습니다.
