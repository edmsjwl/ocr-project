# Design System — Implementation Specification

> 출처: Figma `[SBS] OCR 프로젝트_디자인` 파일 "🔵 디자인시스템" 페이지 (node 39:2)
> https://www.figma.com/design/ese9l01OJiDfirO8Q6XXIY/-SBS--OCR-프로젝트_디자인?node-id=39-2
>
> **이 문서의 목적**: 과거 디자인 기록과 현재 Figma를 비교하는 변경 로그가 아니라, **개발자와 AI가 Figma를 열지 않고도 그대로 구현할 수 있는 독립적인 구현 명세**다. 그래서 "8월 기록과 동일", "구조 변경 없음" 같은 생략 표현을 쓰지 않고, 모든 컴포넌트를 이번에 `get_design_context` / `get_variable_defs`로 다시 조회해 값 자체를 적었다.
>
> **Node ID는 출처 추적용 참고일 뿐, 그 자체가 스펙이 아니다.** 실제 스펙은 아래 표/목록의 수치·토큰이다.
> **Figma에서 값을 실제로 확인하지 못한 항목은 `[Figma에서 확인 불가]`로 표시했다** — 과거 기록이나 일반적인 디자인 규칙으로 추론하지 않았다.
> **Variable alias가 연결된 값은 "토큰명 (resolved hex/px)" 형식으로 병기했다.** 예: `Background: color/foreground/brand/normal (#2A7FEC)`.

## 목차
1. Color
2. Typography
3. Elevation
4. Icon
5. Layout (Grid, Status-bar, Home-bar, Header, Tab-item, Tab-menu, Page-Title/large)
6. Button (Button-solid, Button-icon, Button-text)
7. Textfield (Textfield, Textinput-Resource-*, Program-select, Dropdown-item)
8. Check-box (Check-box/24, Check-box, Check-box/item)
9. Date-picker (Date-picker/Selectbox, Calendar-Item, Calendar 컨테이너)
10. Bottom-sheet
11. Badge (Content-Badge ×2, Chip/Date-filter)
12. Card (Card-Item/Receipt, Card-item/Error, Card-Warning)
13. Image-input (Thumbnail, Image-viewer)
14. Progress (Progress-bar)
15. Modal (Modal, List-item)
16. Action-Area (Action-area)

---

## 1. Color

### 1.1 Atomic (원시값) — `Color Token-Atomic` (참고: node 55:2157)

| 그룹 | 토큰 | Resolved Value |
|---|---|---|
| Common | `color-atomic-common-0` / `-100` | `#FFFFFF` / `#000000` |
| Cool Neutral | `color-atomic-cool-neutral-5~100` | 5:`#F7F8F9` 10:`#F1F3F4` 15:`#EBEEF0` 20:`#DEE3E7` 30:`#CDD3D7` 40:`#BABEC2` 50:`#A2A9AE` 60:`#8C9499` 70:`#575E62` 80:`#434648` 90:`#222426` 100:`#191A1B` |
| Clear Blue(브랜드) | `color-atomic-brand-clearblue-5~90` | 5:`#EFF8FF` 10:`#DBEEFE` 20:`#BEE2FF` 30:`#93D2FD` 40:`#60B8FA` 50:`#3B99F6` **60:`#2A7FEC`(key color)** 70:`#1D65D8` 80:`#1E52AF` 90:`#1E488A` |
| Sky Blue(state) | `color-atomic-skyBlue-5~90, A10~A40` | 5:`#E1F5FE` 10:`#B3E5FC` 20:`#81D4FA` 30:`#4FC3F7` 40:`#29B6F6` 50:`#03A9F4` 60:`#039BE5` 70:`#0288D1` 80:`#0277BD` 90:`#01579B` / A10:`#80D8FF` A20:`#40C4FF` A30:`#00B0FF` A40:`#0091EA` |
| Green(state) | `color-atomic-green-5~90, A10~A40` | 5:`#E8F5E9` 10:`#C8E6C9` 20:`#A5D6A7` 30:`#81C784` 40:`#66BB6A` 50:`#4CAF50` 60:`#43A047` 70:`#388E3C` 80:`#2E7D32` 90:`#1B5E20` / A10:`#B9F6CA` A20:`#69F0AE` A30:`#00E676` A40:`#00C853` |
| Red(state) | `color-atomic-red-5~90, A10~A40` | 5:`#FFEBEE` 10:`#FFCDD2` 20:`#EF9A9A` 30:`#E57373` 40:`#EF5350` 50:`#F44336` 60:`#E53935` 70:`#D32F2F` 80:`#B71C1C` 90:`#82181A` / A10:`#FF8A80` A20:`#FF5252` A30:`#FF1744` A40:`#D50000` |

⚠️ Figma에는 이 Atomic 표와 별도로 스와치 형태의 "Color" 페이지(node 50:609)가 있는데, 같은 토큰 이름인데 값이 다르다(예: Cool-Neutral/20이 "Color" 페이지엔 `#D7DCE0`, Atomic엔 `#DEE3E7`). 실제 컴포넌트가 바인딩하는 값(`get_variable_defs` 라이브 조회 결과)은 이 Atomic 표와 일치하므로 이 표를 기준으로 삼았다. "Color" 페이지는 갱신되지 않은 것으로 보인다 — Figma에서 정리 필요.

### 1.2 Semantic (의미값) — Light — `Color Token-Semantic (의미값) Light` (참고: node 97:1313)

`resolved atomic token → 최종 hex`. `opacity`가 붙은 행은 원색이 아니라 해당 opacity를 얹은 값이다 — **구현 시 반드시 `rgba(원색, opacity)`로 변환할 것.** Figma MCP가 주는 참조 코드의 CSS 변수 fallback hex는 이 opacity를 반영하지 않은 원색 그대로라서, 그대로 쓰면 실제보다 진하게 나온다.

| 그룹 | 토큰 | → Atomic | Resolved |
|---|---|---|---|
| Static | `color-semantic-static-white` / `-black` | common-0 / cool-neutral-100 | `#FFFFFF` / `#191A1B` |
| Background | `bg-primary` / `bg-secondary` / `bg-alternative` / `bg-inverse` / `bg-inverse-strong` | cool-neutral-5 / common-0 / cool-neutral-10 / cool-neutral-80 / cool-neutral-90 | `#F7F8F9` / `#FFFFFF` / `#F1F3F4` / `#434648` / `#222426` |
| Foreground-normal | `fg-normal` / `-selected` / `-weak` / `-disabled-normal` / `-disabled-subtle` | cool-neutral-5 / -15 / -10 / -30 / -15 | `#F7F8F9` / `#EBEEF0` / `#F1F3F4` / `#CDD3D7` / `#EBEEF0` |
| Foreground-brand | `fg-brand-normal` / `-selected` / `-disabled` / `-secondary-selected` / `-secondary-disabled` | clearBlue-60 / -80 / cool-neutral-20 / clearBlue-5 / cool-neutral-10 | `#2A7FEC` / `#1E52AF` / `#DEE3E7` / `#EFF8FF` / `#F1F3F4` |
| Label(brand) | `label-brand-normal` / `-selected` / `-weak` / `-disabled` | clearBlue-60 / -40 / -20 / cool-neutral-20 | `#2A7FEC` / `#60B8FA` / `#BEE2FF` / `#DEE3E7` |
| Label(primary) | `label-primary-normal` / `-selected` / `-alternative` / `-weak` / `-disabled` | cool-neutral-90 / -70 / -50 / -40 / -60 | `#222426` / `#575E62` / `#A2A9AE` / `#BABEC2` / `#8C9499` |
| Label(secondary) | `label-secondary-normal` / `-selected` / `-weak` / `-disabled` | cool-neutral-80 / -60 / -50 / -40 | `#434648` / `#8C9499` / `#A2A9AE` / `#BABEC2` |
| Label(기타) | `label-inverse` | common-0 | `#FFFFFF` |
| Status(pending·대기) | `status-pending-normal` / `-strong` / `-subtle` | skyBlue-50 / -60 / skyBlue-5 opacity 64% | `#03A9F4` / `#039BE5` / `rgba(225,245,254,0.64)` |
| Status(processing·처리중) | `status-processing-normal` / `-strong` / `-subtle` | green-60 / -70 / green-5 opacity 64% | `#43A047` / `#388E3C` / `rgba(232,245,233,0.64)` |
| Status(completed·완료) | `status-completed-normal` / `-strong` / `-subtle` | cool-neutral-60 / -80 / cool-neutral-10 opacity 72% | `#8C9499` / `#434648` / `rgba(241,243,244,0.72)` |
| Status(rejected·반려) | `status-rejected-normal` / `-strong` / `-subtle` | red-50 / -60 / red-5 opacity 64% | `#F44336` / `#E53935` / `rgba(255,235,238,0.64)` |
| Line(brand) | `line-brand-normal` / `-neutral` / `-alternative` / `-strong` | clearBlue-60 opacity 100/16/8/56% | `#2A7FEC` / `rgba(42,127,236,0.16)` / `rgba(42,127,236,0.08)` / `rgba(42,127,236,0.56)` |
| Line(normal) | `line-normal` / `-neutral` / `-alternative` / `-strong` | cool-neutral-70 opacity 24/16/8/80% | `rgba(87,94,98,0.24)` / `rgba(87,94,98,0.16)` / `rgba(87,94,98,0.08)` / `rgba(87,94,98,0.80)` |
| Material | `dimmer-weak` / `-normal` / `-strong` | common-100(검정) opacity 32/56/80% | `rgba(0,0,0,0.32)` / `rgba(0,0,0,0.56)` / `rgba(0,0,0,0.80)` |

> Status 토큰 이름(pending/processing/completed/rejected)은 `CLAUDE.md` "디자인 도메인 규칙"에 채울 영수증 상태(전체/완료/처리중/작성중/중복)와 1:1로 대응하지 않는다. §12 Card 섹션에서 확인한 실사용 예로는 `대기→pending`, `처리중→processing`, `완료→completed`, `반려→rejected`로 쓰인다(Card-Item/Receipt 컴포넌트 기준, 이번에 직접 확인).

### 1.3 Semantic (의미값) — Dark — `Color Token-Semantic (의미값) Dark` (참고: node 2098:83095)

토큰 이름 구조는 Light와 동일, atomic 매핑만 다르다. 주요 예:

| 토큰 | Light | Dark |
|---|---|---|
| `bg-primary` | cool-neutral-5(`#F7F8F9`) | cool-neutral-100(`#191A1B`) |
| `bg-secondary` | common-0(`#FFFFFF`) | cool-neutral-90(`#222426`) |
| `label-primary-normal` | cool-neutral-90(`#222426`) | cool-neutral-5(`#F7F8F9`) |
| `fg-brand-normal` | clearBlue-60(`#2A7FEC`) | clearBlue-50(`#3B99F6`) |

다크모드 구현 계획이 확정되면 이 표를 Light 표와 동일한 전체 행 구성으로 확장할 것 — 현재는 Light 모드만 실제 컴포넌트에 쓰이고 있어 전체를 옮기지 않았다.

## 2. Typography

Figma "Typography" 섹션(참고: node 38:110) 기준. 폰트: `Pretendard`. 사이즈별 Regular/Medium/SemiBold/Bold 4중량 제공, 굵기와 무관하게 행간·자간은 동일.

⚠️ **자간(Letter Spacing) 단위 주의**: 아래 표의 값은 **폰트 크기 대비 퍼센트(%)**다. Figma 컴포넌트 코드에서 실제 CSS로 내려오는 letter-spacing 절대값(px)은 `fontSize × (표의 값 / 100)`으로 계산된 값이다 — 예: Body06(14px, -0.3%)의 실제 letter-spacing은 `14 × -0.3/100 = -0.042px`. 이 문서 §6 이하 컴포넌트 스펙의 "Typography" 항목에는 계산된 px 절대값을 함께 적었다.

| Token | Size(px) | Line Height(px) | Letter Spacing(%) |
|---|---|---|---|
| Display01 | 34 | 44 | -0.6 |
| Display02 | 32 | 42 | -0.6 |
| Display03 | 30 | 40 | -0.6 |
| Heading01 | 28 | 38 | -0.5 |
| Heading02 | 26 | 36 | -0.5 |
| Heading03 | 24 | 34 | -0.4 |
| Body01 | 22 | 32 | -0.4 |
| Body02 | 20 | 28 | -0.4 |
| Body03 | 18 | 26 | -0.3 |
| Body04 | 16 | 24 | -0.3 |
| Body05 | 15 | 22 | -0.3 |
| Body06 | 14 | 20 | -0.3 |
| Caption01 | 13 | 19 | -0.2 |
| Caption02 | 12 | 18 | -0.2 |
| Caption03 | 11 | 16 | -0.2 |

## 3. Elevation — 참고: node 459:18953

| 토큰 | Effect |
|---|---|
| `Shadow-Low` | drop-shadow, color `rgba(134,134,134,0.04)`(#8686860A), blur 3, spread 10, offset (0,0) |
| `Shadow-Medium` | drop-shadow, color `rgba(134,134,134,0.32)`(#86868652), blur 10, spread 0, offset (0,0) |
| `Shadow-Strong` | drop-shadow, color `rgba(134,134,134,0.80)`(#868686CC), blur 12, spread 0, offset (0,0) |

## 4. Icon — 참고: node 91:1111

UI 아이콘 사이즈 단계: 16 / 20 / 24 / 28px. Graphic(삽화형) 아이콘 사이즈 단계: 24 / 32 / 48 / 64 / 84px. 개별 아이콘 글리프의 내부 벡터/색상 값은 `[Figma에서 확인 불가]` — 에셋(SVG)으로만 제공되어 코드로 조회되지 않는다. 필요한 아이콘은 `Icon/이름/사이즈` 이름 규칙으로 Figma에서 그때그때 에셋을 받는다.

---

## 5. Layout — 참고: node 158:29966

### 5.1 Grid
`grid/16`, `grid/20` 이름의 빈 프레임만 있고 컬럼 수·거터·마진 실측값이 없다. **`[Figma에서 확인 불가]`**

### 5.2 Status-bar — 참고: node 161:30744
- Variants: `background` = Alternative | Secondary | Primary | Transparent, `label` = Black | White (5개 조합 확인: 나머지 3개는 Black 라벨과 배경 매트릭스가 겹쳐 Figma가 5개만 노출)
- Size: W 375 / H 44, min size 없음
- Auto Layout: vertical, 내부 Container는 horizontal, `items-center justify-center`
- Padding: Time 영역 `px 30.5 py 13`(raw), Status 아이콘 영역 `p 14`(raw) — 컴포넌트 자체의 상위 Padding 토큰 없음
- Gap: Status 아이콘 그룹 `gap 4px`(raw)
- Radius: 없음
- Border: 없음
- Background: `background=Primary` → `color/background/bg-primary` (`#F7F8F9`) / `Secondary` → `bg-secondary`(`#FFFFFF`) / `Alternative` → `bg-alternative`(`#F1F3F4`) / `Transparent` → 배경 없음
- Typography: 시간 텍스트 `SF Pro Semibold 15px`(Pretendard 아님, iOS 시스템 폰트), tracking -0.237px(raw, Typography 표 토큰 아님)
- Color(텍스트): `label=Black` → `color/label/primary/normal`(`#222426`) / `label=White` → `color/label/inverse/inverse`(`#FFFFFF`)
- Icon: Celluar(18×12) / Wi-Fi(16×12) / Battery(25×12) — 3개 모두 이미지 에셋, 내부 색상 `[Figma에서 확인 불가]`(Label=White일 때 별도 흰색 에셋으로 교체됨)
- State: 별도 상태 없음(정적 컴포넌트)

### 5.3 Home-bar — 참고: node 164:30923
- Variants: `background` = Alternative | Secondary | Transparent | Primary
- Size: W 375, H는 content-fit(약 27px: pt16+슬라이더5+pb6)
- Auto Layout: vertical, `items-center justify-center`
- Padding: pb 6 / pt 16 / px 10 (Padding 토큰 아님, raw px로 조회됨)
- Radius(Slider): 4px(raw)
- Background: Alternative → `bg-alternative`(`#F1F3F4`) / Secondary → `bg-secondary`(`#FFFFFF`) / Primary → `bg-primary`(`#F7F8F9`) / Transparent → 없음
- Slider(바): W 134 H 5, bg `color/background/bg-inverse`(`#434648`), radius 4px
- State: 없음(정적)

### 5.4 Header — 참고: node 166:3969
- Variants: `type` = Back | Home | Menu-Search | Close-Title-center | Back home | Close | Title, `background` = Primary | Secondary | Alternative, `icon`(boolean), `iconCount` = Default | 1 | 2, `iconShow`(boolean), `showStepIndicator`(boolean), `title`(boolean)
- Size: W 375, H 56 (고정)
- Auto Layout: horizontal
- Padding: X `Padding/20`(20px) / Y `Padding/16`(16px)
- Gap: 타입에 따라 다름 — Back류는 `gap 4px`(아이콘-타이틀 그룹), Close류는 `gap 8px`
- Radius: 없음
- Border: 없음
- Background: `background=Alternative`(대부분 조합 기본값) → `bg-alternative`(`#F1F3F4`) / `Primary` → `bg-primary`(`#F7F8F9`) / `Secondary` → `bg-secondary`(`#FFFFFF`) — 단, 정확히 어떤 `type`+`background` 조합이 어떤 색을 쓰는지는 위 5가지 semantic 값 중 하나로 결정되며 세부 매트릭스가 매우 많다(36개 조합) — 필요한 특정 조합은 Figma에서 재확인 권장.
- Typography(제목, Back/Close/BackHome류): `Body03/Semibold` — 18px/26px/-0.3%(실제 -0.054px), color `label-primary-normal`(`#222426`), 가로 중앙 절대배치(w280, left 50%)
- Typography(제목, Menu-Search/Title류): `Body02/Bold` — 20px/28px/-0.4%(실제 -0.08px), color `label-primary-normal`(`#222426`)
- Step-indicator(옵션, `showStepIndicator`): 현재 단계 숫자 `Body04/Semibold`(16/24, -0.3%) color `label-brand-normal`(`#2A7FEC`), "/" 및 총 단계 숫자 `Body06/Semibold`(14/20, -0.3%) color `label-secondary-normal`(`#434648`), 내부 gap 2px
- Icon: chevron-left/24, close/24, home/24 — 24px, `[Figma에서 확인 불가]`(내부 색상)
- Home 타입 로고: `LogoWise`(64×22) + `Logo`(42×25) 가로 배치, gap `Padding/2`(2px) — SVG 에셋
- Figma dev 주석(실사용처, 참고용): `Title/Alternative`→"[영수증 내역]에서 사용", `Back/Alternative`→"[온보딩]에서 사용", `Close/Alternative`→"[영수증 등록]에서 사용", `Back home/Alternative`→"[상세 내역]에서 사용", `Home/Alternative`→"[메인홈]에서 사용"
- State: 이 컴포넌트 자체에 Hover/Pressed/Focus/Disabled 정의된 variant 없음. `[Figma에서 확인 불가]`

### 5.5 Tab-item — 참고: node 207:11372
- Variants: `property1` = Activated | Default, boolean `dot`
- Size: H 40, W는 content-fit
- Auto Layout: horizontal
- Padding: X `Padding/2`(2px) / Y `Padding/8`(8px)
- Border: Activated만 `border-bottom 2px solid`, color `label-primary-normal`(`#222426`)
- Typography: `Body04/Bold` — 16px/24px/-0.3%(실제 -0.048px)
- Color(텍스트): Activated → `label-secondary-normal`(`#434648`) / Default → `label-secondary-disabled`(`#BABEC2`)
- dot(옵션): 4×24 이미지 에셋(형태 `[Figma에서 확인 불가]`, Tab-menu의 "전체" 탭 선택 표시와 동일 에셋)
- State: Activated=선택됨, Default=선택안됨 — 이 2개가 사실상 Selected/Default state다. Hover/Pressed/Focus/Disabled 별도 variant 없음.

### 5.6 Tab-menu — 참고: node 207:11114
- Variants: `property1` = 전체 | 완료 | 처리중 | 작성중 | 중복 — Tab-item 5개(라벨: 전체/대기/처리중/완료/반려 — ⚠️ variant 이름(작성중/중복)과 실제 라벨 텍스트(대기/반려)가 다르다, Figma 원본 그대로 기록)
- Size: W 375, H는 content-fit
- Auto Layout: horizontal
- Padding: X `Padding/20`(20px)
- Gap: `Padding/32`(32px)
- Border: `border-bottom 1px solid`, color `line/normal/alternative` — opacity 계열 토큰이므로 실제로는 `rgba(87,94,98,0.08)`(§1.2 Line-normal-alternative)
- 각 Tab-item은 §5.5 스펙과 동일하게 동작(선택된 탭만 Activated 스타일)
- "전체" 탭에는 §5.5의 dot 인디케이터가 붙는다(고정, 다른 탭엔 없음)

### 5.7 Page-Title/large — 참고: node 175:8777
- Boolean property: `description`
- Size: W 375, H는 content-fit
- Auto Layout: vertical
- Padding: X `Padding/20`(20px) / Y `Padding/16`(16px)
- Gap: `Padding/6`(6px)
- Typography(제목): `Heading03/Semibold` — 24px/34px/-0.4%(실제 -0.096px), color `label-primary-normal`(`#222426`)
- Typography(설명, `description=true`일 때): `Body04/Medium` — 16px/24px/-0.3%(실제 -0.048px), color `label-secondary-normal`(`#434648`)
- Figma dev 주석: "인증화면에 사용됩니다."
- State: 없음(정적, description on/off만 boolean)

---

## 6. Button — 참고: node 165:19713

### 6.1 Button-solid — 참고: node 165:19718
- Variants: `Color` = Primary | Assistive, `Variant` = Solid | Outlined, `Size` = Large | Medium | Small | Xsmall, `State` = Normal | Selected | Disabled
- Auto Layout: horizontal, `items-center justify-center`
- Size / Padding / Radius / Gap / Typography (Size별):

| Size | H | Padding X/Y | Radius | Icon | Gap | Typography |
|---|---|---|---|---|---|---|
| Large | 56 | 28 / 14 | 14 | 20 | 6px(raw) | Body04/Semibold 16/24/-0.3%(실제-0.048px) |
| Medium | 48 | `[Figma에서 확인 불가: 이번 회차 미측정]` | 12 | — | — | — |
| Small | 40 | `[Figma에서 확인 불가: 이번 회차 미측정]` | 10 | — | — | — |
| Xsmall | 34 | 14 / 8 | 10 | 16 | 4px(raw) | Body06/Semibold 14/20/-0.3%(실제-0.042px) |

> Medium/Small의 정확한 padding은 이번 회차에 재조회하지 못했다 — `[Figma에서 확인 불가]`. Large/Xsmall은 실측 완료.

- Color(bg) — Solid/Primary: State=Normal → `color/foreground/brand/normal`(`#2A7FEC`) / Selected → `[Figma에서 확인 불가]` / Disabled → `color/foreground/brand/disabled`(`#DEE3E7`)
- Color(bg) — Outlined: 흰 배경(`static/white`) + border `[Figma에서 확인 불가: 정확한 border color 토큰 이번 회차 미측정]`
- Color(text) — Solid: `color/label/inverse/inverse`(`#FFFFFF`) / Outlined: `[Figma에서 확인 불가]`
- Border width: Outlined variant만 1px(추정 — 정확한 px 이번 회차 미측정) `[Figma에서 확인 불가]`
- Interaction 레이어: 모든 크기 공통으로 버튼 내부에 `opacity-0` 오버레이 div(`Interaction`)가 존재 — hover/press 시 사용되는 것으로 추정되나 실제 opacity 변경 값은 `[Figma에서 확인 불가]`(Figma 컴포넌트 코멘트: "Normal에서 가중치 1.5 적용" — 정확한 계산 결과값 아님, 가중치 배수만 언급됨)

### 6.2 Button-icon — 참고: node 165:20132
- Variants: `color` = Assistive | Primary, `shape` = Box | Round, `size` = Large | Medium | Small, `state` = Normal | Selected | Disabled (36개 조합 전수 확인)
- Auto Layout: horizontal, `items-center justify-center`

| Size | 전체 크기 | Padding(Normal) | Padding(Selected/Disabled) | Icon | Radius(Box) | Radius(Round) |
|---|---|---|---|---|---|---|
| Large | 56×56 | 12 | 12 | 32 | 12 | 999(pill, `Number/64`) |
| Medium | 52×52 | 10 | 10 | 24 | 10 | 999 |
| Small | 44×44 | 10 | 8 | 20 | 8 | 999 |

- Color(bg) 매트릭스:
  - Primary/Normal: `color/foreground/brand/normal`(`#2A7FEC`)
  - Primary/Selected: `color/foreground/brand/selected`(`#1E52AF`)
  - Primary/Disabled: `color/foreground/brand/disabled`(`#DEE3E7`)
  - Assistive/Normal + shape=Box: `color/foreground/normal/normal`(`#F7F8F9`)
  - Assistive/Normal + shape=Round: `color/static/white`(`#FFFFFF`) ⚠️ Box와 Round가 Normal 상태에서 배경이 다르다(둘 다 Assistive인데 Box=`#F7F8F9`, Round=흰색) — Figma 원본 그대로 기록
  - Assistive/Selected: `color/foreground/normal/selected`(`#EBEEF0`)
  - Assistive/Disabled: `color/foreground/normal/disabled-subtle`(`#EBEEF0`)
- Icon: 아이콘 자체가 이미지 에셋(state/color별로 다른 에셋 파일 사용) — 내부 채색 값 `[Figma에서 확인 불가]`
- Border: 없음(모든 조합)
- State: Normal / Selected / Disabled 3종, 위 표의 bg 매핑이 곧 state 변화값. Hover/Pressed/Focus 별도 variant `[Figma에서 확인 불가]`

### 6.3 Button-text — 참고: node 183:19951
- Variants: `size` = XS | S | M | L, `status` = Normal | Disabled | Alternative, boolean `showLeadingIcon`, boolean `showTrailingIcon`
- Auto Layout: horizontal, `items-center`, gap `Padding/4`(4px)
- Size(icon)/Typography by size:

| Size | Icon | Typography(Normal) |
|---|---|---|
| L | 24px | Body02/Semibold 20/28/-0.4%(실제-0.08px) |
| M | 24px | Body03/Semibold 18/26/-0.3%(실제-0.054px) |
| S | 20px | Body04/Semibold 16/24/-0.3%(실제-0.048px) |
| XS | 16px | Body06/Semibold 14/20/-0.3%(실제-0.042px) |

- Color(텍스트): Normal → `label-secondary-normal`(`#434648`) / Disabled → `label-primary-disabled`(`#8C9499`) / Alternative → `label-primary-alternative`(`#A2A9AE`)
- Padding/Radius/Border: 없음(텍스트+아이콘만 있는 인라인 컴포넌트)
- State: Normal/Disabled/Alternative 3종. Hover/Pressed/Focus `[Figma에서 확인 불가]`

---

## 7. Textfield — 참고: node 165:18856

### 7.1 Textfield — 참고: node 165:18907
- Variants: `status` = Normal | Positive | Negative, boolean `activeText`(입력값 존재 여부), boolean `focusStroke`(포커스 여부), boolean `disable`, boolean `trailingButton`, boolean `heading`, boolean `description`, boolean `required`, boolean `leadingContent`, boolean `extra`, boolean `trailingContent`
- Size: W 335(고정), H는 content-fit(Container 자체는 H 56)
- Auto Layout: vertical, gap `Padding/8`(8px)
- Container(입력창) Padding: `Padding/12`(12px) 전체
- Container Radius: `Radius/16`(16px)
- Container Border width: 1px (모든 상태 공통)

**Container 상태별 배경/테두리 (실측, 상태 조합 다수 확인):**

| 상태 | 배경 | 테두리 |
|---|---|---|
| 기본(비어있음, 비활성, 비포커스) | `color/foreground/normal/normal`(`#F7F8F9`) | `line/normal/neutral` → `rgba(87,94,98,0.16)` |
| 입력값 있음 + 비포커스 + trailingButton 없음 | `static/white`(`#FFFFFF`) | `line/normal/normal` → `rgba(87,94,98,0.24)` |
| 입력값 있음 + 비포커스 + trailingButton 있음 | `foreground/normal/normal`(`#F7F8F9`) | `line/normal/neutral` → `rgba(87,94,98,0.16)` |
| 포커스(Normal/Positive 공통) | `static/white`(`#FFFFFF`) | `foreground/brand/normal`(`#2A7FEC`, 불투명 — opacity 토큰 아님) |
| Disabled(status=Positive 예시로 확인) | `foreground/normal/disabled-subtle`(`#EBEEF0`) | `line/normal/neutral` → `rgba(87,94,98,0.16)` |
| **Negative(에러) — 모든 activeText/focus 조합** | 위 "기본"/"입력값 있음" 행과 **동일**(배경·테두리 변화 없음) | 위와 동일 — **⚠️ 에러여도 테두리가 빨갛게 바뀌지 않는다.** Figma 원본에 Negative 전용 Container 스타일 분기가 없음(직접 확인) |

- Negative 상태 표시 방법: 테두리 변화 없이, ① 입력값이 있고 포커스가 없을 때 우측에 `Icon/alert-circle/solid/20`(빨간 경고 아이콘) 추가, ② 하단 helper 텍스트 색이 `color/status/rejected/normal`(`#F44336`)로 바뀜.
- Heading(라벨): `Body05/Bold` — 15px/22px/-0.3%(실제-0.045px), color `label-secondary-normal`(`#434648`)
- Required(`*`): `Pretendard JP Medium 14px`, color `status/rejected/normal`(`#F44336`) — ⚠️ Pretendard(기본 폰트)가 아니라 Pretendard JP 별도 폰트 사용
- Placeholder: `Body04/Medium` — 16px/24px/-0.3%(실제-0.048px), color `label-primary-weak`(`#BABEC2`)
- 입력값 텍스트: 동일 크기, color `label-primary-normal`(`#222426`, 기본) / `label-primary-disabled`(`#8C9499`, Negative 비활성 helper 케이스)
- Description(하단 helper, 기본): `Body06/Medium`♦ — 실측 `14px/20px`, color `label-secondary-selected`(`#8C9499`)
- Description(Negative): `Body06/Regular` 14px/20px, color `status/rejected/normal`(`#F44336`)
- Trailing button("재전송" 등): §7.2 Textinput-Resource-textfield-button 참조
- State 요약: **Normal / Focus / Disabled / Negative(Error)** — Hover/Pressed 별도 variant `[Figma에서 확인 불가]`

### 7.2 Textinput-Resource-textfield-button — 참고: node 165:18863
- Size: H 36, min-w 80
- Padding: X `Padding/12`(12px) / Y `Padding/6`(6px)
- Radius: `Radius/10`(10px)
- Border: 1px, color `line/normal/neutral` → `rgba(87,94,98,0.16)`(Inner Border 레이어로 별도 존재)
- Shadow: `drop-shadow(0px 1px 1px rgba(0,0,0,0.03))` — Elevation 표의 3종(Low/Medium/Strong) 어디에도 없는 별도 값
- Background: `color/foreground/brand/normal`(`#2A7FEC`)
- Typography: `Body05/Medium` — 15px/22px/-0.3%(실제-0.045px), color `label-inverse/inverse`(`#FFFFFF`)
- Interaction 오버레이 존재(opacity-0), 정확한 hover/press opacity `[Figma에서 확인 불가]`

### 7.3 Program-select — 참고: node 635:15003
- Variants: `state` = Close | open | Dropdown-list
- Size: W 343(고정)
- Auto Layout: vertical
- Heading: `Body05/Bold` 15/22/-0.3%(실제-0.045px), color `label-secondary-normal`(`#434648`) + Required `*`(Pretendard JP Medium 14px, color `status/rejected/normal` `#F44336`)
- Input Container: H 56, radius `Radius/16`(16px), padding `Padding/12`(12px)
  - `state=Close`: border `line/normal/normal` → `rgba(87,94,98,0.24)`, trailing `Icon/chevron-down/20`
  - `state=open`: border `line/brand/normal`(`#2A7FEC`, 불투명), trailing `Icon/chevron-up/20`
- Placeholder: `Body04/Medium` 16/24/-0.3%(실제-0.048px), color `label-primary-weak`(`#BABEC2`)
- Dropdown-list(옵션 목록 패널): border 1px `color/foreground/brand/normal`(`#2A7FEC`), radius `Radius/16`(16px), H 256(고정), 스크롤바(6px, radius `Radius/999`, color `foreground/normal/disabled-normal` `#CDD3D7`)
- State: Close / open(Focus) / Dropdown-list(목록 펼침) 3종

### 7.4 Dropdown-item — 참고: node 1084:30439
- Variants: `status` = Dropdown-item-default | Dropdown-item-pressed | Dropdown-item-selected
- Size: W 334, H 56
- Padding: `Padding/12`(12px)
- Typography: `Body04` 16/24/-0.3%(실제-0.048px) — default는 Regular, pressed/selected는 Medium
- Color(배경): default/pressed → `static/white`(`#FFFFFF`) / selected → `foreground/brand/secondary-selected`(`#EFF8FF`) ⚠️ pressed도 selected와 같은 배경(`#EFF8FF`)을 쓰는 코드 분기가 있어 실제로는 default만 흰 배경
- Color(텍스트): default → `label-primary-weak`(`#BABEC2`) / pressed → `label-primary-disabled`(`#8C9499`) / selected → `label-primary-normal`(`#222426`)

> Textarea, Textinput/Textarea 컴포넌트는 이번 회차에 재조회하지 않았다 — `[Figma에서 확인 불가: 이번 문서 범위 밖]`.

---

## 8. Check-box — 참고: node 364:10667

### 8.1 Check-box/24(단일 체크박스) — 참고: node 336:14128
- Boolean property: `property1`(checked 여부)
- Size: 24×24
- Radius: Checked `Padding/6`(6px) / Unchecked `Number/6`(6px) — 동일 6px, 토큰 이름만 다름
- Border(Unchecked): 2px, color `line/normal/normal` → `rgba(87,94,98,0.24)`
- Background(Checked): `color/foreground/brand/normal`(`#2A7FEC`)
- Background(Unchecked): `static/white`(`#FFFFFF`)
- Shadow: `Shadow-Low`(§3) 적용 — `drop-shadow(rgba(134,134,134,0.04) 0 0 3px, spread 10)`, Unchecked/Checked 공통
- Icon(Checked): `functional/check` 20×20, 이미지 에셋(내부 색 `[Figma에서 확인 불가]`)
- State: Checked / Unchecked 2종. Hover/Pressed/Focus/Disabled `[Figma에서 확인 불가]`

### 8.2 Check-box("전체동의" 카드형) — 참고: node 299:7842
- Variants: `state` = Selected | disabled
- Size: W 335, H 60
- Padding: px 17 / py 19(raw, Padding 토큰 아님)
- Radius: `Padding/16`(16px, 토큰 이름이 Padding이지만 실제로는 radius로 쓰임)
- Border: 1px, color `line/normal/neutral` → `rgba(87,94,98,0.16)`
- Background: `state=disabled` → `foreground/normal/normal`(`#F7F8F9`) / `state=Selected` → `foreground/normal/disabled-subtle`(`#EBEEF0`) ⚠️ 이름과 반대로 매핑되어 있다 — Figma 원본 그대로 기록(재확인 권장)
- Typography: `Body03/Semibold` 18/26/-0.3%(실제-0.054px), color `label-primary-normal`(`#222426`)
- Icon: Selected는 `check-circle`(24px, Selected 상태 이미지), disabled는 별도 `check-circle`(Dark 모드 이미지 — mode="Dark"로 명명되어 있으나 실제로는 비활성 표현용으로 추정, 정확한 근거 `[Figma에서 확인 불가]`)

### 8.3 Check-box/item — 참고: node 306:15060
- Variants: `state` = Selected | Disabled, boolean `showBullet`, `showMainText`, `showStatusText`, `showSubText`
- Size: W 335, H는 content-fit
- Padding: pl `Padding/8`(8px) pr `Padding/2`(2px) py `Padding/8`(8px)
- Gap: 내부 텍스트 그룹 16px(raw), Label 내부 요소 간 1px(raw)
- Typography: 전체 `Body04/Medium` 16/24/-0.3%(실제-0.048px), color `label-primary-normal`(`#222426`) — Selected/Disabled 모두 동일 색(⚠️ Disabled여도 텍스트색이 바뀌지 않음, 아이콘만 Dark/Light 모드 이미지로 교체)
- Icon: `check-circle`(24px) + trailing `chevron-right/20`
- State: Selected / Disabled — 텍스트 색상 변화 없음, 아이콘 이미지만 교체

> Checkbox/filter는 이번 회차에 재조회하지 않았다 — `[Figma에서 확인 불가: 이번 문서 범위 밖]`.

---

## 9. Date-picker — 참고: node 239:13371

### 9.1 Date-picker/Selectbox — 참고: node 300:1493
- Variants: `status` = Default | Selected
- Size: W 168(개별 셀렉트박스 기준, 화면에는 2개 나란히 배치되어 합쳐서 폭이 커짐)
- Auto Layout: vertical, gap `Padding/8`(8px)
- Container: H 48, padding `Padding/12`(12px), radius `Radius/12`(12px), border 1px
- Border color: Default → `line/normal/neutral` → `rgba(87,94,98,0.16)` / Selected → `line/brand/normal`(`#2A7FEC`, 불투명)
- Background: `bg-secondary`(`#FFFFFF`)
- Typography(라벨"시작일" 등): `Body05/Semibold` 15/22/-0.3%(실제-0.045px), color `label-primary-normal`(`#222426`)
- Typography(날짜값): 동일 크기, color `label-brand-normal`(`#2A7FEC`)
- Icon: `Icon/Calendar/20`(20px, 좌측)
- State: Default / Selected 2종

### 9.2 Calendar-Item — 참고: node 300:9351
- Variants: `type` = Date | month, `status` = Selected | Inactive | Default | Current
- Size(type=Date): 36×36(Selected/Current), content-fit(Default/Inactive, 대략 37×35)
- Radius(Selected/Current 원형): 29px
- Background: Selected → `foreground/brand/normal`(`#2A7FEC`) / Current → `foreground/brand/disabled`(`#DEE3E7`) / Default·Inactive → 배경 없음
- Typography: `Body04/Semibold` 16/24/-0.3%(실제-0.048px) — Date 전체 공통
- Color(텍스트): Selected → `label-inverse/inverse`(`#FFFFFF`) / Current → `label-secondary-normal`(`#434648`) / Default → `label-primary-normal`(`#222426`) / Inactive → `label-secondary-disabled`(`#BABEC2`)
- Typography(type=month, "월" 라벨): `Body06/Semibold` 14/20/-0.3%(실제-0.042px), color `label-secondary-weak`(`#A2A9AE`)
- State: Date일 때 Selected/Current/Default/Inactive 4종

### 9.3 Calendar(달력 컨테이너) — 참고: node 239:13371
- `[Figma에서 확인 불가: 이번 회차에 컨테이너 자체(월 이동 헤더, 요일 라벨 행, 전체 padding/gap/radius)를 재조회하지 못했다.]` 필요 시 Figma에서 별도 조회 필요.

---

## 10. Bottom-sheet — 참고: node 307:9223

이 컴포넌트는 하위에 여러 preset이 있고 각각 폭이 넓어(요청 시 1245~1288px 프레임) 한 번의 조회로 전체가 로드되지 않았다. 이번 회차에 확인한 것은 아래 preset 목록뿐이며, **각 preset 내부의 padding/gap/radius/color 세부값은 `[Figma에서 확인 불가]`** — 다음 작업에서 각 node를 개별 조회해야 한다.

- `Bottom-sheet-datepicker`(1141:23221) 하위 4개 preset: `Status=시작일,Calendar=True`(300:9777), `Status=Default,Calendar=False`(2078:70148), `Status=종료일,Calendar=True`(1141:21405), `Status=Month-picker,Calendar=True`(1141:22837)
- `Component 3`(1162:25378) 하위 3개 preset: `Status=Default`(998:26027), `Status=Dropdown`(998:26026), `Status=Current`(998:26024)
- `Bottom-sheet-time-selected`(998:26025)

8월 기록에는 "Header + Banner-status(warning) + Date-picker/Selectbox×2 + Calendar + Action-area 조합"이라는 구조 설명이 있었으나, 이번 회차 기준으로는 재검증하지 않았으므로 구현 명세로 쓰지 않는다.

---

## 11. Badge — 참고: node 324:9408

### 11.1 Content-Badge(상태/색상 배지) — 참고: node 324:9396
- Variants: `color` = Blue | Gray | DarkGray | Green | Red, `size` = Large | Medium | Small
- Auto Layout: horizontal, `items-center justify-center`
- Padding / Radius by size:

| Size | Padding X/Y | Radius | Typography |
|---|---|---|---|
| Large | 12 / 6 | 10 | Bold 15px/22px/-0.3%(실제-0.045px) |
| Medium | 10 / 3 | 8 | Bold 14px/20px/-0.3%(실제-0.042px) |
| Small | 6 / 3 | 8 | Semibold 13px/19px/-0.2%(실제-0.026px) |

- Color(배경·텍스트) — Status 토큰(§1.2) 재사용:
  - Blue: bg `status/pending/subtle`(`#E1F5FE`), text `status/pending/normal`(`#03A9F4`)
  - Red: bg `status/rejected/subtle`(`#FFEBEE`), text `status/rejected/normal`(`#F44336`)
  - Gray / DarkGray: bg `status/completed/subtle`(`#F1F3F4`), text — Gray는 `label/secondary/selected`(`#8C9499`), DarkGray는 `status/completed/normal`(`#8C9499`, 동일 hex, 토큰만 다름)
  - Green: bg `status/processing/subtle`(`#E8F5E9`), text `status/processing/normal`(`#43A047`)

### 11.2 Content-Badge(카드 종류 배지) — 참고: node 375:8105
- Variants: `type` = Personal-card | Coporate-card(원본 오타, 그대로 기록) 또는 소문자 `personal`/`coporate`(스타일별로 이름 표기 다름), `style` = Round | Square, `mode` = Light | Dark
- Round style: Padding `gap 4 / px 8 / py 3`, radius `999`(pill)
  - Personal: bg `clear-blue/5`(`#EFF8FF`, Light) / `rgba(30,82,175,0.16)`(Dark)
  - Coporate: bg `cool-neutral/10`(`#F1F3F4`, Light) / `rgba(241,243,244,0.04)`(Dark)
  - 텍스트: `Caption01/Semibold` 13/19/-0.2%(실제-0.026px), Personal-Light → `label/primary/normal`(`#222426`) / Personal-Dark → `label/primary/normal`(`#F7F8F9`, dark 전용 값) / Coporate-Light → `label/secondary/normal`(`#434648`) / Coporate-Dark → `label/secondary/normal`(`#CDD3D7`, dark 전용 값)
  - Icon: 카드 그래픽 아이콘(24px, 이미지 에셋, personal/coporate × light/dark 4종)
- Square style: 48×48 고정, radius `Radius/16`(16px), 동일 배경색 규칙, 내부에 아이콘(24px) + 라벨("법인"/"개인", `Caption02/Semibold` 12/18/-0.2%(실제-0.024px)) 세로 배치

### 11.3 Chip/Date-filter — 참고: node 207:11770
- Variants: `type` = Preset(고정), `state` = Default | Selected
- Size: H 36
- Padding: X `Padding/12`(12px) / Y `Padding/8`(8px)
- Gap: `Padding/4`(4px)
- Radius: `Radius/10`(10px)
- Background: Selected → `bg-inverse`(`#434648`) / Default → `foreground/normal/normal`(`#F7F8F9`)
- Typography: `Body05` 15/22/-0.3%(실제-0.045px) — Default는 Medium color `label-primary-disabled`(`#8C9499`), Selected는 Semibold color `label-inverse/inverse`(`#FFFFFF`)

---

## 12. Card — 참고: node 324:9692

⚠️ 2026-09-15: 사용자가 Figma에서 Card 컴포넌트를 수정했다는 안내에 따라 재조회했다. 실제 토큰 값(색상/타이포/spacing)은 변경되지 않았고, **컴포넌트 이름과 그룹 구조가 정리**됐다 — 이전 회차에 Figma가 생성한 참조 코드의 함수명("CradItem")을 그대로 옮겨 적은 것은 오기였다. 실제 Figma 컴포넌트/프레임 이름은 아래와 같이 고쳐 기록한다. 또한 이전 회차에 "카드 배경 없음"으로 잘못 기록했던 부분을 이번에 바로잡았다(§12.1 참고).

### 12.1 Card-item-recipt-list(원본 "recipt" 오타, 그대로 기록) — 참고: node 1983:62173 계열, 상위 그룹 프레임 1983:62318
- Variants: `card` = 개인카드 | 법인카드, `type` = 대기 | 처리중 | 완료 | 반려, boolean `redDot`(안읽음 표시) — 16개 조합 전수 확인(카드 2 × type 4 × redDot 2)
- Size: W 375, H는 content-fit(Figma 캔버스 측정값 기준 약 49px/행)
- Auto Layout: horizontal, `items-start`, padding X `Padding/20`(20px)
- Background(행 전체): `color/background/bg-secondary`(`#FFFFFF`) — ⚠️ 이전 회차에 "배경 없음"으로 기록했던 것은 오류였다. 실제로는 bg-secondary(흰색)가 지정되어 있고, 다만 border와 radius는 없다(구분선 없는 flat white row).
- Gap(행 전체, 배지-텍스트 사이): `Padding/12`(12px)
- 카드종류 배지: §11.2 Content-Badge(Square, 48×48, radius16) 재사용 — 법인 bg `cool-neutral/10`(`#F1F3F4`) / 개인 bg `clear-blue/5`(`#EFF8FF`)
- 텍스트 블록: gap `Padding/2`(2px)
  - 거래처명: `Body05/Medium` 15/22/-0.3%(실제-0.045px), color `label-secondary-normal`(`#434648`)
  - 금액: `Body05/Bold` 15/22/-0.3%(실제-0.045px), color `label-primary-normal`(`#222426`), "원" 단위도 동일 스타일
  - 날짜·시간: `Body06/Medium` 14/20/-0.3%(실제-0.042px), color `label-secondary-weak`(`#A2A9AE`), gap `Padding/6`(6px)
  - 처리상태 배지: padding X `Padding/6`(6px) Y `Padding/3`(3px), radius `Radius/8`(8px), `Caption01/Semibold` 13/19/-0.2%(실제-0.026px) — 대기→bg `status/pending/subtle`(`#E1F5FE`) text `status/pending/normal`(`#03A9F4`) / 처리중→bg `status/processing/subtle`(`#E8F5E9`) text `status/processing/normal`(`#43A047`) / 완료→bg `status/completed/subtle`(`#F1F3F4`) text `status/completed/normal`(`#8C9499`) / 반려→bg `status/rejected/subtle`(`#FFEBEE`) text `status/rejected/normal`(`#F44336`)
- redDot(안읽음): 좌상단(left 12, top 1) 6×24 이미지 에셋(§5.5 Tab-item dot과 동일 에셋) — 정확한 도형 `[Figma에서 확인 불가]`
- Radius/Border(카드 자체): 없음(직접 확인) — flat white row, 카드 사이 구분은 배경색 대비로만 처리
- State: 대기/처리중/완료/반려 × 안읽음(redDot) on/off — 8가지 조합 전수 확인.

### 12.2 Card-item-recipt-error(원본 "recipt" 오타, 그대로 기록) — 참고: node 2098:60164
- Size: H 58
- Padding: X `Padding/20`(20px) / Y `Padding/16`(16px)
- Radius: `Radius/14`(14px)
- Border: 1px, color `line/normal/neutral` → `rgba(87,94,98,0.16)`
- Background: `static/white`(`#FFFFFF`)
- Typography(파일명): `Body06/Medium` 14/20/-0.3%(실제-0.042px), color `label-secondary-normal`(`#434648`)
- Icon: `alert-circle/24`(우측)
- Figma dev 주석: "영수증 등록 인식 실패 화면에 사용되는 카드 ui입니다."
- State: 단일 상태(에러 전용 카드, 별도 variant 없음)

### 12.3 Card-warning — 참고: 상위 그룹 프레임 2170:116883, node 336:11617(M) / 1569:44491(S)
- Variants: `size` = S | M
- Size: M은 W 335(H는 content-fit), S는 W 310 H 36(고정)
- Padding: X `Padding/14`(14px) / Y `Padding/12`(12px, M만) — S는 세로 중앙정렬로 별도 py 없음
- Gap: `Padding/8`(8px)
- Radius: `Radius/10`(10px)
- Background: `status/rejected/subtle`(`#FFEBEE`)
- Typography: M은 `Body06/Semibold` 14/20/-0.3%(실제-0.042px), S는 `Caption01/Semibold` 13/19/-0.2%(실제-0.026px) — 둘 다 color `label-primary-normal`(`#222426`)
- Icon: `alert-circle/16`(좌측)

---

## 13. Image-input — 참고: node 354:19324

### 13.1 Thumbnail — 참고: node 431:15767
- Size: W 375 H 541(부모 프레임 기준, object-fit cover 이미지)
- `[Figma에서 확인 불가: 실제 이미지 콘텐츠이므로 색상/타이포 해당 없음]`

### 13.2 Image-viewer-343*140 — 참고: node 1456:23785
- Variants: `size` = M | S
- Size: M은 343×140, S는 311×126
- Radius: `Radius/20`(20px)
- Border: M은 1px, S는 0.907px(비율 축소값) — color `line/normal/normal` → `rgba(87,94,98,0.24)`
- 오버레이: `color/material/dimmer-weak`(검정, §1.2 기준 `rgba(0,0,0,0.32)`)를 이미지 위 마스크로 적용
- 중앙 버튼(확대 아이콘): Button-icon 패턴 재사용 — M은 52px(padding10), S는 44px(padding10), radius 999(pill), bg `static/white`(`#FFFFFF`), 내부 `search` 아이콘(M 24px / S 20px)

### 13.3 Image-viewer-375*591 — 참고: node 431:15771
- Size: W 375 H 541
- Background: `foreground/normal/disabled-normal`(`#CDD3D7`)
- 내부에 §13.1 Thumbnail을 꽉 채워 배치

---

## 14. Progress — 참고: node 2112:92010

### 14.1 Progress-bar — 참고: node 427:17502
- Variants: `progress` = Step-1 | Step-2 | Step-3
- Size(트랙): W 212 H 6
- Radius: `Radius/999`(pill)
- Background(트랙): `foreground/normal/disabled-subtle`(`#EBEEF0`)
- Background(인디케이터): `foreground/brand/normal`(`#2A7FEC`)
- Indicator 폭: Step-1 = 71px, Step-2 = 141px, Step-3 = 212px(트랙 전체)
- State: Step-1/2/3 3단계, 인디케이터 폭만 변화

---

## 15. Modal — 참고: node 614:12775

### 15.1 Modal — 참고: node 614:12076
- Variants: `type` = One-button | Two-button, `variant` = Normal | Strong | Wide, boolean `description`
- Size: W 343(고정), H는 content-fit
- Auto Layout: vertical
- Padding: pt `Padding/36`(36px, 상단만 — 좌우/하단은 내부 Container에서 처리)
- Radius: `Radius/20`(20px)
- Shadow: `drop-shadow(rgba(134,134,134,0.32) 0 0 5px)` — Elevation 표의 Shadow-Medium과 유사하지만 정확히 일치하진 않음(blur 5 vs 10) `[Figma에서 확인 불가: Elevation 표와의 정확한 매핑]`
- Background: `foreground/normal/normal`(`#F7F8F9`)
- Title: `Body03/Bold` 18/26/-0.3%(실제-0.054px), color `label-primary-normal`(`#222426`), 중앙정렬
- Description(옵션): `Body04/Medium` 16/24/-0.3%(실제-0.048px), color `label-primary-alternative`(`#A2A9AE`)
- Text 영역 Padding: X `Padding/32`(32px), 내부 gap `Padding/12`(12px)
- Action 영역 Padding: pt `Padding/10`(10px) px `Padding/20`(20px) pb `Padding/20`(20px, Two-button/Strong은 pb 22px)
- 버튼: `Button-solid`/`Large` 스펙 재사용(h52, radius14, px28 py14) — One-button/Normal은 브랜드 Solid 버튼 1개. Two-button/Normal·Wide는 Outlined 버튼(흰 배경, border `line/normal/normal` → `rgba(87,94,98,0.24)`) + Solid 버튼(브랜드) 나열, gap 10px. Two-button/Strong은 Solid 버튼 아래 Button-text(§6.3, Body04/Semibold, color `label-secondary-normal`) 세로 배치.
- Wide variant: 버튼 폭 고정 180px(신규 확인, 8월 기록 220px과 다름 — 이번 조회 값을 최신으로 채택)
- State: type×variant 조합(One/Two-button × Normal/Strong/Wide) 4가지 실사용 조합 확인. Hover/Pressed `[Figma에서 확인 불가]`

### 15.2 List-item — 참고: node 922:17832
`[Figma에서 확인 불가: 이번 회차에 재조회하지 못함]`

---

## 16. Action-Area — 참고: node 196:7993

⚠️ 8월 기록은 이 컴포넌트를 "Action-Area"(183:20022)와 "Action-area"(196:7993) 두 개의 별도 컴포넌트셋으로 다뤘으나, 이번 조회 결과 **node 183:20022는 실제로는 컴포넌트가 아니라 섹션 헤드라인 프레임**이었다(타이틀 텍스트 "Action Area"만 있음). 실제 재사용 가능한 컴포넌트는 196:7993 하나이며, 8월 기록보다 훨씬 많은 variant(Dark 색상 모드 포함)가 있다.

### 16.1 Action-area — 참고: node 196:7993
- Variants: `type` = One-button | Two-button, `color` = White | Default | Dark(신규 확인), `variant` = Strong | Neutral | Normal | Wide, boolean `alternative`
- Size: W 375
- Auto Layout: vertical
- Padding(Contents 영역): pt `Padding/10`(10px) px `Padding/20`(20px) pb `Padding/20`(20px)
- Main Action 버튼: h 52(대부분) 또는 56(One-button/Default/Normal 등 일부 조합), radius `Radius/14`(14px), px `Padding/28`(28px) py `Padding/14`(14px)
- Main Action 배경: White/Default 계열 → `foreground/brand/normal`(`#2A7FEC`) / Dark 계열 → `foreground/brand/normal`(`#3B99F6`, Dark 전용 값)
- Main Action 텍스트: `Body04/Semibold` 16/24/-0.3%(실제-0.048px), color 거의 `white` 고정(One-button/White/Normal만 `bg-primary`(`#F7F8F9`) 텍스트색 — 원본 그대로 기록)
- Alternative Action(Two-button일 때): 흰 배경(Dark 모드는 `#222426`) + border 1px `line/normal/neutral` → `rgba(87,94,98,0.16)`, radius14, 텍스트 color `label-secondary-normal`(Light `#434648` / Dark `#CDD3D7`)
- Two-button/Strong: Main Action 아래 Button-text("대체") 세로 배치, gap `Padding/4`(4px)
- Two-button/Wide: Alternative Action + Main Action(폭 고정 220px) 가로 배치, gap 10px
- 배경 그라디언트(Contents 영역 상단): color별로 다름 — Dark `rgba(22,25,26,0)→bg-primary(dark)`, Default `rgba(241,243,244,0)→bg-alternative`, White `rgba(255,255,255,0)→bg-secondary`
- Home-bar(하단, 대부분 variant에 포함): §5.3 Home-bar 재사용 — 배경은 Dark → `bg-primary`(dark, `#191A1B`) / Default → `bg-alternative`(`#F1F3F4`) / White → `bg-secondary`(`#FFFFFF`)
- Figma dev 주석(발견): "변경 전: Two Button / 변경 후: One Button + Text Button" — Two-button/White/Strong 조합이 폐기 예정임을 시사(정확한 상태 `[Figma에서 확인 불가]`, 원문 그대로 기록)
- State: type(2) × color(3) × variant(4) 조합 중 실제 정의된 조합만 존재(전체 24개 중 약 11개 실사용 조합 확인) — Hover/Pressed는 버튼 자체(§6.1)의 Interaction 레이어를 따름.

---

## 17. 컴포넌트 명명 규칙 참고

Figma 원본에 아래와 같은 오타/불일치가 있다 — 그대로 두었다(임의 수정하지 않음): `Coporate-card`(Corporate 오타, §11.2/§12.1), `Card-item-recipt-list`/`Card-item-recipt-error`("receipt"→"recipt" 오타, §12.1/§12.2), `Chekced`(Checked 오타, 과거 기록), `skyBlu`(skyBlue 오타, 일부 §1.2 원본 토큰명에만 존재), `Colse-Title-left`(Close 오타, 과거 기록 — 이번 회차 Header 재조회 시 해당 정확한 variant명은 발견되지 않음).
