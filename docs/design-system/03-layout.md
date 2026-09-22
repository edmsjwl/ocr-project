# Layout

> 상위 문서: [DESIGN.md](../../DESIGN.md)
> Figma: `[SBS] OCR 프로젝트_디자인` 🔵 디자인시스템 페이지

Grid, Status-bar, Home-bar, Header, Tab-item, Tab-menu, Page-Title-text, Navigation, Page-title-date, Status-message, Skeleton, ios-keyboard.

---

## Grid

`grid/16`, `grid/20` 프레임만 존재하고 컬럼 수·거터·마진 값은 설정되어 있지 않다.

**Tokens**
- 배경 `bg-primary` (#F7F8F9), 테두리 `line/normal/normal`

---

## Status-bar

iOS 상태바. 배경·라벨 색상 조합에 따른 정적 컴포넌트.

**Properties**

| Property | Values |
|---|---|
| `background` | Alternative \| Secondary \| Primary \| Transparent |
| `label` | Black \| White |

5개 조합만 존재(Alternative/Secondary/Primary/Transparent × Black, Transparent × White).

**Size & Layout**
- 전체: W 375 × H 44
- Time 영역(좌): W 93, padding X 30.5 / Y 13(raw), 텍스트 "9:41"
- Status 영역(우): W 95, padding 14, 내부 gap 4, padding-top 3 / bottom 1
- 아이콘: Celluar 18×12, Wi-Fi 16×12, Battery 25×12(이미지 에셋)
- Radius·Border 없음

**Tokens**

| background | 값 |
|---|---|
| Primary | `bg-primary` (#F7F8F9) |
| Secondary | `bg-secondary` (#FFFFFF) |
| Alternative | `bg-alternative` (#F1F3F4) |
| Transparent | 없음 |

| label | 텍스트 색 |
|---|---|
| Black | `label/primary/normal` (#222426) |
| White | `label/inverse/inverse` (#FFFFFF) |

텍스트 서체는 Pretendard가 아니라 `SF Pro Semibold(590) 15px`, letter-spacing -0.237px(raw, 시스템 폰트 예외).

**States**
없음(정적 컴포넌트)

**Usage**
Figma 설명: "iPhone X"

---

## Home-bar

iOS Home Indicator 영역.

**Properties**
`background` = Alternative | Secondary | Primary | Transparent

**Size & Layout**
- W 375, H 27 (padding-top 16 + Slider 5 + padding-bottom 6), padding X 10
- Slider: W 134 × H 5, radius 4

**Tokens**

| background | 값 |
|---|---|
| Alternative | #F1F3F4 |
| Secondary | #FFFFFF |
| Primary | #F7F8F9 |
| Transparent | 없음 |

Slider bg `bg-inverse` (#434648)

**States**
없음(정적)

---

## Header

앱 상단 헤더. 타입별로 좌/우 아이콘과 제목 배치가 다르다.

**Properties**

| Property | Values |
|---|---|
| `type` | Home \| Back \| Back home \| Close \| Close-Title-center |
| `background` | Primary \| Secondary \| Alternative |
| `icon` | "True"(고정) |
| `iconCount` | 1 \| 2 |
| `iconShow` / `showStepIndicator` / `title` | boolean |

총 12개 인스턴스 확인. Hover/Pressed/Focus/Disabled variant 없음.

**Size & Layout**
- W 375 × H 56, padding X `Padding/20`(20px) / Y `Padding/16`(16px). Radius·Border 없음
- 제목: 가로 중앙(W 280)
- Home 타입: 좌측 로고 `LogoWise`(64×22) + `Logo`(42×25), gap `Padding/2`(2px) — SVG `assets/logo-wise-wordmark.svg`, `assets/logo-scan-mark.svg`
- Back 타입: 좌측 `Icon/chevron-left/24` + 제목 그룹 gap `Padding/4`(4px, 내부 gap 3px)
- Back home 타입: 좌측 `Icon/chevron-left/24`, 우측 `Icon/home/24`, 중앙 제목
- Close 타입: 우측 `Icon/close/24`, gap 8px, justify-end, 중앙 제목(W 37 × H 26)
- Close-Title-center(Secondary 배경): 우측 `Icon/close/24`, 중앙 제목(gap `Padding/8`)
- Step-indicator(`showStepIndicator=true`, Back 타입): 현재 숫자 + "/" + 총 단계 숫자, 내부 gap `Padding/2`(2px)

**Tokens**

| background | 값 |
|---|---|
| Alternative | `bg-alternative` (#F1F3F4) |
| Secondary | `bg-secondary` (#FFFFFF) |
| Primary | `bg-primary` (#F7F8F9) |

- 제목(전 타입 공통): `Body03/Semibold` 18px/26px/-0.3%(실제 -0.054px), `label/primary/normal` (#222426)
- Step-indicator 현재 숫자: `Body04/Semibold` 16/24/-0.3%, `label/brand/normal` (#2A7FEC)
- Step-indicator "/"·총 단계: `Body06/Semibold` 14/20/-0.3%, `label/secondary/normal` (#434648)
- 아이콘 24px 내부 색: `[Figma에서 확인 불가]`(이미지 에셋)

**States**
Hover/Pressed/Focus/Disabled variant 없음

**Usage**
Figma dev 주석(실사용처): Home→"[메인홈]", Back→"[온보딩]", Back home→"[상세 내역]", Close→"[영수증 등록]"

---

## Tab-item

**Properties**
`Property 1` = Activated | Default, boolean `dot`

**Size & Layout**
- H 40, W content-fit, padding X `Padding/2`(2px) / Y `Padding/8`(8px)
- `dot`: W 4 × H 24 이미지 에셋(라벨 우측)

**Tokens**
- 타이포: `Body04/Bold` 16/24/-0.3%(실제 -0.048px)
- Activated: 텍스트 `label/secondary/normal` (#434648), `border-bottom 2px solid label/primary/normal` (#222426)
- Default: 텍스트 `label/secondary/disabled` (#BABEC2), 테두리 없음

**States**
Activated(선택됨) / Default(선택안됨). Hover/Pressed/Focus/Disabled variant 없음.

---

## Tab-menu

**Properties**
`Property 1` = 전체 | 완료 | 처리중 | 작성중 | 중복 (variant 이름). 실제 탭 라벨 텍스트는 **전체 / 대기 / 처리중 / 완료 / 반려** — variant 이름과 라벨 텍스트가 다르다.

**Size & Layout**
- W 375, 높이 41(Tab-item 40 + 하단 border 1)
- padding X `Padding/20`(20px), gap `Padding/32`(32px)

**Tokens**
- Border: `border-bottom 1px solid line/normal/alternative` → rgba(87,94,98,0.08)
- 탭 스타일은 [Tab-item](#tab-item)과 동일

**States**
첫 탭 "전체"만 Activated + dot(4×24), 나머지 4개는 Default

---

## Page-Title-text

**Properties**
boolean `description`; 텍스트 props `title`("타이틀이 들어갑니다"), `text`("타이틀에 대한 설명이 들어갑니다")

**Size & Layout**
W 375 × H 96, padding X `Padding/20`(20px) / Y `Padding/16`(16px), gap `Padding/6`(6px), Auto Layout vertical

**Tokens**
- 제목: `Heading03/Semibold` 24/34/-0.4%(실제 -0.096px), `label/primary/normal` (#222426)
- 설명: `Body04/Medium` 16/24/-0.3%(실제 -0.048px), `label/secondary/normal` (#434648)

**Usage**
Figma 주석: "인증화면에 사용됩니다."

---

## Navigation

하단 pill 내비게이션. Navigation-item(개별 탭) → Navigation-menu(pill 컨테이너) → Navigation-bottom(Home-bar 포함 전체) 3단 구성.

**Properties**

| 컴포넌트 | Property | Values |
|---|---|---|
| Navigation-item | `Property 2` | Home-Selected \| Home-Default \| Receipt-Default \| Receipt-Selected |
| Navigation-bottom | `Type` | Home \| Receipt |

**Size & Layout**
- Navigation-item: W 100 × H 57, radius `Number/64`(64px), padding X `Padding/20`(20px) / Y `Padding/2`(2px), 내부 세로 gap `Padding/3`(3px)
- Navigation-menu: H 69, radius 64, padding `Padding/6`(6px), Navigation-item 2개 가로 배치
- Navigation-bottom: Navigation-menu + Home-bar(H 27) 세로 조합, 375×96

**Tokens**
- Navigation-item bg: Home-Selected `foreground/normal/normal` (#F7F8F9), Receipt-Default `foreground/normal/selected` (#EBEEF0)
- 아이콘: `Iimg-nav/24`(24px, Type=home|list, Status=activated|disabled)
- 라벨: `Caption01/Bold` 13/19/-0.2%(실제 -0.026px) — 홈 "홈"(`label/primary/normal` #222426), 영수증 탭 "영수증 내역"(선택 안 됨 `label/secondary/weak` #A2A9AE)
- Navigation-menu bg `foreground/normal/selected` (#EBEEF0), Shadow `Shadow-Nav`([01-foundation.md](01-foundation.md#elevation))

---

## Page-title-date

**Size & Layout**
W 232, padding X `Padding/16`(16px) / Y `Padding/8`(8px), Auto Layout vertical

**Tokens**
텍스트 "2026년 8월": `Body05/Semibold` 15/22/-0.3%(실제 -0.045px), `label/primary/alternative` (#A2A9AE), "2026년"·"8월" 사이 gap `Padding/4`(4px)

**Usage**
Figma 주석: "영수증 내역 페이지 타이틀에 사용됩니다."

---

## Status-message

빈 상태·에러 상태 안내 화면 구성 요소. text/icon/button 3가지 변형.

**Properties**

| 컴포넌트 | Boolean |
|---|---|
| Status-message-text | `description` |
| Status-message-icon | `showDescription` |
| Status-message-button | `showDescription`, `showButtonSolid` |

**Size & Layout**
- Status-message-text: W 375, padding top `Padding/120`(120px) / bottom `Padding/80`(80px) / X `Padding/32`(32px), 세로 gap `Padding/6`(6px), 가운데 정렬
- Status-message-icon: W 375, padding Y `Padding/80`(80px) / X `Padding/20`(20px), gap `Padding/20`(20px). 상단 `Img-empty/64`(64×64, light)
- Status-message-button: W 343 × H 342, padding Y `Padding/80`(80px) / X `Padding/20`(20px), gap 20 / 안쪽 그룹 gap `Padding/24`(24px). 상단 `Img-warning/48`(Color=gray, 52×52)

**Tokens**
- 제목: `Body03/Semibold` 18/26/-0.054px, `label/secondary/normal` (#434648) — 예시 "타이틀이 들어갑니다"
- 설명(text·icon 공통): `Body05/Medium` 15/22/-0.045px, `label/primary/disabled` (#8C9499) — 예시 "보조 메시지가 들어갑니다"
- Status-message-button 제목: `Body02/Semibold` 20/28/-0.4%(실제 -0.08px), `label/secondary/normal` (#434648) — "인터넷 연결을 확인해주세요"
- Status-message-button 설명: `Body04/Medium` 16/24/-0.048px, `label/secondary/selected` (#8C9499), 2줄
- Status-message-button 버튼: Button-solid `Color=Assistive, Variant=Outlined, Size=Medium`(H 44, padding X 20 / Y 10, radius 12, border 1px `line/normal/neutral`) — 라벨 "재시도" `Body05/Semibold` 15/22 `label/secondary/normal`, 아이콘 없음. 상세 스펙은 [04-actions-inputs.md → Button-solid](04-actions-inputs.md#button-solid)

---

## Skeleton

로딩 placeholder. list/detail 2종.

**Size & Layout**
- Skeleton-card-list: W 343 × H 48, padding X `Padding/20`(20px), radius `Radius/14`(14px). 좌측 48×48 박스 radius `Radius/16`(16px). 우측 텍스트 영역 gap `Padding/12`(12px) / 세로 gap `Padding/3`(3px): 1행 막대 H 22 radius `Radius/6`(6px) W 120·W 64, 2행 막대 H 20 radius 6 W 48·W 40
- Skeleton-card-detail: W 343, padding X `Padding/20`(20px) / Y `Padding/18`(18px), gap `Padding/10`(10px), radius 14, border 1px `line/normal/alternative` → rgba(87,94,98,0.08). 행 H 30 × 7개: 막대 H 26 radius 6(좌 W80/우 W80 1~2행, W120 3~7행). 마지막 행: W 64×H 26 막대 + 180×112 radius `Radius/8`(8px) 박스

**Tokens**
- 막대색: Skeleton-card-list `foreground/normal/selected` (#EBEEF0) / Skeleton-card-detail `foreground/normal/disabled-subtle` (#EBEEF0)
- 배경: Skeleton-card-detail `bg-secondary` (#FFFFFF)
- 그림자: `drop-shadow(0 0 2px rgba(134,134,134,0.05))`(둘 다 동일)

---

## ios-keyboard

iOS 기본 키보드 UI(`UIKeyboardType.default`).

**Size & Layout**
- W 375, 제안 행 H 48(3칸, 구분선 H 25 opacity 10%) + 키 4행(각 H 44, 행 gap 12, padding 4) + Home Indicator 영역 H 72(바 W 37.5%×H 5 radius 5)

**Tokens**
- 배경 `rgba(197,201,208,0.9)` + backdrop blur 27(`iOS/Background Blur` radius 54), 스타일 토큰 `iOS/Keyboard Background #C5C9D0`
- 키: bg `iOS/Key Background Highlight #FFFFFF`, radius 5, `drop-shadow(0 1px 0 rgba(0,0,0,0.3))`, 글자 SF Pro Text 23px `iOS/Key Label #000000`(스페이스·리턴 등 16px)
- 기능 키 bg `iOS/Key Background Dim #AEB3BE`

**Usage**
Figma 설명: "Default keyboard. UIKeyboardType.default"

---

## Figma References

파일: `[SBS] OCR 프로젝트_디자인` (`ese9l01OJiDfirO8Q6XXIY`), "🔵 디자인시스템" 페이지.

| 컴포넌트 | Node ID |
|---|---|
| Layout(섹션 전체) | 158:29966 |
| Grid — `grid/16` | 158:30270 |
| Grid — `grid/20` | 2150:104533 |
| Status-bar | 161:30744 |
| Home-bar | 164:30923 |
| Header(전체) | 166:3969 |
| Header — Home | 164:31037 |
| Header — Back | 998:28960 |
| Header — Back home | 164:31326 |
| Header — Close | 239:13289 |
| Header — Close-Title-center | 239:13292 |
| Tab-item | 207:11372 |
| Tab-menu | 207:11114 |
| Page-Title-text | 175:8777 |
| Navigation-item | 432:17481 |
| Navigation-menu | 432:17480 |
| Navigation-bottom | 614:11468 |
| Page-title-date | 307:7625 |
| Status-message-text | 239:12641 |
| Status-message-icon | 682:18229 |
| Status-message-button | 1000:27331 |
| Skeleton-card-list | 1983:69188 |
| Skeleton-card-detail | 844:21863 |
| ios-keyboard | 1169:23686 |
