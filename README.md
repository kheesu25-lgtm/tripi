# 트리피 (Tripi) — 여행 계획 챗봇 프로토타입

트리피는 여행 계획을 대화로 정리하고, 일정을 편집하며, 외부 여행 상품 검색으로 이어지도록 설계한 프로토타입입니다. 이 저장소의 ZIP 프로젝트는 Node.js 서버와 Groq API를 사용하는 챗봇 구현을 포함합니다. 별도로 관리되는 HTML 미리보기에는 Trip.com 검색 폼이 포함되어 있습니다.

## 주요 기능

- Groq API 기반 한국어 멀티턴 여행 질의응답
- 여행지, 날짜, 인원, 예산 등 여행 조건 정리
- 일차별 일정 확인
- 일정 추가·수정·삭제
- 일정표 TXT 내보내기
- 모바일 반응형 UI
- 서버에서 API 키를 읽어 브라우저 코드에 노출하지 않는 구조

## Trip.com 검색 폼

HTML 미리보기의 검색 폼은 검색 종류에 따라 입력 항목을 바꿉니다.

- **숙소:** 숙소 여행지 입력
- **항공권:** 출발지와 도착지 입력
- **기차:** 출발역/도시와 도착역/도시 입력
- 날짜 입력 및 시작일·종료일 검증
- 입력 조건을 바탕으로 Trip.com의 해당 검색 페이지 열기

> **연동 범위:** 현재 폼은 Trip.com 검색 페이지로 이동하는 프로토타입입니다. Trip.com의 실시간 상품 API나 예약 시스템과 직접 연결되어 있지 않으며, URL 파라미터가 검색 조건을 자동으로 채워 주는 것도 보장되지 않습니다. 실제 상품 가격·재고·예약 가능 여부를 조회하려면 공식 API 또는 제휴 검색 도구가 별도로 필요합니다.

## 준비물

- Node.js 18 이상
- Groq API key: https://console.groq.com/keys

## Windows에서 실행하기

1. ZIP 파일을 압축 해제합니다.
2. 압축을 푼 `tripi-travel-chatbot` 폴더에서 터미널(Windows Terminal 또는 VS Code Terminal)을 엽니다.
3. 의존성을 설치하고 환경 변수 파일을 만듭니다.

```powershell
npm install
Copy-Item .env.example .env
```

4. `.env` 파일에 본인의 Groq API 키를 입력합니다.

```env
GROQ_API_KEY=gsk_여기에_발급받은_키_입력
GROQ_MODEL=llama-3.3-70b-versatile
PORT=3000
```

5. 서버를 실행합니다.

```powershell
npm start
```

6. 브라우저에서 http://localhost:3000 을 엽니다.

## API 키 안전 수칙

- API 키를 `public/app.js`, `public/index.html` 또는 채팅창에 붙여넣지 마세요.
- 실제 `.env` 파일을 GitHub 등 공개 저장소에 올리지 마세요. `.env.example`만 공유하세요.
- API 키가 노출되었다면 Groq 콘솔에서 해당 키를 폐기하고 새 키를 발급하세요.
- 공개 배포 시 HTTPS, 접근 제한, 사용량 제한 및 속도 제한을 고려하세요.
- 개인 API 키를 제한 없이 다수의 공개 사용자와 공유하지 마세요.

## 배포 안내

이 ZIP 프로젝트는 `server.js`를 실행할 수 있는 Node.js 호스팅 환경이 필요합니다. 배포 환경의 서버 환경 변수 설정에 `GROQ_API_KEY`를 등록하세요. 정적 HTML만 호스팅하면 서버 기반 Groq 챗봇은 동작하지 않습니다.

HTML 미리보기의 Trip.com 이동 기능은 외부 검색 페이지를 여는 방식이며, 예약이나 결제를 대신 수행하지 않습니다. 공식 제휴 검색 도구를 사용하는 경우 제공 업체의 이용 조건과 생성된 코드를 따르세요.

## 참고 링크

- Groq API 키: https://console.groq.com/keys
- Groq Quickstart: https://console.groq.com/docs/quickstart
- Groq 보안 안내: https://console.groq.com/docs/production-readiness/security-onboarding
- Trip.com 제휴 도구: https://kr.trip.com/partners/tools
