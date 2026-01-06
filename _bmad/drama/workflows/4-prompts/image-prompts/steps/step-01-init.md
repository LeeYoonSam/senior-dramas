# Step 1: 초기화

## 목표
이미지 프롬프트 정리를 위한 환경을 준비합니다.

## 수행 작업

### 1. 프로젝트 및 대본 로드

```
project = load({output_folder}/{project_name})
scripts = load_all({output_folder}/{project_name}/scripts/*.md)
characters = load({output_folder}/{project_name}/characters.json)
```

### 2. 현재 상태 확인

> **이미지 프롬프트 현황**
>
> | 챕터 | 대본 | 프롬프트 |
> |------|------|----------|
> | Ch1  | ✅   | 3개      |
> | Ch2  | ✅   | 3개      |
> | ...  |      |          |
>
> 총 프롬프트: {total_count}개

### 3. 작업 모드 선택

> **어떤 작업을 하시겠어요?**
>
> 1. **전체 정리** - 모든 챕터 프롬프트 통합 문서 생성
> 2. **특정 챕터 수정** - 개별 챕터 프롬프트 수정
> 3. **추가 장면** - 기존 3개 외 추가 장면 생성
> 4. **API 형식 변환** - n8n/이미지 생성 API용 JSON

### 4. 이미지 프롬프트 폴더 생성

```
mkdir -p {output_folder}/{project_name}/image-prompts
```

## 다음 단계
→ step-02-analyze.md (장면 분석)
