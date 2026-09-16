# B1-1 web-portfolio — 구현 명세

> 나를 소개하는 웹페이지 처음부터 만들기

| 항목 | 값 |
|---|---|
| 폴더 | `b1-1-web-portfolio` |
| **과제번호** | **B1-1** (가변 — 개편 시 이 줄과 `INDEX.md`만 고친다) |
| 단계 | 1단계 · AI/SW 기초 |
| 구분 | 웹 기초와 프론트엔드 |
| 학습시간 | 80시간 · 필수 |
| 원문 | `source/assignment.md` |
| 제출 repo | https://github.com/codewhite7777/codyssey-b1-portfolio / 브랜치 `main` |
| 배포 URL | https://codewhite7777.github.io/codyssey-b1-portfolio/ — **하위 경로 배포이므로 자산은 전부 상대경로** |
| 상태 | **구현 완료 · 검증 중** |

---

## 1. 미션 한 줄 정의

라이브러리 없이 HTML/CSS/JS만으로 반응형 포트폴리오를 만들되,
**평가 대상은 화면의 완성도가 아니라 "이벤트 → 상태 변경 → DOM 렌더링" 흐름을 설명할 수 있는가**이다.
(원문 §7: "UI 고퀄리티보다 이벤트 → 상태 → 렌더링 흐름 이해 우선")

## 2. 최종 산출물

- [ ] GitHub 저장소 URL
- [ ] GitHub Pages 배포 URL (외부 접속 가능)
- [ ] 스크린샷 3종: 데스크톱 / 모바일 / 다크모드
- [ ] README (프로젝트 설명 · 사용 기술 · 배포 URL · 스크린샷 · **임계값 3개 명시**)

## 3. 제약 사항 (절대 조건 — 위반 시 구현 무효)

| # | 제약 | 검증 |
|---|---|---|
| 금지 1 | React·Vue·jQuery·Bootstrap·Tailwind 등 **외부 라이브러리 사용 금지** | V-1 |
| 금지 2 | `var` 사용 금지 (`const`/`let`만) | V-3 |
| 금지 3 | HTML `onclick` 속성 금지 (`addEventListener`만) | V-4 |
| 금지 4 | 인라인 스타일 `style="..."` 금지 | V-5 |
| 허용 | Font Awesome(아이콘), Google Fonts(웹폰트) | — |
| 환경 | 최신 Chrome에서 정상 동작 / VS Code + Live Server 개발 | V-2 |

> 주의: 금지 1은 CDN `<script>`·`<link>` 한 줄로도 위반된다. Font Awesome·Google Fonts 외의
> 외부 링크가 하나라도 있으면 그 자리에서 탈락 요인이다.

---

## 4. 기능 요구사항 (R) — 이 표가 곧 추적 매트릭스

`구현 위치`는 코드 작성 시 `파일:라인`으로 채운다. 코드에는 `[R-n]` 앵커를 남긴다 (SPEC §4).

### A. 프로젝트 기본 구성

| R-ID | 요구사항 | 구현 위치 | V | C | E |
|---|---|---|---|---|---|
| R-1 | `index.html` / `css/` / `js/` / `images/`로 역할이 분리된 폴더 구조 | `index.html:35` | V-1 | C-16 | E-2.1 |
| R-2 | 외부 스타일시트와 JS 파일이 HTML에 올바르게 연결됨 | `index.html:36` | V-1 | C-16 | — |
| R-3 | VS Code + Live Server로 실시간 개발 환경 구성 | README.md (로컬 실행) | V-2 | C-16 | — |

### B. HTML 시맨틱 마크업

| R-ID | 요구사항 | 구현 위치 | V | C | E |
|---|---|---|---|---|---|
| R-4 | `header`/`nav`/`main`/`section`/`article`/`footer` 사용, div 래핑만으로 구성하지 않음 | `index.html:48` `index.html:78` 외 1 | V-6 | C-1 | E-2.1, E-3.1 |
| R-5 | Hero 섹션 (인사말 + CTA 버튼) | `index.html:81` | V-6 | C-1 | E-1.1 |
| R-6 | About 섹션 (자기소개 + 프로필 이미지) | `index.html:97` | V-6 | C-1 | E-1.1 |
| R-7 | Skills 섹션 (기술 스택 목록) | `index.html:125` | V-6 | C-1 | E-1.1 |
| R-8 | Projects 섹션 (GitHub API 카드 영역) | `index.html:139` | V-6 | C-1 | E-1.1 |
| R-9 | Contact 섹션 (문의 폼) | `index.html:152` | V-6 | C-1 | E-1.1 |
| R-10 | Footer (저작권 + 소셜 링크) | `index.html:193` | V-6 | C-1 | E-1.1 |
| R-11 | 네비게이션에 각 섹션 앵커 링크 존재 | `index.html:54` | V-12 | C-1 | — |
| R-12 | 모든 `<img>`에 의미 있는 `alt` | `index.html:101` | V-7 | C-1 | E-3.1 |
| R-13 | 폼 `<label for>` ↔ `<input id>` 매칭 | `index.html:161` | V-8 | C-1 | E-3.1 |

### C. CSS 레이아웃 & 반응형

| R-ID | 요구사항 | 구현 위치 | V | C | E |
|---|---|---|---|---|---|
| R-14 | 외부 스타일시트 `css/style.css` 사용 | `index.html:36` | V-1 | C-16 | — |
| R-15 | `:root`에 색상·폰트·간격 CSS 변수 정의 | `css/style.css:15` | V-15 | C-7 | E-2.3 |
| R-16 | `[data-theme="dark"]`에 다크 모드 변수 별도 정의 | `css/style.css:68` | V-15 | C-7 | E-2.3 |
| R-17 | 네비게이션 = **Flexbox** (로고 왼쪽 / 메뉴 오른쪽) | `css/style.css:172` | V-9 | C-2 | E-2.2, E-3.2 |
| R-18 | Projects 카드 = **Grid** `repeat(auto-fit, minmax(...))` | `css/style.css:375` | V-9 | C-2 | E-2.2, E-3.2 |
| R-19 | 모바일 퍼스트 작성 (기본 스타일 = 모바일, `min-width`로 확장) | `index.html:5` `css/style.css:524` | V-9 | C-8 | E-2.2 |
| R-20 | 브레이크포인트 768px(태블릿) / 1024px(데스크톱) | `css/style.css:524` | V-9 | C-8 | E-2.2 |
| R-21 | 모바일에서 nav 숨김 + 햄버거 버튼 노출 | `index.html:69` `css/style.css:195` 외 1 | V-10 | C-8 | E-1.2 |
| R-22 | 버튼·카드 hover 효과 + `transition` 적용 | `css/style.css:290` `css/style.css:300` | V-9 | C-15 | — |
| R-23 | 카드에 `box-shadow` 적용 | `css/style.css:394` | V-9 | C-15 | — |

### D. JavaScript 기초 (DOM & 이벤트)

| R-ID | 요구사항 | 구현 위치 | V | C | E |
|---|---|---|---|---|---|
| R-24 | `<script defer>`로 JS 연결 | `index.html:39` | V-1 | C-3 | E-3.2 |
| R-25 | `var` 없이 `const`/`let`만 사용 | `js/main.js:5` | V-3 | C-4 | — |
| R-26 | 모든 이벤트를 `addEventListener`로 연결 (`onclick` 속성 0건) | `js/main.js:7` | V-4 | C-3 | E-3.2 |
| R-27 | `querySelector` / `querySelectorAll`로 요소 선택 | `js/utils.js:8` | V-23 | C-3 | E-3.2 |
| R-28 | `textContent` / `innerHTML`로 내용 변경 | `js/form.js:98` | V-23 | C-3, C-13 | E-4.2 |
| R-29 | `classList.add` / `remove` / `toggle`로 클래스 조작 | `js/scroll.js:49` `js/nav.js:40` | V-23 | C-3 | E-2.3 |
| R-30 | `click` / `submit` / `scroll` / `input` 4종 이벤트 처리 | `js/scroll.js:22` `js/form.js:52` | V-23 | C-3 | E-3.2 |
| R-31 | `event.preventDefault()`로 기본 동작 방지 | `js/form.js:74` | V-17 | C-3 | E-3.2 |

### E. 인터랙션

| R-ID | 요구사항 | 구현 위치 | V | C | E |
|---|---|---|---|---|---|
| R-32 | 햄버거 버튼 클릭 → 메뉴 표시, 재클릭 → 숨김 (`classList.toggle('active')`) | `index.html:69` | V-11 | C-6 | E-1.2 |
| R-33 | nav 메뉴 클릭 시 해당 섹션으로 **부드러운 스크롤** | `css/style.css:100` `js/nav.js:24` | V-12 | C-11 | E-1.2 |
| R-34 | 스크롤 **300px** 이상에서 탑 버튼 표시, 클릭 시 최상단 이동 (임계값 README 명시) | `index.html:203` `js/scroll.js:11` | V-13 | C-11 | E-1.2 |
| R-35 | 스크롤 **60px** 이상에서 nav 배경색 변경 (임계값 README 명시) | `css/style.css:166` `js/scroll.js:11` | V-14 | C-11 | E-1.2 |
| R-36 | 다크 모드 토글 버튼으로 테마 전환 | `index.html:63` | V-15 | C-7 | E-2.3 |
| R-37 | 테마 설정이 **localStorage**에 저장되어 새로고침 후 유지 | `index.html:11` `js/theme.js:27` | V-15 | C-7 | E-3.6 |
| R-38 | Intersection Observer로 스크롤 애니메이션 (threshold **0.2 이상**, README 명시) | `css/style.css:512` `js/observer.js:10` 외 1 | V-16 | C-9 | E-4.5 |
| R-39 | Contact 폼 3필드 존재 (이름 / 이메일 / 메시지) | `index.html:157` | V-17 | C-12 | E-1.5 |
| R-40 | 필수값 검증 — 빈 필드 제출 불가 | `js/form.js:18` | V-17 | C-6, C-12 | E-2.5 |
| R-41 | 이메일 형식 검증 | `js/form.js:13` | V-17 | C-6, C-12 | E-2.5 |
| R-42 | 에러 메시지가 **해당 입력 필드 근처**에 표시 | `css/style.css:454` `js/form.js:96` | V-17 | C-6, C-12 | E-2.5 |
| R-43 | 제출 시 `preventDefault()` + 성공 메시지 표시 | `index.html:187` `js/form.js:69` 외 1 | V-17 | C-3, C-6, C-12 | E-3.2 |

### F. ES6+ 문법 & 배열 메서드

| R-ID | 요구사항 | 구현 위치 | V | C | E |
|---|---|---|---|---|---|
| R-44 | 화살표 함수 활용 | `js/utils.js:8` | V-23 | C-4 | E-3.3 |
| R-45 | 템플릿 리터럴로 HTML 동적 생성 | `js/projects.js:19` | V-23 | C-4, C-13 | E-3.3, E-4.2 |
| R-46 | 구조분해 할당으로 객체/배열 값 추출 | `js/projects.js:19` | V-23 | C-4 | E-3.3 |
| R-47 | `map`으로 GitHub 데이터 → HTML 카드 변환, `forEach`로 순회 | `js/projects.js:61` | V-19 | C-4, C-14 | E-3.3 |

### G. 비동기 처리 & GitHub API

| R-ID | 요구사항 | 구현 위치 | V | C | E |
|---|---|---|---|---|---|
| R-48 | `fetch` + `async/await`로 `https://api.github.com/users/codewhite7777/repos` 호출 | `js/projects.js:87` | V-19 | C-5 | E-3.4 |
| R-49 | **로딩 상태** UI (스피너 또는 "로딩 중...") | `js/projects.js:54` | V-18 | C-5, C-6 | E-2.4 |
| R-50 | **성공 상태** UI (카드 리스트 렌더링) | `js/projects.js:61` | V-19 | C-5, C-6, C-14 | E-2.4 |
| R-51 | **에러 상태** UI ("프로젝트를 불러올 수 없습니다" + 재시도 버튼) | `js/projects.js:74` | V-20 | C-5, C-6 | E-2.4 |
| R-52 | **빈 상태** UI ("표시할 프로젝트가 없습니다") | `js/projects.js:68` | V-21 | C-5, C-6 | E-2.4 |
| R-53 | `try/catch`로 에러 처리 | `js/projects.js:87` | V-20 | C-5 | E-3.4 |
| R-54 | 레이트 리밋 403 응답 시 에러 상태 UI가 표시됨 | `js/projects.js:102` | V-22 | C-10 | E-4.3 |

### H. 상태 관리 패턴 (이 과제의 핵심)

| R-ID | 요구사항 | 구현 위치 | V | C | E |
|---|---|---|---|---|---|
| R-55 | "이벤트 → 상태 변경 → 화면 업데이트" 흐름이 **3가지 이상** 코드에서 식별 가능 | `js/main.js:21` `js/state.js:9` 외 1 | V-23 | C-6 | E-3.5, E-4.4 |

채택할 3흐름 (원문 예시 1~3) — 전부 `state.js`의 단일 상태를 거친다 (설계 결정 #3):

| # | 이벤트 | `setState` | 렌더 |
|---|---|---|---|
| 1 | 토글 버튼 `click` | `{ theme }` | `documentElement.dataset.theme` 갱신 → CSS 변수 전환 |
| 2 | 진입/재시도 `click` | `{ status, repos }` | `renderers[status]()`로 Projects 섹션 교체 |
| 3 | 폼 `submit` / `input` | `{ errors }` | 필드별 에러 메시지 표시·숨김 |

> **상태를 DOM에서 읽지 않는다.** 현재 테마를 `classList.contains()`로 확인하는 식의 코드가
> 하나라도 들어가면 흐름이 양방향이 되어 E-3.5를 설명할 수 없게 된다.

### I. 배포

| R-ID | 요구사항 | 구현 위치 | V | C | E |
|---|---|---|---|---|---|
| R-56 | GitHub Pages 배포 + 외부 접속 가능한 URL 존재 | GitHub Pages `main` / root | V-24 | C-16 | E-1.6 |
| R-57 | 배포 URL에서 반응형·인터랙션·API·폼 검증이 모두 동작 | 배포 URL 검증 — V-24 | V-24 | C-16 | E-1.6 |
| R-58 | README에 설명·사용 기술·배포 URL·스크린샷 + **임계값 3개(300/60/0.2)** 명시 | README.md | V-25 | C-16 | E-1.6 |

### 보너스 (선택 — 수행/미수행 모두 기록)

| B-ID | 내용 | 수행 |
|---|---|---|
| B-1 | 언어별 프로젝트 필터링 버튼 (`array.filter()`) — 4번째 상태 흐름이 되므로 **우선 권장** | ☐ |
| B-2 | Hero 타이핑 효과 | ☐ |
| B-3 | Formspree / EmailJS로 폼 실제 전송 | ☐ |
| B-4 | `prefers-color-scheme`로 시스템 다크 모드 감지 | ☐ |

---

## 5. 알아야 하는 개념 (C)

C-1 ~ C-6은 원문 §3 "과제 목표"에서 그대로 온 것이다. **평가에서 반드시 질문된다.**
C-7 ~ C-16은 원문 목표에는 없지만 **기능 요구사항을 구현하면 반드시 마주치는** 개념이다.
C-11 ~ C-16은 요구사항 커버리지 감사에서 개념이 비어 있던 13건을 메우며 추가했다.

정리본은 `NOTE.md` §2에 작성되어 있다. **정리본은 읽는 자료이고, 각 카드의 ✍️ 칸은 직접 채운다.**
구술에서 묻는 것은 개념의 정의가 아니라 "네 코드의 어디에서 그것을 썼고 왜 그렇게 정했나"이므로,
✍️ 칸이 비어 있으면 그 개념은 아직 준비되지 않은 것으로 본다.

| C-ID | 개념 | 왜 이 과제에 필요한가 | 정리본 | 내 답변 |
|---|---|---|---|---|
| C-1 | 시맨틱 태그와 문서 구조 설계 기준 | R-4~R-13의 근거. "왜 div가 아닌가"가 질문된다 | ✅ | ☐ |
| C-2 | Flexbox vs Grid — 1차원 vs 2차원 | nav는 Flex, 카드는 Grid로 **지정**되어 있다. 이유를 못 대면 실패 | ✅ | ☐ |
| C-3 | querySelector 선택 → addEventListener 바인딩 → event 객체 | 모든 인터랙션의 공통 뼈대 | ✅ | ☐ |
| C-4 | ES6+ (화살표 함수 / 구조분해 / map·filter) | 선언적 데이터 변환. "왜 for문이 아닌가" | ✅ | ☐ |
| C-5 | fetch · async/await · Promise · try/catch | API 연동 4상태의 기반 | ✅ | ☐ |
| C-6 | 이벤트 → 상태 → 렌더링 단방향 흐름 | **이 과제의 핵심.** React 상태-렌더링의 원형 | ✅ | ☐ |
| C-7 | CSS 변수 + `data-theme` 속성 + localStorage 지속성 | 다크 모드 구현 방식의 근거 | ✅ | ☐ |
| C-8 | 모바일 퍼스트와 `min-width` 미디어 쿼리 누적 | 브레이크포인트 설계의 근거 | ✅ | ☐ |
| C-9 | Intersection Observer가 scroll 이벤트보다 나은 이유 | 메인 스레드 비용·리플로우 | ✅ | ☐ |
| C-10 | GitHub API 레이트 리밋(60회/시간)과 에러 상태 설계 | 403 처리 요구의 배경 | ✅ | ☐ |
| C-11 | 스크롤 제어와 `scroll` 이벤트 | 부드러운 스크롤·탑 버튼·nav 변경의 기반. IO(C-9)와 역할이 다르다 | ✅ | ☐ |
| C-12 | 폼 검증과 접근성(ARIA) | R-40~R-43의 방법론. E-2.5가 검증 시점을 직접 묻는다 | ✅ | ☐ |
| C-13 | XSS와 안전한 렌더링 | 템플릿 리터럴+`innerHTML` 결정(설계 #4)의 대가. E-4.2가 정면으로 묻는다 | ✅ | ☐ |
| C-14 | 렌더링 파이프라인과 성능 | E-4.1("100개면 병목이 어디인가")에 답할 근거 | ✅ | ☐ |
| C-15 | `transition`과 시각 효과 비용 | R-22·R-23의 근거. 어떤 속성을 애니메이션할지가 성능을 가른다 | ✅ | ☐ |
| C-16 | 정적 사이트 구조와 배포 | 파일 분리 이유·Live Server가 필요한 진짜 이유·하위 경로 배포 | ✅ | ☐ |

## 6. 평가문항 (E) — **예측치**

> 이 과제의 평가지는 아직 받지 못했다. 아래는 원문 §3 "과제 목표"와
> `references/eval-criteria.md`의 질문 어휘 패턴(어떻게 / 왜 / 만약 ~라면 / 판단 흐름)으로
> **역산한 예측**이다. 실제 평가지를 받으면 이 절을 통째로 교체한다.

### 항목 1 — 동작 검증

| E-ID | 예상 질문 |
|---|---|
| E-1.1 | 6개 섹션이 모두 존재하고 모바일/태블릿/데스크톱에서 레이아웃이 최적화되는가? |
| E-1.2 | 햄버거 메뉴·부드러운 스크롤·스크롤 탑·nav 배경 변경이 모두 동작하는가? |
| E-1.3 | 다크 모드 토글이 동작하고 새로고침 후에도 설정이 유지되는가? |
| E-1.4 | GitHub API 연동의 로딩/성공/에러/빈 상태가 모두 UI로 표현되는가? |
| E-1.5 | 폼 필수값·이메일 형식 검증과 에러/성공 메시지가 동작하는가? |
| E-1.6 | 배포 URL에서 전 기능이 동작하고 README 필수 항목이 포함되어 있는가? |

### 항목 2 — 구현 방법 ("어떻게")

| E-ID | 예상 질문 |
|---|---|
| E-2.1 | 시맨틱 태그로 문서 구조를 **어떻게** 나눴고, 그 기준은 무엇인가? |
| E-2.2 | 네비게이션에 Flexbox를, Projects 카드에 Grid를 쓴 이유를 각각 설명할 수 있는가? `auto-fit`과 `minmax`가 하는 일은? |
| E-2.3 | 다크 모드를 `data-theme` 속성 + CSS 변수로 **어떻게** 구현했는가? 클래스 토글 방식과 비교하면? |
| E-2.4 | 로딩/성공/에러/빈 4가지 상태를 **어떻게** 분기해 렌더링했는가? |
| E-2.5 | 폼 검증을 `input` 시점과 `submit` 시점 중 언제 실행했고, 왜 그렇게 정했는가? |

### 항목 3 — 개념 원리 ("왜")

| E-ID | 예상 질문 |
|---|---|
| E-3.1 | 시맨틱 태그를 **왜** 쓰는가? (접근성·SEO·유지보수 관점) `alt`와 `label for`는 왜 필요한가? |
| E-3.2 | `querySelector`로 선택하고 `addEventListener`로 연결하는 흐름을 설명하라. `preventDefault()`는 무엇을 막는가? |
| E-3.3 | 화살표 함수·구조분해·`map`이 **왜** 필요한가? `map`과 `forEach`의 차이는? |
| E-3.4 | `async/await`와 Promise의 관계는? `try/catch`가 잡는 에러와 **못 잡는 에러**는? (예: 404는 왜 catch로 안 가는가) |
| E-3.5 | 이벤트 → 상태 → DOM 업데이트 흐름을 설명하라. 이것이 React의 무엇에 해당하는가? |
| E-3.6 | localStorage에 언제 쓰고 언제 읽는가? 페이지 로드 시 테마가 깜빡이는 문제는 왜 생기는가? |

### 항목 4 — 확장·응용 ("만약 ~라면")

| E-ID | 예상 질문 |
|---|---|
| E-4.1 | 저장소가 100개로 늘어나면 현재 렌더링 구조의 병목은 어디이고 어떻게 개선하겠는가? |
| E-4.2 | API 응답을 `innerHTML`로 렌더링할 때의 위험은? (XSS) 어떻게 대응하겠는가? |
| E-4.3 | 레이트 리밋 403이 실제로 발생하면 사용자에게 무엇을 보여주겠는가? 재호출을 줄이려면? |
| E-4.4 | 이 페이지를 React로 옮긴다면 지금 코드의 무엇이 무엇으로 대체되는가? |
| E-4.5 | Intersection Observer 대신 `scroll` 이벤트로 구현했다면 어떤 문제가 생기는가? |
| E-4.6 | 다시 만든다면 무엇을 다르게 하겠는가? |

> **E-4.6(다시 만든다면)만 개념 카드가 없다.** 회고 문항이라 사전 학습 대상이 아니며,
> `NOTE.md` §6에서 구현을 마친 뒤 채운다. 나머지 22건은 전부 개념 카드가 받친다.

### 항목 5 — 보너스

| E-ID | 내용 |
|---|---|
| E-5 | 보너스 과제 수행에 따른 크레딧 부여 여부 |

## 7. 검증 절차 (V)

증거는 `evidence/`에 저장한다. 파일명 규칙: `v<번호>-<내용>.<확장자>`

| V-ID | 검증 방법 | 기대 결과 | 증거 |
|---|---|---|---|
| V-1 | 폴더 구조와 `<link>`/`<script>` 연결 확인 | index.html/css/js/images 분리, 외부 라이브러리 링크 0개 | `v1-structure.txt` |
| V-2 | Live Server 실행 | localhost에서 페이지 로드 | `v2-liveserver.png` |
| V-3 | `rg -n '\bvar\b' js/` | 매치 0건 | `v3-var.txt` |
| V-4 | `rg -n 'on[a-z]+=' index.html` | `onclick` 등 인라인 핸들러 0건 | `v4-onclick.txt` |
| V-5 | `rg -n 'style="' index.html` | 인라인 스타일 0건 | `v5-inline-style.txt` |
| V-6 | 시맨틱 태그·6섹션 존재 확인 | header/nav/main/section/article/footer + 6개 id | `v6-semantic.txt` |
| V-7 | `<img>` 개수와 `alt=` 개수 비교 | 동일 (누락 0) | `v7-alt.txt` |
| V-8 | `label for` 값과 `input id` 값 대조 | 전부 매칭 | `v8-label.txt` |
| V-9 | DevTools 320 / 768 / 1024 / 1440px 캡처 | 레이아웃 붕괴 없음, nav=Flex, 카드=Grid | `v9-responsive-*.png` |
| V-10 | 375px 폭에서 nav 표시 상태 확인 | nav 숨김 + 햄버거 노출 | `v10-mobile-nav.png` |
| V-11 | 햄버거 클릭 → 재클릭 | 메뉴 표시 → 숨김 | `v11-hamburger-*.png` |
| V-12 | nav 앵커 클릭 | 해당 섹션으로 부드럽게 이동 | `v12-anchor.png` |
| V-13 | 300px 미만/초과 스크롤 | 탑 버튼 숨김 → 표시, 클릭 시 최상단 | `v13-scrolltop-*.png` |
| V-14 | 60px 미만/초과 스크롤 | nav 배경색 변화 | `v14-nav-*.png` |
| V-15 | 다크 토글 → 새로고침 → Application 탭 확인 | 테마 유지 + localStorage에 키 존재 | `v15-theme-*.png` |
| V-16 | 섹션 진입 스크롤 | 애니메이션 발동, threshold 값 코드와 README 일치 | `v16-observer.png` |
| V-17 | 빈 제출 / 잘못된 이메일 / 정상 제출 3케이스 | 차단 → 형식 에러 → 성공 메시지, 페이지 새로고침 없음 | `v17-form-*.png` |
| V-18 | Network 탭 Slow 3G 스로틀링 후 로드 | 로딩 상태 UI 표시 | `v18-loading.png` |
| V-19 | 정상 로드 | 카드 리스트 렌더링 | `v19-success.png` |
| V-20 | 존재하지 않는 사용자명으로 404 유도 | 에러 메시지 + 재시도 버튼, 재시도 동작 | `v20-error.png` |
| V-21 | DevTools 응답 오버라이드로 빈 배열 주입 (계정 public repo 13개 → 실제 재현 불가) | "표시할 프로젝트가 없습니다" | `v21-empty.png` |
| V-22 | DevTools로 403 응답 오버라이드 (또는 실제 레이트 리밋) | 에러 상태 UI 표시 | `v22-ratelimit.png` |
| V-23 | 전체 조작 후 Console 확인 + 코드 리뷰 | Console 에러 0건, R-24~R-31·R-44~R-47·R-55 요소가 코드에 존재 | `v23-console.png` |
| V-24 | **배포 URL**에서 V-9~V-22 핵심 재확인 | 로컬과 동일 동작 | `v24-deployed-*.png` |
| V-25 | README 항목 확인 | 설명·기술·URL·스크린샷·임계값 3개 | `v25-readme.png` |

## 8. 설계 결정 로그

구현 전에 정해야 할 갈림길. 여기서 고른 근거가 **평가 항목 2~3의 답변 원료**가 된다.
`?` 표시는 아직 결정 안 된 것 — 구현 착수 전에 채운다.

| # | 결정 | 선택지 | 택한 것 | 이유 / 기각 이유 |
|---|---|---|---|---|
| 1 | JS 파일 분할 | 단일 `main.js` / ES 모듈 분할 / 전역 네임스페이스 | **ES 모듈 분할** (`state` `theme` `nav` `projects` `form` `observer`) | 책임 경계가 `import`/`export`로 코드에 드러나 E-2.1 답변이 생긴다. 구 평가 샘플에서 "모듈 3개 이상 분리 + 책임 설명"이 FAIL 항목이었다. 단일 파일은 규모가 커지면 답할 거리가 없어 기각. 전역 네임스페이스는 의존 순서가 `<script>` 배열에 숨어 기각 |
| 2 | 테마 전환 방식 | `data-theme` 속성 / `.dark` 클래스 | `data-theme` | 원문 §4가 `[data-theme="dark"]`를 명시. 선택지가 아님 |
| 3 | 상태 보관 위치 | 단일 상태 객체+구독 / 모듈 지역 상태 / DOM을 상태로 | **단일 상태 객체 + 구독 렌더** | `state.js`에 상태 하나와 `setState`를 두고, 변경 시 구독된 렌더 함수를 호출한다(약 25줄). 흐름이 코드에 그대로 드러나 R-55·E-3.5를 코드로 증명할 수 있고, 다음 과제인 React의 `useState`→리렌더링과 1:1로 대응된다. 모듈 지역 상태는 상태가 3곳에 흩어져 "상태가 어디 있느냐"에 한 번에 답할 수 없어 기각. DOM을 상태로 쓰는 방식은 이 과제의 목표(상태와 렌더링 분리)와 정반대라 기각 |
| 4 | 카드 렌더링 | 템플릿 리터럴+`innerHTML` / `createElement` | **템플릿 리터럴 + `escapeHtml()` 유틸** | R-45가 템플릿 리터럴을 요구하므로 방식 자체는 고정. 다만 GitHub API의 `name`·`description`은 외부 입력이라 그대로 `innerHTML`에 넣으면 XSS가 열린다. 삽입 직전 이스케이프 유틸을 거치는 것으로 요구사항과 안전성을 동시에 만족시킨다. 이 결정이 곧 E-4.2의 답변이다 |
| 5 | 폼 검증 시점 | `submit`만 / `submit` 후 `input` 재검증 / 항상 `input` | **`submit` 전체 검증 → 이후 해당 필드만 `input` 재검증** | 첫 제출 전에는 간섭하지 않고, 한 번 틀린 필드만 입력 중 에러가 풀린다(touched 패턴). R-30의 `input` 이벤트 요구를 억지 없이 충족한다. `submit`만 쓰면 에러를 고쳐도 메시지가 남고, 항상 검증하면 이름 한 글자에 형식 오류가 떠 공격적인 UX가 되어 둘 다 기각 |
| 6 | 4상태 렌더링 | if/else 분기 / 상태별 렌더 함수 맵 / DOM 블록 토글 | **상태별 렌더 함수 맵** | `renderers[status]()` 형태. 상태가 4개라는 사실과 각각이 무엇을 그리는지가 한눈에 보여 E-2.4 답변이 명확해지고, 보너스 필터 상태를 추가할 때도 한 줄이면 된다. if/else는 분기가 길어지며 상태 종류가 코드에 흩어져 기각. DOM 블록 토글은 상태 파악에 HTML과 JS를 함께 봐야 해 기각 |
| 7 | 임계값 | 300px / 60px / 0.2 (원문 권장값) | 권장값 사용 | 변경 시 README 명시 의무 발생. 바꿀 이유 없음 |

## 9. 구현 순서 (제안)

의존 관계상 아래 순서가 되돌아가는 일이 가장 적다.

1. **골격** — 폴더 구조 + 시맨틱 HTML 6섹션 (R-1~R-13)
2. **토큰** — `:root` 변수 + 다크 변수 정의 (R-14~R-16)
3. **레이아웃** — 모바일 퍼스트 → 768 → 1024, nav Flex / 카드 Grid (R-17~R-23)
4. **상태 골격** — 전역 상태 객체와 렌더 함수부터 만든다 (R-55). **이걸 먼저 만들어야 나머지가 흐름에 붙는다**
5. **인터랙션** — 햄버거 → 스크롤 3종 → 다크모드+localStorage (R-32~R-38)
6. **API** — 4상태 렌더링 → fetch/async/await → try/catch → 403 (R-48~R-54)
7. **폼** — 검증 → 에러 표시 → 성공 (R-39~R-43)
8. **배포·문서** — Pages 배포 → README → 스크린샷 (R-56~R-58)

> 4번을 3번 뒤로 미루지 않는다. 상태 구조를 나중에 끼워 넣으면 R-55가 "사후 정리"가 되고,
> 그 상태로는 E-3.5(React 연결)를 설명할 수 없다.

## 10. 완료 정의

- [ ] R-1 ~ R-58 전부 구현 위치가 채워짐
- [ ] V-1 ~ V-25 전부 PASS + 증거 파일 존재
- [ ] C-1 ~ C-10 노트 카드 작성 완료
- [ ] E-1.1 ~ E-4.6 노트 없이 답변 가능
- [ ] 설계 결정 로그의 `?` 없음
- [ ] 보너스 B-1~B-4 수행/미수행 명시
- [ ] repo URL · 배포 URL이 `INDEX.md`에 기록됨
