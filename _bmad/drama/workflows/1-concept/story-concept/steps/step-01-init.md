# Step 1: 초기화

## 목표
스토리 컨셉 개발을 위한 환경을 준비합니다.

## 수행 작업

### 1. 설정 로드
```
config = load({project-root}/_bmad/drama/config.yaml)
```

### 2. 프로젝트 이름 확인
사용자에게 프로젝트 이름을 요청합니다:

> "새로운 드라마 프로젝트를 시작하겠습니다.
> 프로젝트 이름을 정해주세요. (예: 엄마의-눈물, 시월드-전쟁)"

### 3. 프로젝트 폴더 생성
```
mkdir -p {output_folder}/{project_name}
```

### 4. 테마 데이터 로드
사용 가능한 테마 목록을 준비합니다:
- 가족 갈등 (family-conflict.yaml)
- 화해와 용서 (reconciliation.yaml)
- 세대 간 사랑 (generational-love.yaml)
- 희생과 헌신 (sacrifice.yaml)

## 다음 단계
→ step-02-theme.md (테마 선택)
