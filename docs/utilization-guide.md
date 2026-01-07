# 시니어 드라마 활용 완전 가이드

Senior Dramas로 생성된 드라마 output을 실제 YouTube 콘텐츠로 활용하는 종합 가이드입니다.

---

## 목차

1. [산출물 이해](#part-1-산출물-이해)
2. [내보내기 상세 가이드](#part-2-내보내기-상세-가이드)
3. [이미지 생성 완전 가이드](#part-3-이미지-생성-완전-가이드)
4. [TTS 음성 생성 가이드](#part-4-tts-음성-생성-가이드)
5. [YouTube 영상 제작 가이드](#part-5-youtube-영상-제작-가이드)
6. [n8n 자동화 파이프라인](#part-6-n8n-자동화-파이프라인)
7. [비용 분석](#part-7-비용-분석)
8. [실전 체크리스트](#part-8-실전-체크리스트)
9. [FAQ & 문제 해결](#part-9-faq--문제-해결)

---

## Part 1: 산출물 이해

### 1.1 Output 폴더 구조

```
output/dramas/{project-name}/
├── story-concept.yaml       # 스토리 컨셉 (테마, 주인공, 갈등)
├── blueprint.yaml           # 8챕터 청사진 (감정 아크, 후킹 포인트)
├── characters.json          # 5명 캐릭터 프로필
├── scripts/
│   ├── chapter-1.md         # 챕터별 대본
│   ├── chapter-2.md
│   └── ... (8개)
├── image-prompts/
│   └── all-prompts.md       # 24개 이미지 프롬프트 (한글/영문)
├── validation-report.md     # 검증 보고서
└── exports/                 # 내보내기 파일
    ├── n8n-workflow.json
    ├── {project}.pdf
    └── {project}.md
```

### 1.2 각 파일의 역할

| 파일 | 용도 | 활용 시점 |
|------|------|----------|
| story-concept.yaml | 스토리 전체 개요 | 기획 검토, 수정 |
| blueprint.yaml | 챕터별 구조 | 대본 수정 전 참고 |
| characters.json | 캐릭터 설정 | 이미지 생성 시 참고 |
| scripts/*.md | 실제 대본 텍스트 | TTS, 영상 제작 |
| image-prompts/*.md | 이미지 생성용 프롬프트 | 이미지 AI에 입력 |
| validation-report.md | 품질 검증 결과 | 수정 필요 여부 판단 |

### 1.3 검증 보고서 해석

```markdown
## 최종 점수: 92.45/100

| 등급 | 점수 범위 | 판정 |
|------|----------|------|
| A    | 90-100   | 우수 - 바로 제작 가능 |
| B    | 80-89    | 양호 - 소규모 수정 후 제작 |
| C    | 75-79    | 합격 - 일부 수정 권장 |
| F    | 75 미만   | 불합격 - 재생성 필요 |
```

**단계별 가중치**:
- 1단계 (스토리 컨셉): 15%
- 2단계 (청사진): 20%
- 3단계 (대본): 35% ← 가장 중요
- 4단계 (이미지 프롬프트): 15%
- 5단계 (통합): 15%

---

## Part 2: 내보내기 상세 가이드

### 2.1 기본 명령어

```bash
# 모든 형식으로 내보내기
/drama:export

# 특정 형식만 내보내기
/drama:export --format n8n
/drama:export --format pdf
/drama:export --format markdown

# 특정 프로젝트 내보내기
/drama:export --project "test-drama-40years"
```

### 2.2 n8n JSON 형식

**용도**: 자동화 워크플로우용

**출력 위치**: `exports/n8n-workflow.json`

**포함 내용**:
- Google Sheets 트리거 노드
- Claude API 대본 생성 노드
- 이미지 생성 API 노드
- 결과 저장 노드

### 2.3 PDF 형식

**용도**: 인쇄, 오프라인 검토, 팀 공유

**출력 위치**: `exports/{project}.pdf`

**PDF 구성**:
1. 표지 (제목, 원라인)
2. 목차
3. 캐릭터 소개
4. 8개 챕터 대본
5. 이미지 프롬프트 목록

**의존성 설치** (PDF 생성 시 필요):

```bash
# macOS
brew install wkhtmltopdf

# 또는 Pandoc + LaTeX
brew install pandoc
brew install --cask mactex

# Ubuntu/Debian
apt install wkhtmltopdf
```

### 2.4 Markdown 형식

**용도**: 편집, 노션/블로그 게시, Git 버전 관리

**출력 위치**: `exports/{project}.md`

**노션 연동**:
1. 노션에서 "Import" 클릭
2. "Markdown" 선택
3. `{project}.md` 파일 업로드
4. 자동 변환 완료

**블로그 연동**:
- Velog: Markdown 직접 붙여넣기
- 티스토리: HTML 변환 후 게시
- GitHub Pages: Jekyll/Hugo 연동

---

## Part 3: 이미지 생성 완전 가이드

### 3.1 수동 생성 방법

#### Midjourney (Discord)

**장점**: 최고 품질, 스타일 일관성
**비용**: $10-30/월 구독

**사용법**:
1. Discord Midjourney 서버 접속
2. `/imagine prompt:` 입력
3. 영문 프롬프트 붙여넣기
4. 생성된 4개 중 선택 (U1-U4)
5. 업스케일 후 다운로드

**권장 설정**:
```
/settings
Stylize: Medium (100)
Chaos: 0 (일관성 우선)
Version: 6.1
```

#### DALL-E 3 (ChatGPT Plus)

**장점**: 사용 편의성, 한글 지원
**비용**: $20/월 (ChatGPT Plus)

**사용법**:
1. ChatGPT에서 "이미지 생성" 선택
2. 영문 프롬프트 입력
3. 생성된 이미지 다운로드

**권장 설정**: 1024x1024, vivid style

#### DALL-E 3 API

**장점**: 자동화 가능
**비용**: $0.04/이미지 (1024x1024)

**API 호출 예시**:
```python
import openai

response = openai.images.generate(
    model="dall-e-3",
    prompt="Korean grandmother, 65 years old, warm smile...",
    size="1024x1024",
    quality="standard",
    n=1
)
image_url = response.data[0].url
```

#### Gemini Imagen (무료)

**장점**: 무료 사용 가능
**비용**: 무료 (API 제한 내)

**사용법**:
1. Google AI Studio 접속
2. "Create image" 선택
3. 프롬프트 입력
4. 다운로드

#### Stable Diffusion (로컬)

**장점**: 무료, 무제한, 커스터마이징
**비용**: 무료 (GPU 필요)

**설치**:
```bash
# AUTOMATIC1111 WebUI
git clone https://github.com/AUTOMATIC1111/stable-diffusion-webui
cd stable-diffusion-webui
./webui.sh
```

**권장 모델**: Realistic Vision v5.1, PhotoReal

#### Leonardo AI

**장점**: 웹 기반, 스타일 다양
**비용**: 무료 150크레딧/일

**권장 설정**:
- Model: Leonardo Diffusion XL
- Style: Cinematic
- Resolution: 1024x1024

### 3.2 자동 생성 방법

#### n8n + Replicate API

**비용**: ~$0.01/이미지

**워크플로우**:
```
이미지 프롬프트 파싱
    ↓
Loop Node (24회 반복)
    ↓
Replicate API 호출
    ↓
이미지 URL 수집
    ↓
Google Drive 저장
```

**Replicate 모델 추천**:
- `stability-ai/sdxl`: 고품질, $0.0023/이미지
- `black-forest-labs/flux-schnell`: 빠른 생성

#### n8n + DALL-E API

**비용**: $0.04/이미지

```json
{
  "name": "DALL-E Generator",
  "type": "n8n-nodes-base.httpRequest",
  "parameters": {
    "url": "https://api.openai.com/v1/images/generations",
    "method": "POST",
    "headers": {
      "Authorization": "Bearer {{$credentials.openAiApi.apiKey}}"
    },
    "body": {
      "model": "dall-e-3",
      "prompt": "{{$json.prompt}}",
      "size": "1024x1024"
    }
  }
}
```

### 3.3 이미지 스타일 권장 설정

**해상도**:
| 용도 | 권장 해상도 |
|------|------------|
| YouTube 영상 | 1920x1080 (16:9) |
| YouTube 썸네일 | 1280x720 |
| 인스타그램 | 1080x1080 (1:1) |

**스타일 일관성 유지 팁**:

1. **동일 시드값 사용** (Stable Diffusion):
   ```
   --seed 12345
   ```

2. **캐릭터 일관성 프롬프트**:
   ```
   same character as before, consistent appearance,
   Korean grandmother with short gray hair,
   round face, warm brown eyes
   ```

3. **스타일 레퍼런스 추가**:
   ```
   cinematic lighting, soft focus,
   warm color palette, 35mm film look
   ```

---

## Part 4: TTS 음성 생성 가이드

### 4.1 한국어 TTS 서비스

#### 네이버 클로바 보이스

**장점**: 자연스러운 한국어, 다양한 음성
**비용**: 4원/글자 (약 30분 = ~$3)

**권장 음성**:
- 여성 내레이션: `nara` (나라)
- 여성 감정적: `nsejong` (세종)
- 남성 내레이션: `nwontak` (원탁)

**API 사용**:
```python
import urllib.request

text = "40년 만에 돌아온 고향집..."
data = f"speaker=nara&text={text}&speed=0&pitch=0"
request = urllib.request.Request(CLOVA_URL)
request.add_header("X-NCP-APIGW-API-KEY-ID", CLIENT_ID)
request.add_header("X-NCP-APIGW-API-KEY", CLIENT_SECRET)
```

#### TypeCast (AI 성우)

**장점**: 감정 표현, 전문 성우 음질
**비용**: 월 $29~

**권장 성우**:
- 시니어 여성: "해리 할머니"
- 시니어 남성: "영수 할아버지"

#### ElevenLabs

**장점**: 음성 복제, 다국어
**비용**: $0.30/1,000자

**사용법**:
1. Voice Lab에서 음성 생성/복제
2. Speech Synthesis에서 텍스트 입력
3. MP3 다운로드

### 4.2 무료 TTS 옵션

#### Google TTS (gTTS)

```python
from gtts import gTTS

text = "40년 만에 돌아온 고향집..."
tts = gTTS(text=text, lang='ko', slow=False)
tts.save("chapter1.mp3")
```

#### macOS Say 명령어

```bash
say -v Yuna "40년 만에 돌아온 고향집..." -o chapter1.aiff
```

#### Microsoft Edge TTS (edge-tts)

```bash
pip install edge-tts
edge-tts --voice ko-KR-SunHiNeural --text "텍스트" --write-media output.mp3
```

**권장 음성**:
- `ko-KR-SunHiNeural`: 여성, 따뜻함
- `ko-KR-InJoonNeural`: 남성, 차분함

### 4.3 TTS 설정 권장값

**시니어 타겟 설정**:
| 설정 | 권장값 | 이유 |
|------|--------|------|
| 속도 | 0.9x | 천천히, 명확하게 |
| 피치 | 0 (기본) | 자연스러움 유지 |
| 볼륨 | 1.0 | 명확한 청취 |

**챕터별 파일 분할**:
```
audio/
├── chapter-1.mp3
├── chapter-2.mp3
├── ...
└── chapter-8.mp3
```

**BGM 믹싱 팁**:
- BGM 볼륨: TTS의 20-30%
- 감정적 장면에서 BGM 페이드 인
- 클라이맥스에서 BGM 볼륨 업

---

## Part 5: YouTube 영상 제작 가이드

### 5.1 영상 편집 도구

#### CapCut (무료, 권장)

**장점**: 무료, 자동 자막, 쉬운 사용
**다운로드**: https://www.capcut.com

**기본 워크플로우**:
1. 이미지 24개 임포트
2. 타임라인에 순서대로 배치
3. 각 이미지 표시 시간 조절 (4-8초)
4. TTS 음성 트랙 추가
5. 음성에 맞춰 이미지 타이밍 조절
6. 자막 자동 생성
7. BGM 추가
8. 내보내기

#### Adobe Premiere Pro

**장점**: 전문가급 편집
**비용**: 월 $22.99

#### DaVinci Resolve (무료)

**장점**: 무료, 전문 기능
**권장 대상**: 중급자 이상

#### Final Cut Pro

**장점**: macOS 최적화
**비용**: $299 (1회 구매)

### 5.2 영상 구조 템플릿

```
[00:00-00:30] 후킹 씬
    - 가장 감동적인 장면으로 시작
    - "40년 만에 어머니 앞에 섰습니다..."

[00:30-01:00] 오프닝
    - 제목 텍스트 오버레이
    - 원라인 소개

[01:00-08:00] Chapter 1-2
    - 시작 단계, 일상과 갈등 발단

[08:00-15:00] Chapter 3-4
    - 갈등 심화, 과거 회상

[15:00-16:00] 미드포인트 반전
    - 핵심 진실 발견
    - BGM 클라이맥스

[16:00-24:00] Chapter 5-6
    - 위기, 감정적 최고점

[24:00-28:00] Chapter 7-8
    - 화해, 해결

[28:00-30:00] 클로징
    - 여운 있는 마무리
    - 구독/좋아요 유도
    - 다음 영상 예고
```

### 5.3 YouTube 최적화

#### 제목 작성 전략

**CTR 높은 제목 패턴**:
```
1. [감정 + 시간] "40년 만에 어머니를 만났습니다"
2. [비밀/진실] "어머니의 일기장에서 발견한 충격적인 진실"
3. [숫자] "60년 만에 알게 된 3가지 비밀"
4. [질문] "왜 어머니는 나만 보냈을까?"
```

**권장 길이**: 30-40자 (한글 기준)

#### 썸네일 제작 가이드

**필수 요소**:
1. 감정적인 얼굴 클로즈업
2. 텍스트 3-5단어
3. 대비 높은 색상
4. 1280x720 해상도

**권장 도구**:
- Canva (무료)
- Adobe Express
- Photoshop

#### 설명란 템플릿

```markdown
[드라마 제목]

"원라인 스토리 요약"

이 영상에서는...
- 포인트 1
- 포인트 2
- 포인트 3

#시니어드라마 #감동스토리 #가족

---
타임스탬프:
00:00 프롤로그
01:00 Chapter 1
...

---
배경음악:
[곡명] by [아티스트] (무료 사용 가능)
```

#### 태그 추천

```
시니어드라마, 가족드라마, 감동스토리, 어머니,
화해, 용서, 치매, 가족관계, 50대이상, 시니어콘텐츠,
Korean drama, family story, emotional
```

### 5.4 수익화 조건

**YouTube 파트너 프로그램 기준**:
- 구독자 1,000명 이상
- 12개월 내 시청 시간 4,000시간
- 또는 Shorts 조회수 1,000만회

**AI 콘텐츠 정책**:
- AI 생성 표시 필요 (2024년 정책)
- 설명란에 "AI-generated content" 명시 권장
- 오리지널 스토리이므로 저작권 문제 없음

**저작권 주의사항**:
- BGM: 저작권 프리 음악 사용
- 이미지: AI 생성 이미지 = 저작권 프리
- 음성: TTS 서비스 이용약관 확인

---

## Part 6: n8n 자동화 파이프라인

### 6.1 n8n 설치

#### Docker 설치 (권장)

```bash
docker run -d \
  --name n8n \
  -p 5678:5678 \
  -v ~/.n8n:/home/node/.n8n \
  n8nio/n8n
```

브라우저에서 `http://localhost:5678` 접속

#### npm 설치

```bash
npm install n8n -g
n8n start
```

#### 클라우드 호스팅

- **n8n.cloud**: $20/월~
- **Railway**: $5/월~
- **Render**: 무료 티어 가능

### 6.2 워크플로우 구성

```
┌─────────────────────┐
│ Google Sheets       │ ← 아이디어 입력
│ Trigger (5분 간격)   │
└──────────┬──────────┘
           ↓
┌─────────────────────┐
│ Filter Node         │ ← status = "pending"
│ (대기 중인 항목만)    │
└──────────┬──────────┘
           ↓
┌─────────────────────┐
│ Set Status          │ ← "processing"
│ "processing"        │
└──────────┬──────────┘
           ↓
┌─────────────────────┐
│ Claude API          │ ← 대본 생성
│ HTTP Request        │
└──────────┬──────────┘
           ↓
┌─────────────────────┐
│ Extract Prompts     │ ← 이미지 프롬프트 추출
│ Code Node (JS)      │
└──────────┬──────────┘
           ↓
┌─────────────────────┐
│ Loop Over Items     │ ← 24개 반복
│ Split In Batches    │
└──────────┬──────────┘
           ↓
┌─────────────────────┐
│ Image Generator     │ ← Replicate/DALL-E
│ HTTP Request        │
└──────────┬──────────┘
           ↓
┌─────────────────────┐
│ Google Drive        │ ← 이미지 저장
│ Upload              │
└──────────┬──────────┘
           ↓
┌─────────────────────┐
│ Google Sheets       │ ← status = "done"
│ Update Row          │
└──────────┬──────────┘
           ↓
┌─────────────────────┐
│ Slack Notification  │ ← 완료 알림
│ (선택)               │
└─────────────────────┘
```

### 6.3 API 설정 상세

#### Claude API 키 발급

1. https://console.anthropic.com 접속
2. API Keys 메뉴
3. "Create Key" 클릭
4. 키 복사 (sk-ant-...)

**n8n 설정**:
```
Credentials → Add Credential → Header Auth
Name: x-api-key
Value: sk-ant-api03-...
```

#### Replicate API 설정

1. https://replicate.com 접속
2. Account Settings → API tokens
3. 토큰 생성

**n8n 설정**:
```
Credentials → Add Credential → Header Auth
Name: Authorization
Value: Token r8_...
```

#### Google Sheets OAuth 설정

1. Google Cloud Console 접속
2. 새 프로젝트 생성
3. APIs & Services → Credentials
4. OAuth 2.0 Client ID 생성
5. n8n에서 OAuth 인증

### 6.4 에러 핸들링

**재시도 로직**:
```json
{
  "name": "Retry Handler",
  "type": "n8n-nodes-base.errorTrigger",
  "parameters": {
    "retries": 3,
    "waitBetweenTries": 10000
  }
}
```

**실패 알림**:
```json
{
  "name": "Error Notification",
  "type": "n8n-nodes-base.slack",
  "parameters": {
    "channel": "#drama-errors",
    "text": "드라마 생성 실패: {{$json.error}}"
  }
}
```

---

## Part 7: 비용 분석

### 7.1 이미지 생성 비용

| 서비스 | 단가 | 24개 비용 | 품질 |
|--------|------|----------|------|
| DALL-E 3 | $0.04 | $0.96 | 최상 |
| Midjourney | $30/월 | ~$2 | 최상 |
| Replicate SDXL | $0.0023 | $0.06 | 상 |
| Gemini Imagen | 무료 | $0 | 중상 |
| Stable Diffusion | 무료 | $0 | 상 (로컬) |

### 7.2 TTS 비용

| 서비스 | 단가 | 30분 비용 | 품질 |
|--------|------|----------|------|
| 네이버 클로바 | 4원/자 | ~$3 | 최상 |
| TypeCast | $29/월 | ~$4 | 최상 |
| ElevenLabs | $0.30/1k자 | ~$2 | 상 |
| Edge TTS | 무료 | $0 | 중상 |
| gTTS | 무료 | $0 | 중 |

### 7.3 대본 생성 비용

| 서비스 | 단가 | 드라마 1편 | 비고 |
|--------|------|-----------|------|
| Claude API | $15/1M tokens | ~$0.50 | Opus |
| Claude API | $3/1M tokens | ~$0.10 | Sonnet |
| GPT-4o | $5/1M tokens | ~$0.20 | |

### 7.4 총 비용 예상

| 옵션 | 이미지 | TTS | 대본 | 총합 |
|------|--------|-----|------|------|
| 최저 비용 | $0 (무료) | $0 (무료) | $0.10 | **~$0.10** |
| 권장 품질 | $0.96 | $2 | $0.50 | **~$3.50** |
| 최고 품질 | $2 | $4 | $0.50 | **~$6.50** |

---

## Part 8: 실전 체크리스트

### 8.1 제작 전 체크리스트

- [ ] 드라마 output 검증 완료 (75점 이상)
- [ ] story-concept.yaml 검토
- [ ] blueprint.yaml 검토 (8챕터 구조)
- [ ] characters.json 검토 (5명 캐릭터)
- [ ] 이미지 프롬프트 24개 확인
- [ ] 대본 8챕터 확인
- [ ] YouTube 메타데이터 준비 (제목/설명/태그)

### 8.2 이미지 생성 체크리스트

- [ ] 스타일 일관성 확인
- [ ] 캐릭터 외모 일치 확인
- [ ] 해상도 1024x1024 이상
- [ ] 파일명 정리 (ch1-scene1.png 형식)
- [ ] 24개 모두 생성 완료
- [ ] 감정 표현 적절성 확인

### 8.3 TTS 생성 체크리스트

- [ ] TTS 서비스 선택
- [ ] 음성 스타일 선택 (따뜻한/차분한)
- [ ] 속도 설정 (0.9x 권장)
- [ ] 챕터별 8개 파일 생성
- [ ] 발음/억양 검토
- [ ] 전체 길이 확인 (25-35분 권장)

### 8.4 영상 편집 체크리스트

- [ ] 이미지-음성 싱크 확인
- [ ] 자막 추가 및 검토
- [ ] BGM 추가 (저작권 프리)
- [ ] 후킹 씬 배치 (0:00-0:30)
- [ ] 트랜지션 효과 적용
- [ ] 최종 프리뷰 확인
- [ ] 1080p 이상으로 내보내기

### 8.5 업로드 체크리스트

- [ ] 제목 최적화 (30-40자)
- [ ] 썸네일 제작 (1280x720)
- [ ] 설명란 작성
- [ ] 태그 추가 (10-15개)
- [ ] 챕터 마커 설정
- [ ] 카테고리 선택 (Entertainment/Education)
- [ ] 공개 설정 (공개/예약/비공개)

---

## Part 9: FAQ & 문제 해결

### Q: 이미지 스타일이 일관되지 않아요

**해결책**:
1. 동일 모델/서비스 사용
2. 프롬프트에 스타일 키워드 고정:
   ```
   cinematic, soft lighting, warm tones,
   Korean family drama aesthetic
   ```
3. 시드값 고정 (가능한 경우)
4. 캐릭터 외모 상세 기술

### Q: TTS 음성이 어색해요

**해결책**:
1. 더 자연스러운 TTS 서비스 사용 (TypeCast, 클로바)
2. 속도를 0.9x로 낮춤
3. 문장 부호로 호흡 조절
4. 긴 문장을 짧게 분할

### Q: n8n 워크플로우가 실패해요

**해결책**:
1. API 키 유효성 확인
2. 노드 연결 상태 확인
3. 실행 로그에서 에러 메시지 확인
4. 재시도 로직 추가
5. 배치 크기 줄이기 (5개씩)

### Q: YouTube에서 AI 콘텐츠 경고가 떠요

**해결책**:
1. 설명란에 "AI-assisted content" 명시
2. 오리지널 스토리임을 강조
3. "Altered or synthetic media" 설정 확인

### Q: 저작권 문제가 걱정돼요

**안심 요소**:
- 스토리: AI 생성 오리지널 = 저작권 프리
- 이미지: AI 생성 = 저작권 프리 (대부분 서비스)
- BGM: 저작권 프리 음악 사용 시 문제 없음
- TTS: 서비스 이용약관에 따름 (대부분 상업 사용 가능)

**주의점**:
- 실제 인물 이미지 생성 금지
- 상표권 있는 로고/캐릭터 사용 금지
- BGM 저작권 확인 필수

### Q: 영상 길이가 너무 길어요

**해결책**:
1. 이미지 표시 시간 단축 (4초 → 3초)
2. 내레이션 속도 조절 (1.0x → 1.1x)
3. 챕터 일부 요약/축소
4. 장편 시리즈로 분할 (전편/후편)

### Q: 조회수가 안 나와요

**해결책**:
1. 썸네일 CTR 개선 (감정적 이미지)
2. 제목 최적화 (숫자, 감정 키워드)
3. 첫 30초 후킹 강화
4. 업로드 시간 최적화 (저녁 7-9시)
5. Shorts 클립으로 홍보

---

## 관련 문서

- [내보내기 가이드](./export.md)
- [n8n 연동 예시](./examples/n8n-integration.md)
- [전체 워크플로우 예시](./examples/full-workflow.md)
- [명령어 레퍼런스](./commands.md)

---

*마지막 업데이트: 2026-01-07*
