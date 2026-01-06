# Step 2: 내보내기 생성

## 목표
선택한 형식으로 파일을 생성합니다.

## 형식별 생성 방법

### n8n JSON 워크플로우

템플릿 로드 및 변수 치환:

```javascript
// 기본 구조
{
  "name": "Senior Drama Generator - {project_name}",
  "nodes": [
    // 1. Google Sheets Trigger
    {
      "type": "n8n-nodes-base.googleSheetsTrigger",
      "parameters": {
        "sheetId": "{SHEET_ID}",
        "sheetName": "주제"
      }
    },
    // 2. System Prompt 설정
    {
      "type": "n8n-nodes-base.set",
      "parameters": {
        "systemPrompt": "{system_prompt_content}"
      }
    },
    // 3. AI 청사진 생성
    {
      "type": "n8n-nodes-langchain.openAi",
      "parameters": {
        "model": "{ai_model}",
        "messages": "{blueprint_prompt}"
      }
    },
    // 4. JSON 파서
    {
      "type": "n8n-nodes-base.code",
      "parameters": {
        "jsCode": "{json_parser_code}"
      }
    },
    // 5. 대본 생성 (Loop)
    // 6. 이미지 생성
    {
      "type": "n8n-nodes-base.httpRequest",
      "parameters": {
        "url": "{image_api_url}",
        "body": "{image_request_body}"
      }
    }
  ],
  "connections": { ... }
}
```

### PDF 문서

pandoc 사용:

```bash
pandoc "{source_md}" \
  -o "{output_pdf}" \
  --pdf-engine=xelatex \
  -V mainfont="Noto Sans CJK KR" \
  -V geometry:margin=2cm \
  --toc \
  --toc-depth=2 \
  --metadata title="{title}" \
  --metadata author="시니어 드라마 생성기"
```

PDF 내용 구조:
1. 표지
2. 목차
3. 스토리 컨셉
4. 등장인물
5. 8챕터 청사진
6. 전체 대본
7. 이미지 프롬프트

### Markdown 통합 문서

```markdown
# {project_name} - 시니어 드라마 완성본

## 메타데이터
- 생성일: {date}
- 테마: {theme}
- 타겟: 50-70대 여성

## 목차
1. [스토리 컨셉](#스토리-컨셉)
2. [등장인물](#등장인물)
3. [8챕터 청사진](#청사진)
4. [대본](#대본)
5. [이미지 프롬프트](#이미지-프롬프트)

---

## 스토리 컨셉
{story_concept_content}

## 등장인물
{characters_content}

## 청사진
{blueprint_content}

## 대본
### 챕터 1
{chapter_1_script}
...

## 이미지 프롬프트
{image_prompts_content}
```

## 수행 작업

### 1. 데이터 수집

```
collect:
  - story-concept.yaml
  - blueprint.yaml
  - characters.json
  - scripts/chapter-*.md
  - image-prompts/*.json
```

### 2. 템플릿 렌더링

선택한 형식의 템플릿에 데이터 적용

### 3. 파일 생성

```
{output_folder}/{project_name}/exports/
├── n8n/
│   └── {project_name}-workflow.json
├── pdf/
│   └── {project_name}-complete.pdf
└── markdown/
    └── {project_name}-complete.md
```

### 4. 유효성 검증

- n8n JSON: JSON 문법 검증
- PDF: 파일 생성 확인
- Markdown: 링크/이미지 경로 확인

## 다음 단계
→ step-03-complete.md (완료)
