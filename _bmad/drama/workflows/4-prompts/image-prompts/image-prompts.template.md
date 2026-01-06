# {{project_name}} - 이미지 프롬프트 모음

## 프로젝트 정보

| 항목 | 내용 |
|------|------|
| **제목** | {{title}} |
| **총 프롬프트** | {{total_prompts}}개 |
| **생성일** | {{created_date}} |

---

## 캐릭터 참조

{{#characters}}
### {{name}} ({{age}}세)

```
{{englishImagePrompt}}
```

{{/characters}}

---

## 챕터별 이미지 프롬프트

{{#chapters}}
### 챕터 {{number}}: {{title}}

{{#scenes}}
#### Scene {{scene_number}}: {{location}}

**상황:**
{{situation}}

**등장인물:**
{{characters_list}}

**영문 프롬프트:**
```
{{imagePrompt}}
```

---

{{/scenes}}
{{/chapters}}

## 썸네일 추천 장면

| 우선순위 | 챕터 | 장면 | 설명 |
|----------|------|------|------|
{{#thumbnails}}
| {{priority}} | Ch{{chapter}} | Scene{{scene}} | {{description}} |
{{/thumbnails}}

---

## n8n API 호출용

아래 JSON을 n8n HTTP Request 노드에서 사용하세요:

```json
{
  "contents": [
    {
      "parts": [
        {
          "text": "{{first_prompt}}"
        }
      ]
    }
  ]
}
```

---

*다음 단계: 내보내기 (/drama:export)*
