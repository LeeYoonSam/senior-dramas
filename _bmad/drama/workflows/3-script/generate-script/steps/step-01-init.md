# Step 1: 초기화

## 목표
대본 생성을 위한 환경을 준비합니다.

## 수행 작업

### 1. 프로젝트 로드

```
blueprint = load({output_folder}/{project_name}/blueprint.yaml)
characters = load({output_folder}/{project_name}/characters.json)
```

### 2. 청사진 요약 확인

> 📋 현재 프로젝트 상태
>
> **프로젝트**: {project_name}
> **제목**: {title}
> **등장인물**: {character_count}명
>
> **챕터 진행 상황**:
> - Ch1: {status} ✅/⏳
> - Ch2: {status}
> - ...

### 3. 스타일 가이드 로드

대본 작성에 필요한 스타일 가이드 참조:

```
load({project-root}/_bmad/drama/data/styles/narration-styles.md)
load({project-root}/_bmad/drama/data/styles/dialogue-patterns.md)
load({project-root}/_bmad/drama/data/styles/emotion-expressions.md)
load({project-root}/_bmad/drama/data/prompts/script-generation.md)
```

### 4. 스크립트 폴더 생성

```
mkdir -p {output_folder}/{project_name}/scripts
```

## 다음 단계
→ step-02-select.md (챕터 선택)
