# 대본 생성 워크플로우

## 개요
8챕터 청사진을 바탕으로 각 챕터의 상세 대본을 생성합니다.

## 워크플로우 단계

### Step 1: 초기화
{project-root}/_bmad/drama/workflows/3-script/generate-script/steps/step-01-init.md

### Step 2: 챕터 선택
{project-root}/_bmad/drama/workflows/3-script/generate-script/steps/step-02-select.md

### Step 3: 대본 작성
{project-root}/_bmad/drama/workflows/3-script/generate-script/steps/step-03-write.md

### Step 4: 검토 및 수정
{project-root}/_bmad/drama/workflows/3-script/generate-script/steps/step-04-review.md

### Step 5: 완료
{project-root}/_bmad/drama/workflows/3-script/generate-script/steps/step-05-complete.md

## 입력
- blueprint.yaml (이전 단계)
- characters.json (이전 단계)

## 출력
- scripts/chapter-{N}.md (각 챕터 대본)
- scripts/chapter-{N}-prompts.json (이미지 프롬프트)

## 필요 데이터
- {project-root}/_bmad/drama/data/prompts/script-generation.md
- {project-root}/_bmad/drama/data/styles/*.md
