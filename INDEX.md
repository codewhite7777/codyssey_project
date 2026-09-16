# Codyssey 올인원 과정 — 진도 보드

> 진도의 단일 진실 원천. 상태가 바뀌면 여기부터 고친다.
> 상태: `미착수` → `분석중` → `구현중` → `검증중` → `제출` → `통과` / `재도전`

| 항목 | 값 |
|---|---|
| 관리 모노레포 | https://github.com/codewhite7777/codyssey_project (public · `main`) |
| GitHub 계정 | `codewhite7777` (public repo 13개 — 빈 상태 검증은 응답 오버라이드 필요) |

## 구조

```
단계(stage)              →  구분(분야)            →  과제(mission)
1단계 AI/SW 기초          →  웹 기초와 프론트엔드   →  나를 소개하는 웹페이지 만들기
                         →  Linux와 OS            →  …
2단계 AI/SW 심화          →  …
3단계 AI/SW 응용          →  …
```

- **과제 번호는 가변이다.** 폴더는 슬러그로 고정하고, 번호는 이 표와
  `MISSION_SPEC.md` 머리표에만 둔다. (근거: `SPEC.md` §1 "과제 ID 규칙")
- `eval_pdf/`의 평가 자료는 **번호 개편 이전 자료**다. 번호·과제명 대조에 쓰지 않고
  채점 구조 참고용으로만 쓴다. → `references/eval-criteria.md`

---

## 1단계 — AI/SW 기초

📁 [`missions/stage-1-ai-sw-basic/`](missions/stage-1-ai-sw-basic/)

| 과제 폴더 | 번호 | 구분 | 과제명 | 시간 | 상태 | repo | 배포 | 평가 | 보너스 |
|---|---|---|---|---|---|---|---|---|---|
| `b1-1-web-portfolio` | B1-1 | 웹 기초와 프론트엔드 | 나를 소개하는 웹페이지 처음부터 만들기 | 80h · 필수 | **구현 대기** | [codyssey-b1-portfolio](https://github.com/codewhite7777/codyssey-b1-portfolio) | [Pages](https://codewhite7777.github.io/codyssey-b1-portfolio/) | — | 미정 |
| | | | *(다음 과제 · React 예정)* | | 미착수 | | | | |

## 2단계 — AI/SW 심화

📁 `missions/stage-2-ai-sw-advanced/` — 착수 시 생성

| 과제 폴더 | 번호 | 구분 | 과제명 | 시간 | 상태 | repo | 배포 | 평가 | 보너스 |
|---|---|---|---|---|---|---|---|---|---|
| | | | | | 미착수 | | | | |

## 3단계 — AI/SW 응용

📁 `missions/stage-3-ai-sw-applied/` — 착수 시 생성

| 과제 폴더 | 번호 | 구분 | 과제명 | 시간 | 상태 | repo | 배포 | 평가 | 보너스 |
|---|---|---|---|---|---|---|---|---|---|
| | | | | | 미착수 | | | | |

---

## 새 과제 착수 절차

```
1. mkdir -p missions/<단계슬러그>/<번호>-<구분>-<슬러그>/{source,evidence}
2. 과제 원문 → source/assignment.md   (수정 금지)
3. templates/{MISSION_SPEC,NOTE,CHECKLIST}.md → missions/<단계>/<과제폴더>/
4. SPEC.md §2 파이프라인 1~6단계 순서로 진행
5. 이 파일과 단계 README.md에 행 추가
```

## 로그

| 날짜 | 내용 |
|---|---|
| 2026-09-17 | 워크스페이스 구성 (SPEC / 템플릿 / 평가기준 역설계) |
| 2026-09-17 | 3단계 계층 구조로 재편. 과제번호를 폴더에서 분리 (슬러그 고정) |
| 2026-09-17 | 3단계 확정: AI/SW 기초 / AI/SW 심화 / AI/SW 응용 |
| 2026-09-17 | B1-1 `b1-1-web-portfolio` 접수·분석 완료 — R 58개 / C 10개 / E 22개(예측) / V 25개 |
| 2026-09-17 | 설계 결정 6건 확정. 모노레포 원격 연결 및 push |
| 2026-09-17 | B1-1 제출 repo 생성 + Pages 활성화. 상대경로 골격 배포로 배포 경로 선검증 |
| 2026-09-17 | B1-1 구현 완료 — HTML/CSS/ES모듈 9개. V-1~V-23 PASS, 증거 7건 확보 |
