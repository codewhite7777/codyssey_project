# B1-1 web-portfolio — 제출 전 자가 검증

> **실행하지 않은 항목은 PASS로 적지 않는다.** 증거 파일 경로를 반드시 남긴다.
> 증거 위치: `evidence/`

## A. 기능 검증 (V) — 평가 항목 1 대응

| V-ID | 검증 | 실제 결과 | 증거 | 판정 |
|---|---|---|---|---|
| V-1 | 폴더 구조 + 외부 라이브러리 링크 확인 | 폰트 외 외부 링크 0 · 역할 분리 O | `evidence/v01-08-static-checks.txt` | ✅ PASS |
| V-2 | Live Server 실행 | python3 http.server로 대체 — 정상 로드 | 동일 | ✅ PASS* |
| V-3 | `rg -n '\bvar\b' js/` | 0건 | 동일 | ✅ PASS |
| V-4 | `rg -n 'on[a-z]+=' index.html` | 0건 | 동일 | ✅ PASS |
| V-5 | `rg -n 'style="' index.html` | 0건 | 동일 | ✅ PASS |
| V-6 | 시맨틱 태그 + 6섹션 | header/nav/main/footer 1, section 5, article은 projects.js | 동일 | ✅ PASS |
| V-7 | `<img>` 수 = `alt=` 수 | img 1 / alt 1 | 동일 | ✅ PASS |
| V-8 | `label for` ↔ `input id` | 3쌍 모두 매칭 | 동일 | ✅ PASS |
| V-9 | 320/768/1024/1440px 캡처 | 892·1489px 정상, 371px 1열 | `v09-10-responsive.json`, `v09-desktop-light.jpg` | ✅ PASS |
| V-10 | 375px nav 상태 | 메뉴 hidden + 햄버거 flex | `v09-10-responsive.json` | ✅ PASS |
| V-11 | 햄버거 토글 2회 | active·aria-expanded 토글 | `v11-17-interactions.json` | ✅ PASS |
| V-12 | nav 앵커 클릭 | 섹션이 헤더 아래 64px에 정렬 | `v13-14-scroll.json` | ✅ PASS |
| V-13 | 스크롤 300px 전후 | 0→off · 100→off · 400→on | `v13-14-scroll.json` | ✅ PASS |
| V-14 | 스크롤 60px 전후 | 0→off · 100→on | `v13-14-scroll.json` | ✅ PASS |
| V-15 | 다크 토글 + 새로고침 | 새로고침 후 dark 유지 | `v11-17-interactions.json`, `v15-dark-projects.jpg` | ✅ PASS |
| V-16 | 섹션 진입 | is-visible 부착 후 unobserve | `v13-14-scroll.json` | ✅ PASS |
| V-17 | 폼 3케이스 (빈값/형식오류/정상) | 3케이스 + 재검증 해제 | `v11-17-interactions.json` | ✅ PASS |
| V-18 | Slow 3G 스로틀링 | aria-busy=true + 스피너 | `v18-22-api-states.json` | ✅ PASS |
| V-19 | 정상 로드 | 카드 15개 | `v18-22-api-states.json` | ✅ PASS |
| V-20 | 잘못된 사용자명 (404) | 404 메시지 + 재시도 복구 | `v18-22-api-states.json` | ✅ PASS |
| V-21 | 빈 응답 | 빈 배열 주입 (실제 재현 불가) | `v18-22-api-states.json` | ✅ PASS* |
| V-22 | 403 오버라이드 | 403 전용 메시지 | `v18-22-api-states.json` | ✅ PASS |
| V-23 | Console + 코드 리뷰 | 의도한 에러 로그 외 0건 | 본문 | ✅ PASS |
| V-24 | **배포 URL** 재확인 | 자산 6종 200 · 모듈 실행 · 카드 15 · 테마/햄버거/폼 동작 | `evidence/v24-deployed.json` | ✅ PASS |
| V-25 | README 항목 | 설명·기술·URL·임계값 기재 | `repo/README.md` | ⚠️ 모바일 샷 누락 |

## B. 제약 준수 (위반 시 무효)

- [x] React/Vue/jQuery/Bootstrap/Tailwind 미사용 (CDN 한 줄도 없음)
- [x] Google Fonts(Inter, Noto Sans KR) 외 외부 링크 없음
- [x] `var` 0건 · `onclick` 속성 0건 · 인라인 `style` 0건
- [x] 최신 Chrome에서 전 기능 동작 (로컬 검증 완료)

## C. 문서·주석 규약 (SPEC §4)

- [x] `style.css` / 각 JS 파일에 헤더 블록(책임 · 담당 R-ID · 실패 정책)
- [x] 핵심 블록마다 `WHAT:` / `WHY:` 분리
- [x] 모든 `WHY:`에 **기각한 대안**이 적혀 있음
- [x] `[R-n]` 앵커로 코드에서 추적됨 — R-54건이 코드 앵커, R-3/56/57/58은 문서·배포로 대응
- [x] 코드를 그대로 읽는 주석·죽은 주석 코드 없음
- [ ] **AI 생성 코드가 `NOTE.md` §3에 내 말로 재설명됨 ← 학습자가 직접 채울 것**

## D. 구술 대비 (E) — 평가 항목 2~4 대응

| 문항 | 노트 없이 답변 가능? |
|---|---|
| E-2.1 ~ E-2.5 (구현 방법) | ☐ 가능 ☐ 불가 |
| E-3.1 ~ E-3.6 (개념 원리) | ☐ 가능 ☐ 불가 |
| E-4.1 ~ E-4.6 (확장 응용) | ☐ 가능 ☐ 불가 |

☐ 불가가 하나라도 남아 있으면 제출하지 않는다.

**특히 자주 막히는 3개 — 먼저 점검**
- [ ] `fetch`가 404/403에서 reject하지 않는다는 것 (E-3.4)
- [ ] `auto-fit`과 `minmax`가 각각 하는 일 (E-2.2)
- [ ] 내 코드의 상태 3개를 이벤트 → 상태 → 렌더링으로 끊어 말하기 (E-3.5)

## E. 제출 형식

- [x] repo URL: https://github.com/codewhite7777/codyssey-b1-portfolio
- [x] 배포 URL (GitHub Pages): https://codewhite7777.github.io/codyssey-b1-portfolio/
- [x] 브랜치: `main`
- [ ] 스크린샷 3종 — 데스크톱 ✅ / 다크모드 ✅ / **모바일 ❌ 미촬영**
- [ ] README: 설명 · 사용 기술 · 배포 URL · 스크린샷 · 임계값 3개(300px / 60px / 0.2)
- [ ] 보너스 B-1~B-4 수행 여부 명시
- [ ] `INDEX.md` 갱신


---

## 미해결 항목 (제출 전 반드시 처리)

| # | 항목 | 이유 | 처리 방법 |
|---|---|---|---|
| 1 | 모바일 스크린샷 | 브라우저 창이 892px 미만으로 줄지 않음 | DevTools 기기 툴바(⌘⇧M) → iPhone → 전체 페이지 캡처 → `repo/docs/screenshots/mobile.jpg` |
| 2 | `NOTE.md` ✍️ 17칸 | 구술 평가 대상 — 대신 채우면 의미가 없음 | 코드를 읽으며 직접 작성 |
| 3 | About/Skills 내용 | 자리표시자 문구 | 본인 소개로 교체 |

\* PASS* 표시는 조건을 바꿔 대체 검증한 항목이다(V-2 정적 서버 대체, V-21 응답 주입).
