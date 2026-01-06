# 예시 3: n8n 연동

n8n 워크플로우를 활용한 자동화 연동 예시입니다.

## 개요

n8n을 사용하면 Google Sheets에 아이디어를 입력하는 것만으로 대본과 이미지를 자동 생성할 수 있습니다.

---

## 전체 흐름

```
Google Sheets     →     n8n     →     Claude API     →     이미지 생성
(아이디어 입력)        (자동화)       (대본 생성)         (Replicate)
                                           ↓
                                    Google Sheets
                                    (결과 저장)
```

---

## Step 1: 워크플로우 내보내기

### 실행

```
사용자: /drama:export --format n8n
```

```
미영: n8n 워크플로우를 생성할게요.

      프로젝트: 시어머니의마음

      생성 중...

      ✓ n8n-workflow.json 생성 완료

      파일 위치:
      output/dramas/시어머니의마음/exports/n8n-workflow.json

      이 파일을 n8n에 가져오시면 됩니다.
```

---

## Step 2: Google Sheets 준비

### 스프레드시트 생성

Google Sheets에서 새 스프레드시트를 만들고 다음 구조로 설정:

| A | B | C | D | E | F | G |
|---|---|---|---|---|---|---|
| ID | 프로젝트명 | 원라인 | 테마 | 상태 | 대본 | 이미지URL |
| 1 | 시어머니의마음 | 30년 갈등 끝에 화해 | reconciliation | pending | | |
| 2 | 손녀의선물 | 할머니와 손녀의 여름 | generational-love | pending | | |

### 열 설명

| 열 | 내용 | 입력 방식 |
|----|------|----------|
| A: ID | 고유 번호 | 자동 |
| B: 프로젝트명 | 드라마 제목 | 수동 입력 |
| C: 원라인 | 한 줄 스토리 | 수동 입력 |
| D: 테마 | 4가지 중 선택 | 수동 선택 |
| E: 상태 | pending/processing/done | 자동 |
| F: 대본 | 생성된 대본 | 자동 |
| G: 이미지URL | 생성된 이미지 | 자동 |

---

## Step 3: n8n 설정

### 3.1 n8n 설치 및 실행

```bash
# Docker로 실행
docker run -it --rm \
  --name n8n \
  -p 5678:5678 \
  -v ~/.n8n:/home/node/.n8n \
  n8nio/n8n

# 브라우저에서 접속
# http://localhost:5678
```

### 3.2 워크플로우 가져오기

1. n8n 대시보드 접속
2. "Workflows" → "Import from File" 클릭
3. `n8n-workflow.json` 파일 선택
4. "Import" 클릭

### 3.3 자격 증명 설정

#### Google Sheets

1. "Credentials" → "Add Credential"
2. "Google Sheets API" 선택
3. OAuth2로 인증
4. 스프레드시트 접근 권한 허용

#### Claude API

1. "Credentials" → "Add Credential"
2. "Header Auth" 선택
3. 설정:
   - Name: `x-api-key`
   - Value: `sk-ant-...` (Anthropic API 키)

#### Replicate API (이미지 생성용)

1. "Credentials" → "Add Credential"
2. "Header Auth" 선택
3. 설정:
   - Name: `Authorization`
   - Value: `Token r8_...` (Replicate API 토큰)

### 3.4 노드 연결 확인

워크플로우 에디터에서 모든 노드가 연결되어 있는지 확인:

```
┌──────────────────┐
│ Google Sheets    │
│ Trigger          │───┐
└──────────────────┘   │
                       ▼
┌──────────────────┐
│ Set Status:      │
│ "processing"     │───┐
└──────────────────┘   │
                       ▼
┌──────────────────┐
│ Claude API       │
│ (Script Gen)     │───┐
└──────────────────┘   │
                       ▼
┌──────────────────┐
│ Replicate API    │
│ (Image Gen)      │───┐
└──────────────────┘   │
                       ▼
┌──────────────────┐
│ Google Sheets    │
│ Update           │
└──────────────────┘
```

---

## Step 4: 워크플로우 실행

### 4.1 워크플로우 활성화

1. 워크플로우 에디터에서 "Active" 토글 켜기
2. 또는 "Execute Workflow" 버튼으로 수동 실행

### 4.2 Google Sheets에 입력

스프레드시트에 새 행 추가:

| A | B | C | D | E |
|---|---|---|---|---|
| 3 | 어머니의봄 | 치매 어머니와의 마지막 봄 | sacrifice | pending |

### 4.3 자동 실행

1. n8n이 새 행 감지
2. 상태가 "processing"으로 변경
3. Claude API로 대본 생성
4. Replicate로 이미지 생성
5. 결과가 스프레드시트에 저장
6. 상태가 "done"으로 변경

---

## Step 5: 결과 확인

### Google Sheets 결과

| A | B | C | D | E | F | G |
|---|---|---|---|---|---|---|
| 3 | 어머니의봄 | 치매 어머니와... | sacrifice | done | [대본 내용] | https://... |

### 생성된 대본 (F열)

```markdown
# 1장: 평범한 일상

**[내레이션]**
봄이 왔다. 어머니는 창밖의 벚꽃을 바라보며
또 그 이름을 물었다...
```

### 생성된 이미지 (G열)

이미지 URL이 저장됨:
`https://replicate.delivery/...`

---

## 고급 설정

### 배치 처리

여러 행을 한 번에 처리:

```json
{
  "name": "Batch Process",
  "type": "n8n-nodes-base.splitInBatches",
  "parameters": {
    "batchSize": 5
  }
}
```

### 오류 처리

실패 시 재시도:

```json
{
  "name": "Error Handler",
  "type": "n8n-nodes-base.errorTrigger",
  "parameters": {
    "retries": 3,
    "waitBetweenTries": 5000
  }
}
```

### 알림 설정

완료 시 Slack 알림:

```json
{
  "name": "Slack Notification",
  "type": "n8n-nodes-base.slack",
  "parameters": {
    "channel": "#drama-production",
    "text": "새 드라마 대본이 생성되었습니다: {{$json.project_name}}"
  }
}
```

---

## 문제 해결

### Google Sheets 권한 오류

```
Error: The caller does not have permission
```

해결:
1. OAuth2 재인증
2. 스프레드시트 공유 설정 확인

### Claude API 오류

```
Error: 401 Unauthorized
```

해결:
1. API 키 확인
2. anthropic-version 헤더 확인: `2023-06-01`

### 이미지 생성 실패

```
Error: Model not found
```

해결:
1. Replicate 모델 ID 확인
2. API 토큰 유효성 확인

---

## 비용 예상

| 서비스 | 단가 | 드라마 1편당 |
|--------|------|-------------|
| Claude API | $3/1M tokens | ~$0.50 |
| Replicate | ~$0.01/이미지 | ~$0.80 (80장) |
| **총합** | | **~$1.30** |

---

## 팁

1. **테스트 먼저**: 실제 실행 전 "Execute Node"로 개별 노드 테스트
2. **로그 확인**: 실행 기록에서 상세 로그 확인
3. **백업**: 중요 데이터는 별도 백업
4. **요금 모니터링**: API 사용량 정기 확인
