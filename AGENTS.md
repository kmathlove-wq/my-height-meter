# My Height Meter — AGENTS.md

## 프로젝트 개요

부모 키와 성별을 입력하면 예상 키를 계산해 보여주는 정적 HTML 프로젝트.
빌드 도구나 패키지 설치 없이 브라우저에서 바로 실행된다.

첫 화면(`index.html`)에서 두 구현을 비교 선택할 수 있다.
- `codex.html`: Codex/ChatGPT가 만든 버전
- `claude code.html`: Claude Code가 만든 버전

## 파일 구조

```
my-height-meter/
├── index.html          # 첫 선택 화면: "어떤 게 더 좋은가요?"
├── codex.html          # Codex/ChatGPT 버전 키 예측기
├── claude code.html    # Claude Code 버전 키 예측기
├── favicon-home.svg    # 첫 화면 탭 로고
├── favicon-codex.svg   # Codex 버전 탭 로고
├── favicon-claude.svg  # Claude Code 버전 탭 로고
├── CLAUDE.md           # Claude 작업 지침
└── AGENTS.md           # Codex 작업 지침
```

## 실행 방법

정적 HTML이라 파일을 브라우저에서 직접 열어도 동작한다.
로컬 서버로 확인하려면:

```bash
python3 -m http.server 8000
# http://localhost:8000
```

## 기술 스택

- 순수 HTML/CSS/JavaScript
- 외부 라이브러리 없음
- 빌드 도구 없음
- package.json 없음

## 페이지 구조

### index.html

첫 진입 페이지.
`어떤 게 더 좋은가요?`라는 질문과 두 선택 버튼을 보여준다.

링크:
- `codex.html`
- `claude%20code.html`

탭 로고:
- `favicon-home.svg`

### codex.html

일러스트형 키 예측기.
왼쪽에는 키 재는 아이와 자, 오른쪽에는 입력 폼이 있다.

주요 DOM:
- `#heightForm`: 입력 폼
- `#momHeight`: 엄마 키 입력
- `#dadHeight`: 아빠 키 입력
- `name="gender"`: 딸/아들 라디오 선택
- `#loading`: 전체 화면 로딩 모달
- `#result`: 결과 메시지
- `.back-link`: `index.html`로 돌아가기

로딩은 1.8초 뒤 결과로 전환된다.
탭 로고는 `favicon-codex.svg`를 사용한다.

### claude code.html

카드형 키 예측기.
입력 폼, 로딩 영역, 결과 영역을 한 카드 안에서 전환한다.

주요 DOM:
- `#form-section`: 입력 폼 영역
- `#mom`: 엄마 키 입력
- `#dad`: 아빠 키 입력
- `#btn-son`, `#btn-daughter`: 성별 선택 버튼
- `#loading-section`: 로딩 영역
- `#result-section`: 결과 영역
- `.back-link`: `index.html`로 돌아가기

로딩은 2.5초 뒤 결과로 전환된다.
탭 로고는 `favicon-claude.svg`를 사용한다.

## 계산 공식

사용자가 지정한 공식:

```js
base = (momHeight + dadHeight) / 2
daughter = base - 10
son = base + 10
```

결과는 소수점 한 자리까지 표시한다.

## 링크 규칙

- 모든 결과 페이지의 돌아가기 버튼은 `index.html`로 연결한다.
- `claude code.html` 파일명에는 공백이 있으므로 링크에서는 `claude%20code.html`을 사용한다.
- `index.html`은 비교 선택 화면이므로 키 계산 로직을 넣지 않는다.

## 주의사항

- 두 구현은 각각 독립된 HTML 파일이다. 공통 CSS/JS 파일이 없으므로 수정 시 각 파일 안에서 처리한다.
- 새 프레임워크, 번들러, 패키지를 추가하지 않는다.
- 파일명 `claude code.html`의 공백을 임의로 바꾸지 않는다.
- 이 앱은 재미용 계산기다. 의학적 예측처럼 표현하지 않는다.

## GitHub

저장소: `https://github.com/kmathlove-wq/my-height-meter`
브랜치: `main`

사용자가 하지 말라고 명시하지 않는 한, 코드나 문서 변경 후 GitHub에 커밋하고 푸시한다.

## 작업 규칙

### 절약 규칙
- 이미 읽은 파일은 다시 확인하지 않는다
- 불필요한 도구 호출은 하지 않는다
- 가능한 도구 호출은 동시에 실행한다
- 20줄 이상의 불필요한 출력은 서브에이전트에 위임한다
- 사용자가 이미 설명한 내용을 다시 반복하지 않는다

### 기타 규칙
- 새로 알게된 내용은 반드시 자동으로 이 파일(CLAUDE.md)에 추가한다
- 이 파일은 반드시 200줄이 넘으면 안 된다
