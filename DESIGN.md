# Design Tokens

> 출처: Figma `[SBS] OCR 프로젝트_디자인` 파일 "🔵 디자인시스템" 페이지 (node 39:2)
> https://www.figma.com/design/ese9l01OJiDfirO8Q6XXIY/-SBS--OCR-프로젝트_디자인?node-id=39-2
>
> 이 문서는 2026-09-14에 Figma를 `get_metadata` / `get_variable_defs` / `get_design_context` / `get_screenshot`로 다시 조회해 **전면 재작성**했다. 이전 버전(2025-08-19 작성)과 비교했을 때 색상 토큰 체계, 타이포그래피 수치, 컴포넌트 구성이 상당히 달라졌다. 아래 값은 실제로 조회한 결과 그대로이며, 임의로 생성한 값은 없다.

## 0. 지난 버전 대비 주요 변경 사항

- **Color 토큰 체계가 완전히 새로 생겼다.** 이전 버전에서 "미완성이라 제외"했던 `Color Token-Atomic`, `Color Token-Semantic` 페이지가 이제 채워져 있고, **Light/Dark 모드가 모두 존재**한다.
- **Cool Neutral 램프와 Red 램프의 실제 값이 바뀌었다.** 같은 토큰 이름이라도 8월 문서의 hex와 지금 hex가 다르다 (§1.4 참고).
- **Typography 수치가 바뀌었다.** Line-height/letter-spacing이 전반적으로 조정됐고, 8월 버전에 있던 이상값(Heading02=Heading03 크기 중복, Caption 일부 line-height 튐)이 해소됐다.
- **새 컴포넌트 확보:** `Modal`(그동안 없던 Dialog/Modal), `Progress-bar`, `Program-select`/`Dropdown-item`(그동안 없던 Select/Dropdown), `Elevation`(그림자 토큰) — 이전 문서와 `design-system-test.html`이 "정의 없어 제외"라고 명시했던 Select/Dialog 공백이 채워졌다.
- Figma 페이지 구성 자체가 바뀌어, 이 문서의 목차도 Figma 최상위 프레임 이름(Layout / Button / Textfield / Check-box / Date-picker / Bottom-sheet / Badge / Card / Image-input / Elevation / Progress / Modal-Tooltip / Action-Area) 순서를 그대로 따르도록 재구성했다.

## 1. Color

### 1.1 Atomic (원시값) — `Color Token-Atomic` (node 55:2157)

| 그룹 | 토큰 | 값 |
|---|---|---|
| Common | color-atomic-common-0 / 100 | #FFFFFF / #000000 |
| Cool Neutral | color-atomic-cool-neutral-5~100 | 5:#F7F8F9 10:#F1F3F4 15:#EBEEF0 20:#DEE3E7 30:#CDD3D7 40:#BABEC2 50:#A2A9AE 60:#8C9499 70:#575E62 80:#434648 90:#222426 100:#191A1B |
| Clear Blue(브랜드) | color-atomic-brand-clearblue-5~90 | 5:#EFF8FF 10:#DBEEFE 20:#BEE2FF 30:#93D2FD 40:#60B8FA 50:#3B99F6 **60:#2A7FEC(key color)** 70:#1D65D8 80:#1E52AF 90:#1E488A |
| Sky Blue(state) | color-atomic-skyBlue-5~90, A10~A40 | 5:#E1F5FE 10:#B3E5FC 20:#81D4FA 30:#4FC3F7 40:#29B6F6 50:#03A9F4 60:#039BE5 70:#0288D1 80:#0277BD 90:#01579B / A10:#80D8FF A20:#40C4FF A30:#00B0FF A40:#0091EA |
| Green(state) | color-atomic-green-5~90, A10~A40 | 5:#E8F5E9 10:#C8E6C9 20:#A5D6A7 30:#81C784 40:#66BB6A 50:#4CAF50 60:#43A047 70:#388E3C 80:#2E7D32 90:#1B5E20 / A10:#B9F6CA A20:#69F0AE A30:#00E676 A40:#00C853 |
| Red(state) | color-atomic-red-5~90, A10~A40 | 5:#FFEBEE 10:#FFCDD2 20:#EF9A9A 30:#E57373 40:#EF5350 50:#F44336 60:#E53935 70:#D32F2F 80:#B71C1C 90:#82181A / A10:#FF8A80 A20:#FF5252 A30:#FF1744 A40:#D50000 |

### 1.2 Semantic (의미값) — Light — `Color Token-Semantic (의미값) Light` (node 97:1313)

의미 토큰은 모두 위 Atomic 토큰을 참조한다. `→` 뒤가 실제 바인딩된 atomic 토큰이다.

| 그룹 | 토큰 | → Atomic |
|---|---|---|
| Static | static-white / static-black | common-0 / cool-neutral-100 |
| Background | bg-primary / bg-secondary / bg-alternative / bg-inverse / bg-inverse-strong | cool-neutral-5 / common-0 / cool-neutral-10 / cool-neutral-80 / cool-neutral-90 |
| Foreground-normal | fg-normal / fg-selected / fg-weak / fg-disabled-normal / fg-disabled-subtle | cool-neutral-5 / -15 / -10 / -30 / -15 |
| Foreground-brand | fg-brand-normal / fg-brand-selected / fg-brand-disabled / fg-brand-secondary-selected / fg-brand-secondary-disabled | clearBlue-60 / clearBlue-80 / cool-neutral-20 / clearBlue-5 / cool-neutral-10 |
| Label(brand) | label-brand-normal / -selected / -weak / -disabled | clearBlue-60 / -40 / -20 / cool-neutral-20 |
| Label(primary) | label-primary-normal / -selected / -alternative / -weak / -disabled | cool-neutral-90 / -70 / -50 / -40 / -60 |
| Label(secondary) | label-secondary-normal / -selected / -weak / -disabled | cool-neutral-80 / -60 / -50 / -40 |
| Label(기타) | label-inverse | common-0 |
| Status(pending·안내) | status-pending-normal / -strong / -subtle | skyBlue-50 / skyBlue-60 / skyBlue-5-opacity-64 |
| Status(processing·진행) | status-processing-normal / -strong / -subtle | green-60 / green-70 / green-5-opacity-64 |
| Status(completed·완료) | status-completed-normal / -strong / -subtle | cool-neutral-60 / -80 / cool-neutral-10-opacity-72 |
| Status(rejected·반려·오류) | status-rejected-normal / -strong / -subtle | red-50 / red-60 / red-5-opacity-64 |
| Line(brand) | line-brand-normal / -neutral / -alternative / -strong | clearBlue-60 (opacity 0/16/8/56%) |
| Line(normal) | line-normal / -neutral / -alternative / -strong | cool-neutral-70 (opacity 24/16/8/80%) |
| Material | dimmer-weak / -normal / -strong | common-100(black) (opacity 32/56/80%) |

> Status 토큰 이름은 pending(대기)/processing(처리중)/completed(완료)/rejected(반려)로, `CLAUDE.md`의 "디자인 도메인 규칙"에 채워 넣을 영수증 상태(전체/완료/처리중/작성중/중복)와 1:1로 대응하지 않는다. 실제 매핑은 Figma 컴포넌트에서 재확인이 필요하다 — 임의로 대응시키지 않았다.
>
> ⚠️ **구현 시 주의:** 위 표에서 "(opacity N%)"가 붙은 행(Line-brand, Line-normal, Material, Status의 -subtle)은 단색이 아니라 원본 atomic 색에 그 %만큼 불투명도를 얹은 값이다. Figma MCP(`get_design_context`)가 주는 참조 코드의 CSS 변수 fallback hex(예: `var(--color/line/normal/normal,#575e62)`)는 이 불투명도를 반영하지 않은 **원색 그대로**라서, 그대로 갖다 쓰면 실제보다 훨씬 진하게 나온다. 코드로 옮길 때는 반드시 `rgba(원색, opacity)` 형태로 변환할 것 — 실제로 이 문제로 `screen-phone-auth.html`의 Textfield 테두리가 과하게 진하게 나온 적이 있다.

### 1.3 Semantic (의미값) — Dark — `Color Token-Semantic (의미값) Dark` (node 2098:83095)

Light와 동일한 토큰 이름 구조를 그대로 쓰고, atomic 매핑만 다르다(예: `bg-primary` → cool-neutral-**100**, `label-primary-normal` → cool-neutral-**5**, `fg-brand-normal` → clearBlue-**50**). 다크모드 구현 계획이 생기면 이 표를 전체 옮겨 적을 것 — 현재는 Light 모드만 실제 컴포넌트에 쓰이고 있어 전체 로우를 옮기지 않았다.

### 1.4 ⚠️ 참고 — "Color" 원시 스와치 페이지(node 50:609)와의 불일치

Figma에는 위 `Color Token-Atomic`과 별도로 스와치 형태의 "Color" 페이지(50:609)가 있다. 같은 토큰 이름인데 값이 다르다 — 예: `Cool-Neutral/20`이 "Color" 페이지에는 `#D7DCE0`로 표시되지만 `Color Token-Atomic`과 실제 `get_variable_defs` 바인딩 값은 `#DEE3E7`이다. Cool Neutral 70~100, Red 램프 전체도 마찬가지로 다르다.

실제 컴포넌트가 참조하는 값(`get_variable_defs`로 조회한 라이브 Variable 값)은 `Color Token-Atomic` 쪽과 일치하므로, **이 문서는 `Color Token-Atomic`을 기준으로 삼았다.** "Color" 페이지는 8월 이후 갱신되지 않은 것으로 보인다 — Figma에서 두 페이지 중 무엇을 유지할지 정리가 필요하다(디자이너 확인 요망).

## 2. Typography

Figma "Typography" 섹션(node 38:110) 기준. 폰트: `Pretendard`. 사이즈별로 Regular/Medium/SemiBold/Bold 4중량을 제공하며, 굵기와 무관하게 행간·자간은 동일하다.

| Token | Size | Line Height | Letter Spacing |
|---|---|---|---|
| Display01 | 34 | 44 | -0.6 |
| Display02 | 32 | 42 | -0.6 |
| Display03 | 30 | 40 | -0.6 |
| Heading01 | 28 | 38 | -0.5 |
| Heading02 | 26 | 36 | -0.5 |
| Heading03 | 24 | 34 | -0.5 |
| Body01 | 22 | 32 | -0.4 |
| Body02 | 20 | 28 | -0.4 |
| Body03 | 18 | 26 | -0.4 |
| Body04 | 16 | 24 | -0.3 |
| Body05 | 15 | 22 | -0.3 |
| Body06 | 14 | 20 | -0.3 |
| Caption01 | 13 | 19 | -0.2 |
| Caption02 | 12 | 18 | -0.2 |
| Caption03 | 11 | 16 | -0.2 |

> 8월 버전에 있던 이상값 — Heading02/03가 둘 다 24px로 중복되던 것, Caption 일부(01/02/03 Bold 등)의 line-height가 38로 튀던 것 — 은 이번 조회에서 모두 해소되어 있다. 즉 Figma 쪽에서 정리된 것으로 보인다.

## 3. Elevation (신규) — node 459:18953

| 토큰 | 값 |
|---|---|
| Shadow-Low | drop-shadow, color #8686860A, blur 3, spread 10, offset (0,0) |
| Shadow-Medium | drop-shadow, color #86868652, blur 10, spread 0, offset (0,0) |
| Shadow-Strong | drop-shadow, color #868686CC, blur 12, spread 0, offset (0,0) |

## 4. Icon — node 91:1111

UI 아이콘은 16 / 20 / 24 / 28px(h) 4단계, 삽화형 "Graphic" 아이콘은 24 / 32 / 48 / 64 / 84px 5단계로 구성되어 있다. 개별 아이콘 글리프 목록은 이 문서에 전부 옮기지 않았다 — 필요한 아이콘은 그때그때 Figma에서 `Icon/이름/사이즈` 규칙으로 조회한다.

## 5. Layout — node 158:29966

### Grid
Figma에 `grid/16`, `grid/20` 두 개의 자리(빈 프레임)만 마련되어 있고, 컬럼 수·거터·마진 같은 실제 수치는 아직 채워지지 않았다. **확정된 그리드 스펙이 없다 — 임의로 만들지 않는다.**

### Dimmed(Material)
§1.2의 `dimmer-weak/normal/strong` 토큰(모두 common-100/검정 opacity 32/56/80%)을 오버레이 배경으로 쓰는 예시가 있다. 실제 정의는 §1.2 Material 항목을 따른다.

### Navigation / Chrome 컴포넌트
아래는 Figma "Layout" 프레임 안에 있고, 현재 보류 상태가 아닌(확정) 컴포넌트다.

**Status-bar** (161:30744) — Layout: h 44px(raw). Variant: `background` = Alternative | Secondary | Primary | Transparent, `label` = Black | White.

**Home-bar** (164:30923) — Variant: `background` = Alternative | Secondary | Transparent.

**Header** (166:3969) — h 56px 대. 다수 variant(Home/Back/Menu/Search 등) 보유.

**Tab-item** (207:11372) / **Tab-menu** (207:11114) — Tab-item을 여러 개 배치해 구성.

**Page-Title/large** (175:8777) — Symbol variant로 존재. 세부 padding/typography는 8월 버전 기록(px `Padding/24` py `Padding/16`, 타이틀 Body01/Semibold)을 참고하되, 색상 hex는 §1.2 시맨틱 표 기준으로 다시 확인할 것.

## 6. Button — node 165:19713

**Button-solid** — Variant: `Color` = Primary | Assistive, `Variant` = Solid | Outlined, `Size` = Large | Medium | Small | **Xsmall(신규)**, `State` = Normal | Selected | Disabled.
- Xsmall 실측(1756:45131): h 34px, px `Padding/14` py `Padding/8`, radius `Radius/10`, icon 16px, gap 4px(raw), 텍스트 Body06/Semibold(14/20).
- Large/Medium/Small의 padding·radius·아이콘 크기는 8월 버전 기록과 구조상 동일 확인(h 56/48/40, radius 14/12/10 등) — 정확한 hex만 §1.2 기준으로 다시 참조할 것.
- Primary/Solid bg는 `color-semantic-fg-brand-normal`(clearBlue-60, #2A7FEC) — 이 값은 8월 이후 변하지 않았다.

**Button-icon** (165:20132) — Variant: `color` = Assistive | Primary, `shape` = Box | Round, `size` = Large | Medium | Small, `state` = Normal | Selected | Disabled. 구조는 8월 기록과 동일 확인.

**Button-text** (183:19951) — Variant: `size` = XS | S | M | L, `status` = Normal | Disabled | **Alternative(신규 확인)**, leading/trailing icon 옵션.

## 7. Textfield — node 165:18856

**Textfield** (165:18907) — 구조는 8월 기록과 동일 확인(Status/Active/Focus/Disable/Trailing Button variant, h 56px, radius `Radius/16`). 색상은 §1.2 기준 재확인 필요.

**Textinput-Resource-textfield-button** (165:18863), **Textinput-Resource-Textfield-Trailing Content** (165:18896) — 8월 기록과 구조 동일 확인.

**Program-select** (635:15003, 신규) — 그동안 없던 **Select/Dropdown류 컴포넌트**.
- `state` = Close | open | Dropdown-list.
- Close/open: 라벨(Body05/Bold 15/22, `color-semantic-label-secondary-normal`) + 필수 표시(`*`, 빨강) + Input(h 56px, radius `Radius/16`, border `color-semantic-line-normal-normal`(닫힘) / `color-semantic-fg-brand-normal`(열림)) + chevron-down/up 아이콘.
- Dropdown-list: 위 Input 아래로 목록(테두리 `color-semantic-fg-brand-normal`, radius `Radius/16`, h 256px, 스크롤바 포함).

**Dropdown-item** (1084:30439, 신규) — Program-select의 목록 한 줄. `status` = Dropdown-item-default | -pressed | -selected. h 56px, padding `Padding/12`. selected/pressed는 bg `color-atomic-brand-clearblue-5`(#EFF8FF), 텍스트는 default가 `label-primary-weak`, pressed가 `label-primary-disabled`, selected가 `label-primary-normal`.

## 8. Check-box — node 364:10667

**Check-box/24** (336:14128, 단일 체크박스) — 8월 기록과 구조 동일 확인.

**Check-box** (299:7842, "전체동의" 카드형) — 8월 기록과 구조 동일 확인.

**Check-box/item** (306:15060) — 8월 기록과 구조 동일 확인.

## 9. Date-picker — node 239:13371

**Date-picker**("Calendar") — 8월 기록과 구조 동일 확인(w 335 h 318, radius `Radius/20`).

**Date-picker/Selectbox** (300:1493), **Calendar-Item** (300:9351) — 8월 기록과 구조 동일 확인.

## 10. Bottom-sheet — node 307:9223

기본 구조(Header + Action-area 조합)는 8월 기록과 동일 확인. 단, 8월 문서가 근거로 삼았던 구체 preset 인스턴스(`datepicker-error`, node 336:13520)는 이번 조회에서 **더 이상 찾을 수 없었다** — 삭제되었거나 다른 node로 옮겨진 것으로 보인다. 재확인 필요.

## 11. Badge — node 324:9408

**Content-Badge** (324:9396, 색상 배지) — 8월 기록과 구조 동일 확인(`color` = Blue/Gray/Green/Red/Orange, `size` = Small/Medium).

**Content-Badge** (375:8105, 카드 종류 배지) — 8월 기록과 구조 동일 확인.

**Chip/Date-filter** (207:11770) — `Type=Preset`, `State` = Default | Selected. 정확한 상위 프레임(현재 Figma 캔버스 좌표상 Badge/Card 인접 그룹으로 추정) 확인이 매끄럽지 않았다 — 재확인 권장. 구조 자체는 8월 기록과 동일.

> Banner-status(8월 문서 node 324:10124)는 이번 조회에서 찾을 수 없었다 — 삭제/이동 여부 확인 필요.

## 12. Card — node 324:9692

Card 상위 프레임 존재는 확인했으나, 8월 문서가 다뤘던 Card-Item/Receipt의 구체 variant(완료/중복 등 상태 포함형)는 이번 회차에서 개별 재조회하지 않았다 — 재사용 전 Figma에서 최신 상태를 확인할 것.

## 13. Image-input — node 354:19324

**Image-input**("Input-receipt-image") — 8월 기록과 구조 동일 확인.

**Image-viewer-343*140** (1456:23785, 신규) — Image-input 계열의 343×140 이미지 뷰어. 세부 스펙은 미조회 — 필요 시 Figma에서 추가 확인.

## 14. Progress (신규) — node 2112:92010

**Progress-bar** (427:17502) — `progress` = Step-1 | Step-2 | Step-3. 트랙 w 212px h 6px, radius `Radius/999`(pill), bg `color-atomic-cool-neutral-15`(#EBEEF0 — foreground/disabled-subtle). Indicator bg `color-semantic-fg-brand-normal`(#2A7FEC), 폭이 Step에 따라 71 / 141 / 212px로 증가.

## 15. Modal/Tooltip (신규) — node 614:12775

**Modal** (614:12076) — 그동안 DESIGN.md/`design-system-test.html`에 없다고 명시했던 **Dialog/Modal 컴포넌트**가 여기에 해당한다.
- Variant: `type` = One-button | Two-button, `variant` = Normal | Strong | Wide, boolean `description`.
- 공통: w 343px, bg `color-atomic-cool-neutral-5`(#F7F8F9), radius `Radius/20`, drop-shadow(Shadow-Medium 계열), pt `Padding/36`.
- Title: Body03/Bold(18/26) `color-semantic-label-primary-normal`(#222426), 중앙 정렬. Description(옵션): Body04/Medium(16/24) `color-semantic-label-primary-alternative`(#A2A9AE).
- 버튼 영역: One-button/Normal은 버튼 1개(브랜드 Solid, h52 radius14). Two-button/Normal·Wide는 Outlined 버튼(흰 배경, border `color-semantic-line-normal-normal`) + Solid 버튼(브랜드) 나열. Two-button/Strong은 브랜드 Solid 버튼 아래 텍스트 버튼(Body04/Semibold, `label-secondary-normal`)을 세로로 배치.

**List-item** (922:17832) — Modal/Tooltip 카테고리 안에 있는 목록 항목형 컴포넌트. 세부 스펙은 미조회 — 필요 시 추가 확인.

## 16. Action-Area — node 183:20022

**Action-Area** (183:20022, "Frame 1707483779") — 8월 기록과 구조 동일 확인(Main/Alternative/Sub Action + Home-bar 조합).

**Action-area** (196:7993, 별개 컴포넌트셋) — 8월 기록과 구조 동일 확인(`type`=One/Two-button, `color`=White/Default, `variant`=Strong/Neutral/Normal/Wide). Main Action bg `color-semantic-fg-brand-normal`(#2A7FEC)은 변하지 않았다.

## 17. 컴포넌트 명명 규칙 참고

Figma 원본에 아래와 같은 오타/불일치가 있다 — 그대로 두었다(임의 수정하지 않음): `Coporate-card`(Corporate 오타), `Chekced`(Checked 오타), `skyBlu`(skyBlue 오타, 일부 토큰에만 존재), `Colse-Title-left`(Close 오타, Header 컴포넌트 — 8월 문서 기록, 이번 회차 재확인 안 함).
