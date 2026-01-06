# Step 3: 완료

## 목표
내보내기를 완료하고 사용 가이드를 제공합니다.

## 수행 작업

### 1. 완료 요약

```
┌──────────────────────────────────────────┐
│ 📦 내보내기 완료!                          │
├──────────────────────────────────────────┤
│ 프로젝트: {project_name}                   │
│                                          │
│ 생성된 파일:                               │
│ ✅ n8n-workflow.json (15.2 KB)           │
│ ✅ complete.pdf (2.3 MB)                 │
│ ✅ complete.md (45.6 KB)                 │
│                                          │
│ 저장 위치:                                 │
│ {output_folder}/{project_name}/exports/   │
└──────────────────────────────────────────┘
```

### 2. n8n 사용 가이드

> **n8n 워크플로우 사용 방법:**
>
> 1. n8n 웹 UI 접속
> 2. 좌측 메뉴 → Workflows → Import from File
> 3. `{project_name}-workflow.json` 선택
> 4. Credentials 설정:
>    - Google Sheets API 키
>    - OpenAI/Claude/Gemini API 키
>    - 이미지 생성 API 키
> 5. Google Sheets에 '주제' 컬럼 추가
> 6. 워크플로우 활성화
>
> 📌 **API 키 설정 위치:**
> - node "System Prompt": 그대로 사용
> - node "AI Generate": API 키 입력
> - node "Image Gen": API 키 입력

### 3. PDF 활용 가이드

> **PDF 문서 활용:**
>
> - 오프라인 검토용
> - 팀 공유용
> - 인쇄하여 리딩 세션
> - 클라이언트 프레젠테이션

### 4. Markdown 활용 가이드

> **Markdown 파일 활용:**
>
> - Git 버전 관리
> - 추가 편집 (VS Code, Obsidian 등)
> - 다른 AI 도구에 컨텍스트로 제공
> - 웹사이트/블로그 게시

### 5. 다음 작업 제안

> **다음 단계:**
>
> 1. **n8n 테스트** - 워크플로우 import 후 테스트 실행
> 2. **새 프로젝트** - 다른 드라마 스토리 시작
> 3. **프롬프트 개선** - 테스트 결과 기반 수정
>
> 명령어:
> - `/drama:agent` - 에이전트 시작
> - `/drama:story` - 새 스토리 시작
> - `/drama:test` - 프롬프트 테스트

## 워크플로우 완료

내보내기 워크플로우가 종료되었습니다.
