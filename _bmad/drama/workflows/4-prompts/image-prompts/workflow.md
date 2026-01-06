# 이미지 프롬프트 워크플로우

## 개요
대본의 핵심 장면을 이미지 생성 AI용 프롬프트로 변환합니다.

## 워크플로우 단계

### Step 1: 초기화
{project-root}/_bmad/drama/workflows/4-prompts/image-prompts/steps/step-01-init.md

### Step 2: 장면 분석
{project-root}/_bmad/drama/workflows/4-prompts/image-prompts/steps/step-02-analyze.md

### Step 3: 프롬프트 생성
{project-root}/_bmad/drama/workflows/4-prompts/image-prompts/steps/step-03-generate.md

### Step 4: 완료
{project-root}/_bmad/drama/workflows/4-prompts/image-prompts/steps/step-04-complete.md

## 입력
- scripts/chapter-{N}.md (대본)
- scripts/chapter-{N}-prompts.json (기존 프롬프트)
- characters.json (캐릭터 정보)

## 출력
- image-prompts/all-prompts.md (전체 정리)
- image-prompts/prompts-for-api.json (API 호출용)

## 필요 데이터
- {project-root}/_bmad/drama/data/prompts/image-prompt-guide.md
