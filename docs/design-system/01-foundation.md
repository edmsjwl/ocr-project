# Foundation

> 상위 문서: [DESIGN.md](../../DESIGN.md)
> Figma: `[SBS] OCR 프로젝트_디자인` 🔵 디자인시스템 페이지

Typography, Color(Atomic / Semantic Light / Semantic Dark), Elevation.

토큰이 연결된 값은 `토큰명 (resolved 값)` 형식으로 적는다. `opacity`가 걸린 토큰은 원색이 아니라 `rgba(원색, opacity)`로 렌더한다 — Figma MCP 코드의 CSS 변수 fallback hex는 opacity를 반영하지 않은 원색이라 그대로 쓰면 실제보다 진하다. 값을 확인하지 못한 항목은 `[Figma에서 확인 불가]`로 표시한다.

---

## Typography

폰트: `Pretendard`(Regular 400 / Medium 500 / SemiBold 600 / Bold 700). Required 표시 `*`만 `Pretendard JP Medium 14px`. 굵기와 무관하게 행간·자간은 같다. Status-bar 시간 텍스트만 `SF Pro Semibold(590) 15px`, ios-keyboard는 `SF Pro Text`.

| Token | Size(px) | Line Height(px) | Letter Spacing(%) | 실제 px (size × %) |
|---|---|---|---|---|
| Display01 | 34 | 44 | -0.6 | -0.204 |
| Display02 | 32 | 42 | -0.6 | -0.192 |
| Display03 | 30 | 40 | -0.6 | -0.180 |
| Heading01 | 28 | 38 | -0.5 | -0.140 |
| Heading02 | 26 | 36 | -0.5 | -0.130 |
| Heading03 | 24 | 34 | -0.4 | -0.096 |
| Body01 | 22 | 32 | -0.4 | -0.088 |
| Body02 | 20 | 28 | -0.4 | -0.080 |
| Body03 | 18 | 26 | -0.3 | -0.054 |
| Body04 | 16 | 24 | -0.3 | -0.048 |
| Body05 | 15 | 22 | -0.3 | -0.045 |
| Body06 | 14 | 20 | -0.3 | -0.042 |
| Caption01 | 13 | 19 | -0.2 | -0.026 |
| Caption02 | 12 | 18 | -0.2 | -0.024 |
| Caption03 | 11 | 16 | -0.2 | -0.022 |

Typography 페이지에 적힌 숫자 라벨 중 `Body03 -0.4`, `Heading03 -0.5`는 컴포넌트가 실제로 바인딩하는 스타일 정의(`Body03/Semibold` letterSpacing -0.3, `Heading03/Bold` letterSpacing -0.4)와 다르다. 위 표는 컴포넌트가 쓰는 스타일 정의 값이다. Display01~03, Heading01~02, Body01, Caption 계열 행은 페이지 라벨 값을 그대로 적었으며, 스타일 정의와의 일치는 `[Figma에서 확인 불가]`(예: `Display01/Bold` 스타일 정의는 34/38/-0.5로 조회된 바 있어 라벨의 44/-0.6과 다르다).

---

## Color

### Atomic (원시값)

`Color Token-Atomic`.

| 그룹 | 토큰 | Resolved Value |
|---|---|---|
| Common | `color-atomic-common-0` / `-100` | `#FFFFFF` / `#000000` |
| Cool Neutral | `color-atomic-cool-neutral-5~100` | 5:`#F7F8F9` 10:`#F1F3F4` 15:`#EBEEF0` 20:`#DEE3E7` 30:`#CDD3D7` 40:`#BABEC2` 50:`#A2A9AE` 60:`#8C9499` 70:`#575E62` 80:`#434648` 90:`#222426` 100:`#191A1B` |
| Clear Blue(브랜드) | `color-atomic-brand-clearblue-5~90` | 5:`#EFF8FF` 10:`#DBEEFE` 20:`#BEE2FF` 30:`#93D2FD` 40:`#60B8FA` 50:`#3B99F6` **60:`#2A7FEC`(key color)** 70:`#1D65D8` 80:`#1E52AF` 90:`#1E488A` |
| Sky Blue(state) | `color-atomic-skyBlue-5~90, A10~A40` | 5:`#E1F5FE` 10:`#B3E5FC` 20:`#81D4FA` 30:`#4FC3F7` 40:`#29B6F6` 50:`#03A9F4` 60:`#039BE5` 70:`#0288D1` 80:`#0277BD` 90:`#01579B` / A10:`#80D8FF` A20:`#40C4FF` A30:`#00B0FF` A40:`#0091EA` |
| Green(state) | `color-atomic-green-5~90, A10~A40` | 5:`#E8F5E9` 10:`#C8E6C9` 20:`#A5D6A7` 30:`#81C784` 40:`#66BB6A` 50:`#4CAF50` 60:`#43A047` 70:`#388E3C` 80:`#2E7D32` 90:`#1B5E20` / A10:`#B9F6CA` A20:`#69F0AE` A30:`#00E676` A40:`#00C853` |
| Red(state) | `color-atomic-red-5~90, A10~A40` | 5:`#FFEBEE` 10:`#FFCDD2` 20:`#EF9A9A` 30:`#E57373` 40:`#EF5350` 50:`#F44336` 60:`#E53935` 70:`#D32F2F` 80:`#B71C1C` 90:`#82181A` / A10:`#FF8A80` A20:`#FF5252` A30:`#FF1744` A40:`#D50000` |

Figma에는 스와치 형태의 별도 "Color" 페이지가 있는데, 같은 토큰명인데 값이 다르다(예: Cool-Neutral/20이 그 페이지엔 `#D7DCE0`, Atomic 표엔 `#DEE3E7`). 컴포넌트가 실제 바인딩하는 값(`get_variable_defs`)은 이 Atomic 표와 일치하므로 이 표가 기준이다.

`get_variable_defs`로 Semantic Light/Dark를 라이브 조회했을 때 되돌아온 atomic 값 27개(Cool Neutral 5/10/15/20/30/40/50/60/70/80/90/100, Clear Blue 5/10/20/30/40/50/60/80/90, Sky Blue 50/60, Green 50/60/70, Red 50/60/A20/A30)는 이 표와 전부 일치한다. 그 외 shade(Common 전체, Sky Blue 70/80/90/A10/A40, Green 5/10/20/30/40/80/90/A10/A40, Red 5/10/20/30/40/70/80/90/A10/A40)는 라이브로 직접 조회되지 않아 `[Figma에서 확인 불가]` 상태의 기존 기록값이다.

### Semantic (의미값) — Light

`Color Token-Semantic-Light`.

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

Status 토큰명(pending/processing/completed/rejected)은 영수증 상태 라벨과 다음과 같이 쓰인다: 대기→pending, 처리중→processing, 완료→completed, 반려→rejected (Card-item-receipt-list, Modal-영수증상태에서 확인).

### Semantic (의미값) — Dark

`Color Token-Semantic-Dark`. 토큰 이름 구조는 Light와 동일하고 atomic 매핑만 다르다. 확인된 행:

| 토큰 | Light | Dark |
|---|---|---|
| `bg-primary` | cool-neutral-5(`#F7F8F9`) | cool-neutral-100(`#191A1B`) |
| `bg-secondary` | common-0(`#FFFFFF`) | cool-neutral-90(`#222426`) |
| `label-primary-normal` | cool-neutral-90(`#222426`) | cool-neutral-5(`#F7F8F9`) |
| `fg-brand-normal` | clearBlue-60(`#2A7FEC`) | clearBlue-50(`#3B99F6`) |

Dark 프레임에서 함께 조회된 atomic 값: `Clear Blue/90 #1E488A`, `Clear Blue/30 #93D2FD`, `Clear Blue/10 #DBEEFE`, `Green/50 #4CAF50`, `Red/A20 #FF5252`, `Red/A30 #FF1744`. 이 값들이 매핑되는 semantic 토큰명은 `get_variable_defs`로 특정되지 않아 `[Figma에서 확인 불가]`.

Action-area Dark에서 쓰이는 dark 값(node는 [06-display-feedback.md → Figma References](06-display-feedback.md#figma-references) 참고): 메인 버튼 bg `#3B99F6`, Button-text·Interaction 색 `#CDD3D7`, Home-bar bg `bg-primary(dark) #191A1B`.

---

## Elevation

Shadow 3종 swatch는 Layout 프레임 안의 그룹에 있다.

| 토큰 | Effect |
|---|---|
| `Shadow-Low` | drop-shadow, color `#8686860A`(rgba(134,134,134,0.04)), blur 3, spread 10, offset (0,0) |
| `Shadow-Medium` | drop-shadow, color `#86868652`(rgba(134,134,134,0.32)), blur 10, spread 0, offset (0,0) |
| `Shadow-Strong` | drop-shadow, color `#868686CC`(rgba(134,134,134,0.80)), blur 12, spread 0, offset (0,0) |
| `Shadow-Nav` | 5개 레이어(Navigation-menu에서 사용): (1,3) blur 3 `#45515A17` / (3,7) blur 5 `#45515A0D` / (5,13) blur 6 `#45515A03` / (8,20) blur 6 `#45515A00` / (-1,-1) blur 10 `#45515A0A` |

컴포넌트에 직접 쓰인 그 외 그림자: Modal 계열 `drop-shadow(0 0 5px rgba(134,134,134,0.32))`, Button-action-card·Skeleton `drop-shadow(0 0 1.5px rgba(134,134,134,0.04))` / `drop-shadow(0 0 2px rgba(134,134,134,0.05))`, 트레일링 버튼 `0 1px 1px rgba(0,0,0,0.03)`.

---

## 명명 불일치

Figma 원본에서 그대로 쓰이는 이름이다(임의 수정하지 않았다). 아래 항목은 이 파일 범위를 넘어 `04-actions-inputs.md` · `05-containers-overlays.md` · `06-display-feedback.md`에 걸쳐 있다.

- `Card-item-recipt-error` — "receipt"의 오타 "recipt" (같은 계열의 `Card-item-receipt-list`는 정상 철자) — 05
- `Iimg-nav/24` — "Img-nav/24"의 오타 "Iimg" — 03
- Check-box 텍스트 prop `lable` — "label"의 오타 — 04
- `Image-viewer-375*591` — 이름의 591과 달리 실제 높이는 541 — 05
- `Button-chip-filter` — 이 문서에서는 예전 이름 "Chip/Date-filter"와 함께 기재 — 04
- `Card-info` — 예전에 "Card-warning"으로 불렸으나 Red(경고)/Blue(정보) 두 색을 모두 가짐 — 05
- variant 값 대소문자·표기 불일치: Check-box `Selected|disabled`(소문자) vs Check-box/item `Selected|Disabled`, Dropdown-box `Close|open|Dropdown-list`, Category-badge `Light|Dark`(Round) vs `light|dark`(Square), Category-badge `personal-card`(Round) vs `personal`(Square), Action-area Two-button `Normal`(White) vs `Neutral`(Default·Dark), Tab-menu variant 이름 `전체|완료|처리중|작성중|중복`과 실제 라벨 `전체|대기|처리중|완료|반려` — 04·05·06

---

## Figma References

파일: `[SBS] OCR 프로젝트_디자인` (`ese9l01OJiDfirO8Q6XXIY`), "🔵 디자인시스템" 페이지.

| 항목 | Node ID |
|---|---|
| Typography | 38:110 |
| Color · Atomic | 55:2157 |
| Color · Atomic — "Color" 스와치 페이지(비교용, 미갱신) | 50:609 |
| Color · Semantic Light | 97:1313 |
| Color · Semantic Dark | 2098:83095 |
| Elevation | 2729:98726 |
