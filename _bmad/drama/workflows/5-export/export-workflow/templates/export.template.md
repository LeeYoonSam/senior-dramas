# {{project_name}} - 시니어 드라마 완성본

> 생성일: {{created_date}}
> 테마: {{theme_main}} > {{theme_sub}}
> 타겟: 50-70대 여성

---

## 목차

1. [스토리 컨셉](#스토리-컨셉)
2. [등장인물](#등장인물)
3. [8챕터 청사진](#8챕터-청사진)
4. [전체 대본](#전체-대본)
5. [이미지 프롬프트](#이미지-프롬프트)
6. [유튜브 활용 자료](#유튜브-활용-자료)

---

## 스토리 컨셉

### 제목 (가제)
**{{title}}**

### 로그라인
{{logline}}

### 핵심 감정 키워드
{{#emotional_keywords}}
- {{.}}
{{/emotional_keywords}}

### 상징적 소품
**{{symbolic_object}}**

{{symbolic_object_description}}

---

## 등장인물

{{#characters}}
### {{name}} ({{age}}세) - {{role}}

| 항목 | 내용 |
|------|------|
| **관계** | {{relationship}} |
| **성격** | {{personality}} |
| **숨겨진 내면** | {{hiddenSelf}} |
| **상처** | {{wound}} |
| **욕망** | {{desire}} |

**외모 (이미지 프롬프트):**
```
{{englishImagePrompt}}
```

---

{{/characters}}

## 8챕터 청사진

{{#chapters}}
### 챕터 {{number}}: {{title}}

**요약:** {{summary}}

**감정 곡선:** {{emotional_start}} → {{turning_point}} → {{emotional_end}}

**챕터 훅:** {{chapter_hook}}

---

{{/chapters}}

## 전체 대본

{{#scripts}}
### 챕터 {{number}}: {{title}}

---

{{content}}

---

**분량:** {{word_count}}자

{{/scripts}}

## 이미지 프롬프트

{{#image_prompts}}
### 챕터 {{chapter}} - Scene {{scene}}

**위치:** {{location}}

**상황:** {{situation}}

**등장인물:** {{characters_list}}

**영문 프롬프트:**
```
{{imagePrompt}}
```

---

{{/image_prompts}}

## 유튜브 활용 자료

### 추천 제목 (5개)

1. {{youtube_title_1}}
2. {{youtube_title_2}}
3. {{youtube_title_3}}
4. {{youtube_title_4}}
5. {{youtube_title_5}}

### 썸네일 텍스트

**{{thumbnail_text}}**

### 영상 설명 템플릿

```
{{video_description}}
```

---

*이 문서는 시니어 드라마 프롬프트 시스템으로 생성되었습니다.*
*자동화 문의: /drama:agent*
