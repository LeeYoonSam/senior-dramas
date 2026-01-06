# 내보내기 워크플로우

## 개요
생성된 드라마 프로젝트를 다양한 형식으로 내보냅니다.

## 지원 형식
1. **n8n JSON** - n8n 워크플로우로 바로 import 가능
2. **PDF** - 인쇄/공유용 문서
3. **Markdown** - 편집 가능한 통합 문서

## 워크플로우 단계

### Step 1: 형식 선택
{project-root}/_bmad/drama/workflows/5-export/export-workflow/steps/step-01-select.md

### Step 2: 내보내기 생성
{project-root}/_bmad/drama/workflows/5-export/export-workflow/steps/step-02-generate.md

### Step 3: 완료
{project-root}/_bmad/drama/workflows/5-export/export-workflow/steps/step-03-complete.md

## 입력
- story-concept.yaml
- blueprint.yaml
- characters.json
- scripts/*.md
- image-prompts/*.json

## 출력
- exports/{format}/{project_name}.{ext}
