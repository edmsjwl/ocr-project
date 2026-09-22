# Actions & Inputs

> 상위 문서: [DESIGN.md](../../DESIGN.md)
> Figma: `[SBS] OCR 프로젝트_디자인` 🔵 디자인시스템 페이지

Button, Textfield, Check-box, Date-picker.

---

## Button

Button-solid, Button-icon, Button-text, Button-check-box, Button-action-card, Button-chip-filter 6종.

### Button-solid

브랜드 색상의 기본 액션 버튼. Primary/Assistive × Solid/Outlined × 4사이즈 × 3상태.

**Properties**

| Property | Values |
|---|---|
| `Color` | Primary \| Assistive |
| `Variant` | Solid \| Outlined |
| `Size` | Large \| Medium \| Small \| Xsmall |
| `State` | Normal \| Selected \| Disabled |
| boolean | `showLeadingIcon`, `showTrailingIcon` |
| text | `label`("텍스트") |

48개 조합. 폭은 고정이 아니라 content-fit(샘플 폭: Large 150 / Medium 131 / Small 117 / Xsmall 105). 아이콘은 라벨 좌·우 양쪽에 배치.

**Size & Layout**

| Size | H | Padding X/Y | Radius | Icon | Gap |
|---|---|---|---|---|---|
| Large | 52 | 28 / 14 | 14 | 20 | 6 |
| Medium | 48 | 20 / 10 | 12 | 20 | 6 |
| Small | 40 | 20 / 8 | 10 | 16 | 4 |
| Xsmall | 34 | 14 / 8 | 10 | 16 | 4 |

높이 예외: `Medium/Assistive/Outlined/Normal`은 H 44, Xsmall Outlined 인스턴스는 H 36.

**Tokens**

| Size | Typography (Pretendard SemiBold) |
|---|---|
| Large | `Body04/Semibold` 16/24/-0.3%(실제 -0.048px) |
| Medium | `Body05/Semibold` 15/22/-0.3%(실제 -0.045px) |
| Small | `Body06/Semibold` 14/20/-0.3%(실제 -0.042px) |
| Xsmall | `Body06/Semibold` 14/20/-0.3%(실제 -0.042px) |

색상(Large 기준으로 조회):

| Color / Variant | Normal | Selected | Disabled |
|---|---|---|---|
| Primary / Solid | bg `foreground/brand/normal` (#2A7FEC), 텍스트 `label/inverse/inverse` (#FFFFFF) | bg `foreground/brand(blue)/brand(blue)-pressed` (#1E52AF), 텍스트 #FFFFFF | bg `foreground/brand/disabled` (#DEE3E7), 텍스트 `label/primary/disabled` (#8C9499) |
| Assistive / Solid | bg `foreground/normal/selected` (#EBEEF0), 텍스트 `label/secondary/normal` (#434648) | bg `foreground/normal/disabled-normal` (#CDD3D7), 텍스트 #434648 | bg `foreground/normal/disabled-subtle` (#EBEEF0), 텍스트 #8C9499 |
| Primary / Outlined | bg `static/white` (#FFFFFF), border 1px `line/normal/normal`(rgba(87,94,98,0.24)), 텍스트 #434648 | bg `foreground/normal/normal` (#F7F8F9), border·텍스트 동일 | bg #EBEEF0(`disabled-subtle`), border 동일, 텍스트 #8C9499 |
| Assistive / Outlined | bg #FFFFFF, border 1px `line/normal/neutral`(rgba(87,94,98,0.16)), 텍스트 #434648 | `[Figma에서 확인 불가]` | `[Figma에서 확인 불가]` |

Medium·Small·Xsmall의 Selected·Disabled·Assistive 색은 미조회(Primary/Solid/Normal만 확인: 모두 bg #2A7FEC, 텍스트 #FFFFFF).

**States**
Normal / Selected / Disabled. Interaction 오버레이(opacity 0 레이어) 채움색 — Primary Solid Large `label/secondary/normal`(#434648) / Primary Solid Medium·Small·Xsmall `label/inverse/inverse`(#FFFFFF) / Assistive Solid Large #434648 / Assistive Outlined Large Normal #434648 / Primary Outlined Normal 색 없음 / Primary Outlined Disabled #FFFFFF.두 Selected 예시 인스턴스에는 Interaction 레이어 자체가 없음. Hover/Press 시 실제 opacity 수치는 `[Figma에서 확인 불가]`(Figma 코멘트: "Normal에서 가중치 1.5가 적용된 값입니다").

### Button-icon

아이콘만 있는 원형/사각 버튼.

**Properties**

| Property | Values |
|---|---|
| `Color` | Primary \| Assistive |
| `Shape` | Box \| Round |
| `Size` | Large \| Medium \| Small |
| `State` | Normal \| Selected \| Disabled |

36개 조합. Border 없음. Hover/Pressed/Focus variant 없음.

**Size & Layout**

| Size | 전체 크기 | Padding(Normal) | Padding(Selected/Disabled) | Icon | Radius(Box) | Radius(Round) |
|---|---|---|---|---|---|---|
| Large | 56×56 | 12 | 12 | 32 | 12(`padding/12`) | 64(`number/64`) |
| Medium | 52×52 | 10 | 10 | 24 | 10(`padding/10`) | 64 |
| Small | 44×44 | 10 | 8 | 20 | 8(`padding/8`) | 64 |

**Tokens**

| Color / Shape / State | bg |
|---|---|
| Primary Normal | `foreground/brand/normal` (#2A7FEC) |
| Primary Selected | `foreground/brand/selected` (#1E52AF) |
| Primary Disabled | `foreground/brand/disabled` (#DEE3E7) |
| Assistive Box Normal | `foreground/normal/normal` (#F7F8F9) |
| Assistive Round Normal | `static/white` (#FFFFFF) |
| Assistive Selected | `foreground/normal/selected` (#EBEEF0) |
| Assistive Disabled | `foreground/normal/disabled-subtle` (#EBEEF0) |

Assistive Round의 Selected·Disabled는 미조회.

### Button-text

텍스트(+옵션 아이콘) 링크형 버튼.

**Properties**

| Property | Values |
|---|---|
| `Size` | XS \| S \| M \| L |
| `Status` | Normal \| Disabled \| Alternative |
| boolean | `showLeadingIcon`, `showTrailingIcon` |

12개 조합. Padding·Radius·Border 없음. 샘플 크기 XS 77×20 / S 90×24 / M 103×26 / L 108×28.

**Tokens**

| Size | Icon | Typography (Pretendard SemiBold) |
|---|---|---|
| L | 24 | `Body02/Semibold` 20/28/-0.4%(실제 -0.08px) |
| M | 24 | `Body03/Semibold` 18/26/-0.3%(실제 -0.054px) |
| S | 20 | `Body04/Semibold` 16/24/-0.3%(실제 -0.048px) |
| XS | 16 | `Body06/Semibold` 14/20/-0.3%(실제 -0.042px) |

텍스트색: Normal `label/secondary/normal`(#434648) / Disabled `label/primary/disabled`(#8C9499) / Alternative `label/primary/alternative`(#A2A9AE)

**States**
Normal / Disabled / Alternative. Hover/Pressed/Focus variant 없음.

### Button-check-box

**Properties**
`Status` = Selected | Default (light/dark 2벌)

**Tokens**
24×24 이미지 에셋(내부 색 `[Figma에서 확인 불가]`)

**Usage**
Check-box "전체동의": Selected → light/Selected, disabled → dark/Default. Check-box/item: Selected → light/Selected, Disabled → dark/Selected.

### Button-action-card

홈 화면 "앨범/파일에서 선택" 카드.

**Size & Layout**
W 161 × H 110, radius `Radius/16`(16px), padding top `Padding/14`(14px) / X `Padding/16`(16px) / bottom `Padding/8`(8px), `drop-shadow(0 0 1.5px rgba(134,134,134,0.04))`

**Tokens**
- bg `bg-secondary` (#FFFFFF)
- 라벨 좌상단: `Body05/Bold` 15/22/-0.045px `label/primary/normal` (#222426) — Gallery "앨범에서 선택", File "파일에서 선택"
- 우하단 `Img` 48×48(Gallery/File, light)

### Button-chip-filter

구 이름 "Chip/Date-filter".

**Properties**
`Type` = Preset(고정), `State` = Default | Selected. 텍스트 prop `text`("Title")

**Size & Layout**
H 36, W content-fit(Default 54 / Selected 55), padding X `Padding/12`(12px) / Y `Padding/8`(8px), gap `Padding/4`(4px), radius `Radius/10`(10px). Border·아이콘 없음

**Tokens**

| State | bg | 텍스트 |
|---|---|---|
| Selected | `bg-inverse` (#434648) | `Body05/Semibold` 15/22/-0.3%(실제 -0.045px) `label/inverse/inverse` (#FFFFFF) |
| Default | `foreground/normal/normal` (#F7F8F9) | `Body05/Medium` 15/22/-0.045px `label/primary/disabled` (#8C9499) |

---

## Textfield

Textfield, 트레일링 버튼, Dropdown-box, Dropdown-item-selectbox, Text-area 5종.

### Textfield

**Properties**

| Property | Values |
|---|---|
| `Status` | Normal \| Positive \| Negative |
| `Active(text)`, `Focus(stroke)`, `Disable`, `Trailing Button` | "True" \| "False" 문자열 |
| boolean | `heading`, `description`, `required`, `leadingContent`, `extra`, `trailingContent` |
| text | `text`("제목"), `text1`("보조 메시지가 들어갑니다."), `placeholder`("텍스트를 입력해 주세요.") |

16개 인스턴스 중 2개는 variant 이름이 서로 동일하다(Focus 예시 인스턴스, Node ID는 [Figma References](#figma-references) 참고).

**Size & Layout**
- W 335. Container H 56, 전체 H 114(Negative + Active(text)=True + 비포커스만 Input H 70, 전체 H 128)
- 세로 gap `Padding/8`(8px). Heading padding X `Padding/4`(4px), gap 4px. Description padding-left `Padding/8`(8px)
- Container: padding `Padding/12`(12px), gap 12px, radius `Radius/16`(16px)(트레일링 버튼 변형은 `Number/16`), border 1px
- 내부 Content gap `Padding/8`(8px), min-height 24, Text padding X `Padding/4`(4px)·gap `Padding/10`(10px)
- 슬롯: leadingContent 아이콘 24px, extra·trailingContent 24×24 자리

**Tokens**
- Heading: `Body05/Bold` 15/22/-0.3%(실제 -0.045px), `label/secondary/normal` (#434648)
- Required `*`: `Pretendard JP Medium` 14px, letter-spacing 0.203px, line-height 1.429, `status/rejected/normal` (#F44336)
- Placeholder/입력값: `Body04/Medium` 16/24/-0.3%(실제 -0.048px)
- Description(helper) 기본: `Body06/Medium` 14/20/-0.042px `label/secondary/selected` (#8C9499)
- Description(helper) Negative: `Body06/Regular` 14/20/-0.042px `status/rejected/normal` (#F44336)

**States**

| 상태 | Container 배경 | 테두리 | 텍스트 / 우측 요소 |
|---|---|---|---|
| Normal·빈값·trailing 없음 | `static/white`(#FFFFFF) | 1px `line/normal/normal`→rgba(87,94,98,0.24) | placeholder `label/primary/weak`(#BABEC2) |
| Normal·빈값·trailing 있음 | `foreground/normal/normal`(#F7F8F9) | 1px `line/normal/neutral`→rgba(87,94,98,0.16) | placeholder `label/primary/disabled`(#8C9499) + 트레일링 버튼 |
| Normal·입력값·trailing 없음 | #FFFFFF | `line/normal/normal` | 입력값 `label/primary/normal`(#222426) |
| Normal·입력값·trailing 있음 | #F7F8F9 | `line/normal/neutral` | 입력값 #222426 + 트레일링 버튼 |
| Focus | #FFFFFF | 1px `foreground/brand/normal`(#2A7FEC) | 입력값 #222426(max-w 275) + `Icon/close-circle/solid/20` |
| Positive·입력값 | #FFFFFF | `line/normal/neutral` | 입력값 #222426 + `Icon/check-circle/solid/20` |
| Disabled | `foreground/normal/disabled-subtle`(#EBEEF0) | `line/normal/neutral` | 텍스트 `label/primary/disabled`(#8C9499) |
| Negative·입력값·비포커스 | 바탕 `#FFFFFF`+`line/normal/neutral` 위에 테두리 1px **`status/rejected/normal`(#F44336)** | 입력 텍스트 없이 세로선(Vector H16)만 + `Icon/alert-circle/solid/20` | helper #F44336 |
| Negative·포커스 | 위와 동일(빨간 1px 테두리) | 입력값 #222426 + `Icon/close-circle/solid/20` | helper #F44336 |

위 9개 상태 + variant 이름이 겹치는 추가 인스턴스 1개 = 10개를 조회했고, 나머지 6개 인스턴스는 미조회다(목록은 [Figma References](#figma-references)). Hover/Pressed variant는 없다.

**Usage**
Figma 주석 — Normal·입력값: "영수증 등록 화면에서 사용됩니다." / Disabled: "증빙 상세-상세 내역 수정 화면에서 사용됩니다."

### 트레일링 버튼 (Textinput-resource-textfield-button)

**Properties**
`Variant` = Normal | Assistive, `Disable` = True | False (조합 3개: Normal/False, Assistive/False, Normal/True). 텍스트 prop `label`

**Size & Layout**
H 36, min-W 80, padding X `Padding/12`(12px) / Y `Padding/6`(6px), radius `Radius/10`(10px)

**Tokens**

| Variant | bg | 텍스트 | Border | 그림자 |
|---|---|---|---|---|
| Normal | `foreground/brand/normal`(#2A7FEC) | `label/inverse/inverse`(#FFFFFF) | 1px `line/normal/neutral` | Textfield 안: `0 1px 1px rgba(0,0,0,0.03)` / 단독 인스턴스: `0 1px 2px rgba(0,0,0,0.03)` |
| Assistive | 없음 | `label/primary/normal`(#222426) | 1px `line/normal/neutral` | `0 1px 2px rgba(0,0,0,0.03)` + 외곽 `drop-shadow(0 0 1.5px rgba(134,134,134,0.04))` |
| Disabled | `foreground/normal/disabled-normal`(#CDD3D7) | `label/secondary/selected`(#8C9499) | 없음 | `Shadow-Low` |

텍스트: `Body05/Medium` 15/22/-0.3%(실제 -0.045px)

**States**
Interaction 오버레이 opacity 0, radius 12, 채움색 Normal `foreground/brand/normal`(#2A7FEC) / Assistive `label/normal`(#171719). 실제 opacity 수치는 `[Figma에서 확인 불가]`(Figma 코멘트: "Normal에서 가중치 0.75가 적용된 값입니다").

### Dropdown-box

구 이름 "Program-select".

**Properties**
`Status` = Close | open | Dropdown-list (`open`은 소문자)

**Size & Layout**
- W 343
- Input Container(`Dropdown-item-input`): H 56, radius `Radius/16`(16px), padding `Padding/12`(12px)
- Dropdown-list(옵션 패널): W 339 × H 256

**Tokens**
- Heading: `Body05/Bold` 15/22/-0.045px `label/secondary/normal`(#434648) "프로그램" + Required `*`
- bg `bg-secondary`(#FFFFFF)
- Close: border 1px `line/normal/normal`→rgba(87,94,98,0.24), 우측 `Icon/chevron-down/20`
- open: border 1px `line/brand/normal`(#2A7FEC), 우측 `Icon/chevron-up/20`
- Placeholder: `Body04/Medium` 16/24/-0.048px `label/primary/weak`(#BABEC2) "프로그램을 선택해 주세요."
- Dropdown-list: border 1px `foreground/brand/normal`(#2A7FEC), radius 16, 스크롤바 W6 radius 64 `foreground/normal/disabled-normal`(#CDD3D7)

**States**
Close / open(Focus) / Dropdown-list(목록 펼침)

### Dropdown-item-selectbox

구 이름 "Dropdown-item".

**Properties**
`Status` = Dropdown-item-default | Dropdown-item-pressed | Dropdown-item-selected

**Size & Layout**
W 322 × H 56, padding `Padding/12`(12px), Text padding X `Padding/4`(4px)

**Tokens**

| Status | bg | 텍스트 | Radius |
|---|---|---|---|
| Default | `static/white`(#FFFFFF) | `Body04/Regular` 16/24/-0.048px `label/primary/weak`(#BABEC2) | 12 |
| Pressed | `foreground/brand/secondary-selected`(#EFF8FF) | `Body04/Regular` `label/primary/disabled`(#8C9499) | 12 |
| Selected | #EFF8FF | `Body04/Medium` 16/24/-0.048px `label/primary/normal`(#222426) | `Padding/10`(10px) |

### Text-area

적요 등 여러 줄 입력.

**Properties**
`State` = Default | Edited | Focus | Negative-active-false, `Active` = True

**Size & Layout**
- W 347 × H 172(Negative는 H 199, Input H 142)
- 세로 gap `Padding/8`(8px), Heading padding X `Padding/4`(4px)
- Input Container: padding `Padding/12`(12px), gap `Padding/10`(10px), radius `Radius/16`(16px), border 1px
- 본문 높이 80
- Byte 영역: padding-right `Padding/10`(10px)
- 스크롤바: W 6 × H 65, radius 64, right 5 / top -1(영역 H 122, padding-top 20)

**Tokens**
- Heading "적요": `Body05/Bold` 15/22/-0.045px `label/secondary/normal`(#434648) + Required `*`
- bg `static/white`(#FFFFFF)
- Border: Default·Edited `line/normal/normal` / Focus `line/brand/normal`(#2A7FEC) / Negative `status/rejected/normal`(#F44336)
- 본문: `Body04/Medium` 16/24/-0.048px — Default·Negative `label/primary/weak`(#BABEC2, placeholder "예시) 200회 '골때리는 개들' VCR 소품 구입(애완용 장난감 외)") / Edited·Focus `label/primary/normal`(#222426)
- 하단 페이드 `dim-down`: H 12 × W 323, `rgba(255,255,255,0)` → `bg-secondary`(#FFFFFF) 그라디언트(Negative는 `static/white`)
- Byte "0 / 100 Byte": `Body06/Medium` 14/20/-0.042px `label/primary/weak`(#BABEC2)
- 스크롤바: `foreground/normal/disabled-normal`(#CDD3D7)
- Negative helper: `Body06/Regular` 14/20/-0.042px `status/rejected/normal`(#F44336) "보조 메세지가가 들어갑니다."

---

## Check-box

Check-box(전체동의), Check-box/item 2종.

### Check-box (전체동의 카드형)

**Properties**
`state` = Selected | disabled (소문자). 텍스트 prop `lable`("전체동의")

**Size & Layout**
W 335 × H 60, padding X 17 / Y 19(raw), radius `Padding/16`(16px), border 1px `line/normal/neutral`→rgba(87,94,98,0.16), 아이콘-라벨 gap 10px

**Tokens**

| state | bg | 아이콘 |
|---|---|---|
| Selected | `foreground/normal/disabled-subtle`(#EBEEF0) | Button-check-box/light Selected(24×24) |
| disabled | `foreground/normal/normal`(#F7F8F9) | Button-check-box/dark Default(24×24) |

라벨: `Body03/Semibold` 18/26/-0.3%(실제 -0.054px) `label/primary/normal`(#222426)

### Check-box/item

**Properties**
`state` = Selected | Disabled, booleans `showBullet`, `showMainText`, `showStatusText`, `showSubText`

**Size & Layout**
W 335, padding left `Padding/8`(8px) / right `Padding/2`(2px) / Y `Padding/8`(8px), 내부 그룹 gap 16px, 아이콘-라벨 gap 10px, Label 내부 gap 1px

**Tokens**
- 아이콘: Selected → Button-check-box/light Selected, Disabled → Button-check-box/dark Selected (24×24)
- 우측 `Icon/chevron-right/20`
- 텍스트(전 상태 동일): `Body04/Medium` 16/24/-0.3%(실제 -0.048px) `label/primary/normal`(#222426) — "개인정보 수집" + Bullet("•") + "이용 동의" + "(필수)"

**States**
Selected / Disabled — 텍스트 색 변화 없음, 아이콘 이미지만 교체

---

## Date-picker

selectbox, calendar-item, Calendar, Month-navigator, Month-picker/item, Date-picker-rangebox, Month-picker/list 7종.

### Date-picker-selectbox

**Properties**
`Status` = Default | Selected

**Size & Layout**
W 168, 세로 gap `Padding/8`(8px). Container H 48, padding `Padding/12`(12px), radius `Radius/12`(12px), border 1px

**Tokens**
- bg `bg-secondary`(#FFFFFF)
- Border: Default `line/normal/neutral`→rgba(87,94,98,0.16) / Selected `line/brand/normal`(#2A7FEC)
- 라벨("시작일"): `Body05/Semibold` 15/22/-0.045px `label/primary/normal`(#222426)
- 날짜값: 같은 스타일, `label/brand/normal`(#2A7FEC)
- 아이콘 `Icon/Calendar/20`(좌측)

### Date-picker/calendar-item

**Properties**
`Type` = Date | month, `Status`(Date일 때) = Selected | Inactive | Default | Current

**Size & Layout**
- Date: 셀 내부 gap `Padding/10`(10px). Selected/Current 36×36(radius 29), Default/Inactive 37×35
- month(요일): 37×20

**Tokens**

| Status | bg | 텍스트 |
|---|---|---|
| Selected | `foreground/brand/normal`(#2A7FEC) | `label/inverse/inverse`(#FFFFFF) |
| Current | `foreground/brand/disabled`(#DEE3E7) | `label/secondary/normal`(#434648) |
| Default | 없음 | `label/primary/normal`(#222426) |
| Inactive | 없음 | `label/secondary/disabled`(#BABEC2) |

- Date 타이포: `Body04/Semibold` 16/24/-0.3%(실제 -0.048px)
- month 타이포: `Body06/Semibold` 14/20/-0.3%(실제 -0.042px) `label/secondary/weak`(#A2A9AE)

### Date-picker/Calendar

달력 컨테이너.

**Properties**
`Status` = Calendar-default | Calendar-selected

**Size & Layout**
- W 343 × H 318, border 1px `line/normal/neutral`→rgba(87,94,98,0.16), radius `Radius/20`(20px), padding `Padding/16`(16px), 세로 gap `Padding/20`(20px)
- 헤더 행: `Icon/chevron-left/24` + 가운데 그룹(W 147, gap `Padding/8`: 월 라벨 + `Icon/chevron-down-solid/16`) + `Icon/chevron-right/24`
- 요일 행과 날짜 영역 gap `Padding/16`(16px). 요일 행 7칸 각 37×20, gap `Padding/8`(8px). 날짜 영역 6행, 행 gap 8px, 셀 gap 8px, 셀 37×35(마지막 행 27·28·29일만 W 36)

**Tokens**
- bg `bg-secondary`(#FFFFFF)
- 월 라벨("2026년 8월"): `Body04/Semibold` 16/24/-0.048px `label/primary/normal`
- 요일 라벨: 일·월·화·수·목·금·토, [calendar-item](#date-pickercalendar-item) month 스타일

**States**
- Calendar-default: 23일이 Current 스타일(#DEE3E7 원형), 이전·다음 달 날짜는 Inactive(#BABEC2)
- Calendar-selected: default와 동일 + 8월 1일이 Selected(#2A7FEC 원형, 흰 글자), 23일 Current 유지

### Month-navigator

구 이름 "Calendar/month-chevron-button".

**Properties**
`Type` = navigator | label, `Status` = activated | disabled | "-", `Chevron` = next | previous | "-"

**Size & Layout**
navigator 20×20 / label content-fit(W 41 × H 34), padding X `Padding/2`(2px)

**Tokens**
- navigator: 20×20 이미지 에셋 4종(내부 색 `[Figma에서 확인 불가]`)
- label("9월"): `Heading03/Bold` 24/34/-0.4%(실제 -0.096px), `label/primary/normal`(#222426)

**States**
navigator activated/disabled × next/previous 4종 + label 1종

### Month-picker/item

구 이름 "Month-picker-dropdown-item".

**Properties**
`Property 1` = Dropdown-month-item-default | -selected | -pressed

**Size & Layout**
W 120 × H 40, padding X `Padding/12`(12px) / Y `Padding/8`(8px), Content gap `Padding/6`(6px), Text padding X `Padding/4`(4px)

**Tokens**

| Property 1 | bg |
|---|---|
| default | `bg-secondary`(#FFFFFF) |
| selected | `foreground/normal/selected`(#EBEEF0) |
| pressed | `foreground/normal/weak`(#F1F3F4) |

텍스트("2026년 8월"): `Body06/Semibold` 14/20/-0.3%(실제 -0.042px) `label/primary/normal`(#222426)

### Date-picker-rangebox

시작일~종료일 기간 표시 필드.

**Size & Layout**
- W 335 × H 44(고정), padding X `Padding/16`(16px) / Y `Padding/12`(12px, 실제 상하 여백은 10px — H가 44로 고정이라 24px 콘텐츠가 세로 가운데에 놓임)
- 바깥 프레임 gap `Padding/12`(12px), Content(icon–text) gap `Padding/8`(8px)

**Tokens**
- radius `Radius/14`(14px), border 1px `label/secondary/normal`(#434648, 불투명 — `line/*` 토큰 아님), bg `static/white`(#FFFFFF)
- 좌측 `Icon/Calendar/24`(24px)
- 날짜 범위 "26.08.11 ~ 26.09.10": `Body04/Medium` 16/24/-0.3%(실제 -0.048px) `label/primary/normal`(#222426), 날짜·`~` 사이 gap `Padding/4`(4px)
- 우측 `Icon/close-circle/solid/20`

**States**
variant 없음(단일 상태). Focus/Disabled 등 `[Figma에서 확인 불가]`

### Month-picker/list

**Size & Layout**
W 120 × H 180, border 1px `line/normal/neutral`, radius `Radius/12`(12px), overflow clip. Month-picker/item 세로 나열(2026년 9월 selected, 8·7·6·5월 default). 스크롤바 W 6 × H 100, right 7 / top -1(영역 H 180, padding Y `Padding/10`)

**Tokens**
bg `bg-secondary`(#FFFFFF), `Shadow-Medium`(0 0 10px rgba(134,134,134,0.32)), 스크롤바 `foreground/normal/disabled-normal`(#CDD3D7)

---

## Figma References

파일: `[SBS] OCR 프로젝트_디자인` (`ese9l01OJiDfirO8Q6XXIY`), "🔵 디자인시스템" 페이지.

### Button

| 컴포넌트 | Node ID |
|---|---|
| Button(섹션 전체) | 165:19713 |
| Button-solid | 165:19718 |
| Button-solid — Medium/Assistive/Outlined/Normal(H44 예외) | 165:19953 |
| Button-solid — Selected 예시 인스턴스 | 165:19719, 174:5200 |
| Button-icon | 165:20132 |
| Button-text | 183:19951 |
| Button-check-box(상위) | 2449:85648 |
| Button-check-box/light | 1156:24613 |
| Button-check-box/dark | 1908:62400 |
| Button-action-card/Gallery | 682:15733 |
| Button-action-card/File | 682:15734 |
| Button-chip-filter | 207:11770 |

### Textfield

| 컴포넌트 | Node ID |
|---|---|
| Textfield(섹션 전체) | 165:18856 |
| Textfield | 165:18907 |
| Textfield — Normal·빈값·trailing 없음 | 165:18908 |
| Textfield — Normal·빈값·trailing 있음 | 175:5641 |
| Textfield — Normal·입력값·trailing 없음 | 165:18923 |
| Textfield — Normal·입력값·trailing 있음 | 175:5656 |
| Textfield — Focus | 165:19074 |
| Textfield — Positive·입력값 | 165:19122 |
| Textfield — Disabled | 165:18938 |
| Textfield — Negative·입력값·비포커스 | 165:19008 |
| Textfield — Negative·포커스 | 165:19052 |
| Textfield — variant 이름이 겹치는 추가 인스턴스 | 2450:69913 |
| Textfield — 미조회 인스턴스 | 165:18986, 175:5719, 175:5741, 175:5781, 175:5818, 175:5850 |
| 트레일링 버튼(Textinput-resource-textfield-button) | 165:18863 |
| 트레일링 버튼 — 단독 인스턴스(그림자 확인용) | 165:18864 |
| Dropdown-box | 635:15003 |
| Dropdown-item-selectbox | 1084:30439 |
| Text-area | 998:20871 |

### Check-box

| 컴포넌트 | Node ID |
|---|---|
| Check-box(섹션 전체) | 364:10667 |
| Check-box(전체동의 카드형) | 299:7842 |
| Check-box/item | 306:15060 |

### Date-picker

| 컴포넌트 | Node ID |
|---|---|
| Date-picker(섹션 전체) | 239:13371 |
| Date-picker-selectbox | 300:1493 |
| Date-picker/calendar-item | 300:9351 |
| Date-picker/Calendar | 2449:90679 |
| Month-navigator | 2449:87700 |
| Month-picker/item | 1165:19265 |
| Date-picker-rangebox | 2097:67358 |
| Month-picker/list | 751:21624 |
