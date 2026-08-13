# FTD Speech Bridge

아두이노(Edge Impulse 키워드 인식) → 웹 화면으로 문장을 교정해 보여주는 정적 웹 앱.

## 동작 방식

1. 아두이노가 Edge Impulse 추론 결과(`apple`, `sleep`, `water`, `cold`, `bathroom`)를
   `Serial.println()`으로 115200 baud에 출력
2. 브라우저가 Web Serial API로 시리얼 포트를 읽음
3. 해당 키워드에 매핑된 "인식된 발화 / 교정된 문장"을 화면에 표시

## 로컬 실행

`index.html`을 그냥 열면 Web Serial API가 동작하지 않을 수 있으므로,
로컬 서버로 띄우는 것을 권장합니다.

```bash
npx serve .
```

## 브라우저 요구사항

Web Serial API는 **Chrome / Edge (데스크톱)** 에서만 지원되며,
**HTTPS 또는 localhost** 에서만 동작합니다. Safari와 Firefox는 미지원입니다.
Vercel 배포 시 HTTPS가 기본 제공되므로 이 조건은 충족됩니다.

## 배포

정적 사이트이므로 Vercel에서 별도 빌드 설정 없이 배포됩니다.
(Framework Preset: Other / Build Command: 없음 / Output Directory: 루트)

## 환경 변수

현재 코드에는 비밀 값이 없습니다. 추후 API 키가 필요해지면
`.env.example`을 참고해 Vercel 대시보드의 Environment Variables에 등록하고,
키를 직접 쓰는 로직은 `/api` 서버리스 함수 쪽에 두세요.
브라우저 번들에 들어간 값은 누구나 볼 수 있습니다.
