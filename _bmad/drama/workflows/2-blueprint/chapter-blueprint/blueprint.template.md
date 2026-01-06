# {{project_name}} - 8챕터 청사진

## 스토리 메타데이터

| 항목 | 내용 |
|------|------|
| **제목 (가제)** | {{title}} |
| **핵심 감정 키워드** | {{emotional_keyword_1}}, {{emotional_keyword_2}} |
| **상징적 소품** | {{symbolic_object}} |

---

## 등장인물

{{#characters}}
### {{name}} ({{age}}세) - {{role}}

| 항목 | 내용 |
|------|------|
| **관계** | {{relationship}} |
| **성격** | {{personality}} |
| **숨겨진 내면** | {{hidden_self}} |
| **상처** | {{wound}} |
| **욕망** | {{desire}} |

**이미지 프롬프트:**
```
{{englishImagePrompt}}
```

{{/characters}}

---

## 8챕터 구조

{{#chapters}}
### 챕터 {{number}}: {{title}}

**요약:**
{{summary}}

**감정 곡선:**
- 시작: {{emotional_start}}
- 전환점: {{turning_point}}
- 끝: {{emotional_end}}

**핵심 장면:**
{{#key_scenes}}
- **{{location}}**: {{description}}
  - 등장: {{characters}}
  - 핵심 대사: "{{key_dialogue}}"
{{/key_scenes}}

**챕터 훅:**
> {{chapter_hook}}

---

{{/chapters}}

## 전체 스토리 아크

```
Ch1 ──→ Ch2 ──→ Ch3 ──→ Ch4 ──→ Ch5 ──→ Ch6 ──→ Ch7 ──→ Ch8
평온    갈등    고립    희망    반전    절망    폭발    화해
  │      │      │      │      │      │      │      │
  ▼      ▼      ▼      ▼      ▼      ▼      ▼      ▼
일상   상처   결심   조력자  비밀   최악  클라이막스 새시작
```

---

*생성일: {{created_date}}*
*다음 단계: 대본 생성 (/drama:script)*
