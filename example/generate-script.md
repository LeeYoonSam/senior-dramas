# 대본생성 Prompt (User Message)

```
system message에 있는 프롬프트 규칙에 따라서 아래 챕터 대본을 구성해줘 앞단계는 모두 완료되었으니 full script writing 다음부터 진행해서 전달해줘
:{{ $json['프롬프트'] }}, 대답은 Json 형태를 꼭 지켜줘 {
  "chapters": {
    "chapter1": "string"
    },
  "imagePrompts": {
    "scene1": {
      "location": "string",
      "situation": "string",
      "characters": "string",
      "imagePrompt": "string"
    },
    "scene2": {
      "location": "string",
      "situation": "string",
      "characters": "string",
      "imagePrompt": "string"
    },
    "scene3": {
      "location": "string",
      "situation": "string",
      "characters": "string",
      "imagePrompt": "string"
    }
  }
}
```