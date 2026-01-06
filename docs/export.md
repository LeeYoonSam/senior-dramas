# 내보내기 가이드

Senior Dramas 결과물을 다양한 형식으로 내보내는 방법에 대한 가이드입니다.

## 지원 형식

| 형식 | 용도 | 파일 |
|------|------|------|
| n8n JSON | 자동화 워크플로우 | n8n-workflow.json |
| PDF | 인쇄/공유용 문서 | {project}.pdf |
| Markdown | 편집/공유용 | {project}.md |

---

## 기본 사용법

### 전체 형식으로 내보내기

```
/drama:export
```

모든 형식(n8n, PDF, Markdown)으로 동시에 내보냅니다.

### 특정 형식만 내보내기

```bash
# n8n 워크플로우만
/drama:export --format n8n

# PDF만
/drama:export --format pdf

# Markdown만
/drama:export --format markdown
```

### 특정 프로젝트 내보내기

```bash
/drama:export --project "시어머니의마음"
```

---

## n8n 워크플로우 내보내기

### 개요

n8n은 오픈소스 워크플로우 자동화 도구입니다. Google Sheets와 연동하여 대본 생성 및 이미지 생성을 자동화할 수 있습니다.

### 출력 파일

```
output/dramas/{project}/exports/n8n-workflow.json
```

### 워크플로우 구조

```
┌─────────────────┐
│ Google Sheets   │ ← 스토리 아이디어 입력
│ Trigger         │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│ AI Script       │ ← Claude API로 대본 생성
│ Generator       │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│ Image Prompt    │ ← 이미지 프롬프트 추출
│ Extractor       │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│ Image Generator │ ← Replicate/DALL-E 이미지 생성
│ (Replicate)     │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│ Google Sheets   │ ← 결과 저장
│ Output          │
└─────────────────┘
```

### n8n 설정 방법

#### 1. n8n 설치

```bash
# Docker로 설치
docker run -it --rm \
  --name n8n \
  -p 5678:5678 \
  -v ~/.n8n:/home/node/.n8n \
  n8nio/n8n

# 또는 npm으로 설치
npm install n8n -g
n8n start
```

#### 2. 워크플로우 가져오기

1. n8n 웹 인터페이스 접속 (http://localhost:5678)
2. "Import from File" 클릭
3. `n8n-workflow.json` 파일 선택
4. "Import" 버튼 클릭

#### 3. 자격 증명 설정

워크플로우에서 다음 자격 증명이 필요합니다:

| 서비스 | 필요한 키 | 설정 위치 |
|--------|----------|----------|
| Google Sheets | OAuth2 | Credentials → Google |
| Claude API | API Key | Credentials → HTTP Header |
| Replicate | API Token | Credentials → HTTP Header |

#### 4. Google Sheets 준비

스프레드시트 구조:

| 열 | 내용 | 예시 |
|----|------|------|
| A | 프로젝트명 | 시어머니의마음 |
| B | 원라인 | 30년 갈등 끝에 화해하는 시어머니와 며느리 |
| C | 테마 | reconciliation |
| D | 상태 | pending → processing → done |
| E | 대본 | (자동 생성) |
| F | 이미지 URL | (자동 생성) |

### 워크플로우 커스터마이징

#### 노드 수정

```json
{
  "name": "AI Script Generator",
  "type": "n8n-nodes-base.httpRequest",
  "parameters": {
    "url": "https://api.anthropic.com/v1/messages",
    "method": "POST",
    "headers": {
      "x-api-key": "{{$credentials.anthropicApi.apiKey}}",
      "anthropic-version": "2023-06-01"
    },
    "body": {
      "model": "claude-3-5-sonnet-20241022",
      "max_tokens": 4096,
      "messages": [...]
    }
  }
}
```

#### 이미지 생성기 변경

Replicate 대신 DALL-E 사용:

```json
{
  "name": "Image Generator",
  "type": "n8n-nodes-base.httpRequest",
  "parameters": {
    "url": "https://api.openai.com/v1/images/generations",
    "method": "POST",
    "headers": {
      "Authorization": "Bearer {{$credentials.openAiApi.apiKey}}"
    }
  }
}
```

---

## PDF 내보내기

### 개요

인쇄 및 공유용 PDF 문서를 생성합니다.

### 출력 파일

```
output/dramas/{project}/exports/{project}.pdf
```

### PDF 구성

1. **표지**
   - 프로젝트명
   - 원라인
   - 생성 날짜

2. **목차**
   - 챕터 목록

3. **캐릭터 소개**
   - 주요 캐릭터 프로필
   - 관계도

4. **대본 본문**
   - 8개 챕터
   - 내레이션/대화/독백 구분

5. **이미지 프롬프트 목록**
   - 씬별 프롬프트

### PDF 스타일 설정

```yaml
# config에서 PDF 스타일 설정
pdf_style:
  font_family: "Noto Sans KR"
  font_size: 12
  line_height: 1.6
  page_margin: "2cm"

  heading:
    chapter: 24
    scene: 18

  narration:
    style: "italic"
    color: "#333333"

  dialogue:
    indent: "2em"
    character_name: "bold"

  inner_monologue:
    style: "italic"
    prefix: "'"
    suffix: "'"
```

### PDF 생성 요구사항

PDF 생성을 위해 다음 도구 중 하나가 필요합니다:

```bash
# 옵션 1: wkhtmltopdf
brew install wkhtmltopdf  # macOS
apt install wkhtmltopdf   # Ubuntu

# 옵션 2: Pandoc + LaTeX
brew install pandoc
brew install --cask mactex

# 옵션 3: Chrome/Chromium (headless)
# 별도 설치 불필요 (시스템 Chrome 사용)
```

---

## Markdown 내보내기

### 개요

편집 및 공유용 단일 Markdown 파일을 생성합니다.

### 출력 파일

```
output/dramas/{project}/exports/{project}.md
```

### Markdown 구조

```markdown
# 시어머니의 마음

> 30년 갈등 끝에 진심을 마주한 시어머니와 며느리

---

## 캐릭터

### 김순자 (68세)
- 역할: 시어머니
- 성격: 완고하지만 속 깊은

### 박민지 (42세)
- 역할: 며느리
- 성격: 참을성 있지만 지친

---

## 1장: 낯선 만남

### 씬 1: 아파트 거실

**[내레이션]**
처음 만난 그날, 두 사람은 서로를 경계했다...

**[대화]**
순자: "어서 오세요..."
민지: "안녕하세요, 어머니..."

---

## 이미지 프롬프트

| 씬 | 프롬프트 |
|----|----------|
| 1-1 | Korean grandmother, modern apartment... |
...
```

### Markdown 사용 용도

1. **GitHub/GitLab**: README, Wiki
2. **노션**: 페이지 가져오기
3. **블로그**: 포스트 작성
4. **편집기**: VS Code, Obsidian

---

## 내보내기 옵션

### 전체 옵션

```bash
/drama:export \
  --project "시어머니의마음" \
  --format all \
  --include-images \
  --include-prompts \
  --output-dir "./custom-output"
```

### 옵션 설명

| 옵션 | 설명 | 기본값 |
|------|------|--------|
| `--project` | 프로젝트명 | 현재 작업 중인 프로젝트 |
| `--format` | 형식 (n8n, pdf, markdown, all) | all |
| `--include-images` | 이미지 프롬프트 포함 | true |
| `--include-prompts` | 시스템 프롬프트 포함 | false |
| `--output-dir` | 출력 디렉토리 | output/dramas/{project}/exports |

### 테스트 건너뛰기

```bash
# 테스트 없이 바로 내보내기
/drama:export --skip-test
```

---

## 출력 파일 구조

내보내기 후 생성되는 파일:

```
output/dramas/시어머니의마음/
├── story-concept.yaml
├── chapter-blueprint.yaml
├── script-full.md
├── scripts/
│   ├── chapter-1.md
│   ├── chapter-2.md
│   └── ...
├── image-prompts.yaml
└── exports/
    ├── n8n-workflow.json
    ├── 시어머니의마음.pdf
    └── 시어머니의마음.md
```

---

## 문제 해결

### n8n 워크플로우가 작동하지 않음

1. **자격 증명 확인**: 모든 API 키가 올바른지 확인
2. **노드 연결 확인**: 노드 간 연결이 끊어지지 않았는지 확인
3. **로그 확인**: n8n 실행 로그에서 오류 메시지 확인

### PDF 생성 실패

1. **의존성 설치**: wkhtmltopdf 또는 Pandoc 설치 확인
2. **한글 폰트**: Noto Sans KR 폰트 설치 확인
3. **메모리**: 대용량 대본의 경우 메모리 부족 가능

### Markdown 깨짐

1. **인코딩**: UTF-8 인코딩 확인
2. **특수문자**: 마크다운 특수문자 이스케이프 확인

---

## 내보내기 후 활용

### n8n 워크플로우 활용

1. Google Sheets에 아이디어 입력
2. n8n이 자동으로 대본 생성
3. 이미지 자동 생성
4. 결과를 다시 Sheets에 저장

### PDF 활용

- 출력하여 회의 자료로 사용
- 이메일로 공유
- 아카이브 보관

### Markdown 활용

- 노션에 가져와서 팀과 공유
- GitHub에 업로드하여 버전 관리
- 블로그에 연재
