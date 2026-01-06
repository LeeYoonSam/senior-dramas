# Step 1: 형식 선택

## 목표
내보낼 형식과 내용을 선택합니다.

## 수행 작업

### 1. 프로젝트 상태 확인

```
project = load({output_folder}/{project_name})

status:
  story_concept: ✅
  blueprint: ✅
  scripts: 8/8 완료
  image_prompts: 24개
```

### 2. 내보내기 형식 선택

> **내보내기 형식을 선택해주세요:**
>
> 1. **n8n JSON 워크플로우** (Recommended)
>    - Google Sheets 트리거
>    - AI 대본 생성 노드
>    - 이미지 생성 노드
>    - n8n에서 바로 import 가능
>
> 2. **PDF 문서**
>    - 전체 드라마 통합 문서
>    - 인쇄 및 오프라인 공유용
>    - 한글 폰트 지원
>
> 3. **Markdown 파일**
>    - 편집 가능한 텍스트
>    - Git 버전 관리 용이
>    - 다른 도구 연동 용이
>
> 4. **모든 형식**
>    - 위 3가지 모두 생성

### 3. 내용 범위 선택

> **내보낼 내용을 선택해주세요:**
>
> - [x] 스토리 컨셉
> - [x] 8챕터 청사진
> - [x] 등장인물 프로필
> - [x] 전체 대본 (8챕터)
> - [x] 이미지 프롬프트
> - [ ] 유튜브 제목 (5개)
> - [ ] 썸네일 텍스트

### 4. 메타데이터 입력

n8n 워크플로우용 추가 정보:

> **n8n 설정:**
>
> - AI 모델: [GPT-4 / Claude / Gemini]
> - 이미지 생성 API: [Gemini Imagen / DALL-E / Midjourney]
> - API 키 placeholder 사용: [예 / 아니오]

## 다음 단계
→ step-02-generate.md (내보내기 생성)
