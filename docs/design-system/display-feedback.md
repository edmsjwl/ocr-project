# Display & Feedback

> 상위 문서: [DESIGN.md](../../DESIGN.md)
> Figma: `[SBS] OCR 프로젝트_디자인` 🔵 디자인시스템 페이지

Badge, Progress, Action-Area.

---

## Badge

Content-badge, Category-badge 2종.

### Content-badge

상태/색상 배지.

**Properties**
`Color` = Blue | Gray | Black | Green | Red, `Size` = Large | Medium | Small (15개 조합)

**Size & Layout**

| Size | Padding X/Y | Radius |
|---|---|---|
| Large | 12 / 6 | 10 |
| Medium | 10 / 3 | 8 |
| Small | 6 / 3 | 8 |

수직·수평 가운데 정렬.

**Tokens**

| Size | Typography |
|---|---|
| Large | `Body05/Bold` 15/22/-0.3%(실제 -0.045px) |
| Medium | `Body06/Bold` 14/20/-0.3%(실제 -0.042px) |
| Small | `Caption01/Semibold` 13/19/-0.2%(실제 -0.026px) |

| Color | bg | 텍스트 |
|---|---|---|
| Blue | `status/pending/subtle` → rgba(225,245,254,0.64) | `status/pending/normal`(#03A9F4) |
| Green | `status/processing/subtle` → rgba(232,245,233,0.64) | `status/processing/normal`(#43A047) |
| Red | `status/rejected/subtle` → rgba(255,235,238,0.64) | `status/rejected/normal`(#F44336) |
| Gray | `status/completed/subtle` → rgba(241,243,244,0.72) | `status/completed/normal`(#8C9499) |
| Black | `foreground/normal/weak`(#F1F3F4) | `label/primary/selected`(#575E62) |

subtle 계열 bg는 [foundation.md → Color](foundation.md#color)의 opacity 규칙대로 rgba로 렌더한다.

**Usage**
- 조회한 인스턴스: Small 5색 전부, Medium Black, Large Green(나머지 조합은 동일 규칙으로 정의되어 있으나 개별 조회는 안 함)
- "완료" 배지는 Modal-영수증상태·File-attachment에서 Black 색으로, Card-item-receipt-list에서는 Gray 색으로 쓰인다

### Category-badge

카드 종류(개인/법인) 배지.

**Properties**
`Style` = Round | Square, `Type` = Round(`personal-card`\|`corporate-card`) / Square(`personal`\|`corporate`), `Mode` = Round(`Light`\|`Dark`) / Square(`light`\|`dark`), `Status` = Default | Selected(2026-11 재확인 시 신규 추가 확인 — 기존엔 문서화돼 있지 않았음)

**Size & Layout**
- Round: gap `Padding/4`(4px), padding X 8 / Y 3, radius 999(pill)
- Square: 48×48, radius `Radius/16`(16px), padding X `Padding/8`(8px) / Y `Padding/3`(3px), 세로 배치(아이콘 24px + 라벨)

**Tokens**

⚠️ 2026-11 재확인 결과 Dark 배경값이 기존 문서(Personal rgba(30,82,175,0.16), Corporate rgba(241,243,244,0.04))와 달랐다 — 아래는 라이브로 다시 확인한 값이다.

Round:

| Type | Mode | Default | Selected |
|---|---|---|---|
| Personal | Light | `clear-blue/5`(#EFF8FF) | `clear-blue/10`(#DBEEFE) |
| Personal | Dark | rgba(42,127,236,0.16) | rgba(42,127,236,0.4) |
| Corporate | Light | `cool-neutral/10`(#F1F3F4) | Default와 동일(시각적 구분 없음) |
| Corporate | Dark | rgba(241,243,244,0.08) | rgba(241,243,244,0.32) |

Square:

| Type | Mode | Default | Selected |
|---|---|---|---|
| Personal | Light | `clear-blue/5`(#EFF8FF) | `clear-blue/10`(#DBEEFE) |
| Personal | Dark | rgba(42,127,236,0.16) | rgba(42,127,236,0.4) |
| Corporate | Light | `cool-neutral/10`(#F1F3F4) | `cool-neutral/15`(#EBEEF0) |
| Corporate | Dark | rgba(241,243,244,0.08) | rgba(241,243,244,0.32) |

Round과 달리 Square는 Corporate/Light에서도 Default·Selected가 시각적으로 구분된다(Round/Corporate/Light만 예외).

- Round 텍스트 `Caption01/Semibold` 13/19/-0.026px: Personal-Light `label/primary/normal`(#222426) / Personal-Dark #F7F8F9 / Corporate-Light `label/secondary/normal`(#434648) / Corporate-Dark #CDD3D7
- Square 라벨("개인"/"법인"): `Caption02/Semibold` 12/18/-0.2%(실제 -0.024px) — Personal-Light `label/primary/normal`(#222426) / Personal-Dark #F7F8F9 / Corporate-Light `label/secondary/normal`(#434648) / Corporate-Dark #CDD3D7 (2026-11 재확인으로 Dark·Corporate 값도 확정, 이전엔 Personal-light만 확인된 상태였음)
- 카드 아이콘 24px(이미지 에셋)

---

## Progress

Progress-bar 1종.

### Progress-bar

**Properties**
`Progress` = Step-1 | Step-2 | Step-3

**Size & Layout**
트랙 W 212 × H 6, radius 64

**Tokens**
- 트랙 bg `foreground/normal/selected`(#EBEEF0)
- 인디케이터 bg `foreground/brand/normal`(#2A7FEC)

**States**

| Step | 인디케이터 폭 |
|---|---|
| Step-1 | 71 |
| Step-2 | 141 |
| Step-3 | 212(트랙 전체) |

---

## Action-Area

Action-area 1종.

### Action-area

화면 하단 고정 CTA 영역.

**Properties**
`Type` = One-button | Two-button, `Color` = White | Default | Dark, `Variant` = Strong | Neutral | Normal | Wide, boolean `alternative`

실제 존재하는 12개 조합(전체 목록·Node ID는 [Figma References](#figma-references) 참고):

| Color | One-button | Two-button(밋밋한 형태) | Two-button/Wide | Two-button/Strong |
|---|---|---|---|---|
| White | Normal | `Normal` | 있음 | 있음 |
| Default | Normal | `Neutral` | 있음 | 있음 |
| Dark | Normal | `Neutral` | 있음 | 있음 |

같은 형태의 Two-button이 White에서는 variant명 `Normal`, Default·Dark에서는 `Neutral`로 다르다([foundation.md → 명명 불일치](foundation.md#명명-불일치) 참고).

**Size & Layout**
- W 375. Contents 영역 padding: top `Padding/10`(10px) / X `Padding/20`(20px) / bottom `Padding/20`(20px)
- 버튼: H 52, radius 14, padding X 28 / Y 14
- Two-button Normal/Neutral: Alternative(flex 1) + Main(flex 1), gap 10px
- Two-button Wide: Alternative(flex 1) + Main(폭 220 고정), gap 10px
- Two-button Strong: Main(가로 전체) 아래 Button-text "대체" 세로 배치(Dark의 Contents gap `Padding/12` 12px)
- Home-bar(하단): W 375, padding top 16 / bottom 6 / X 10, Slider W 134×H 5 radius 4

**Tokens**
- 버튼 텍스트: `Body04/Semibold` 16/24/-0.3%(실제 -0.048px)
- Main Action bg: White·Default `foreground/brand/normal`(#2A7FEC) / Dark #3B99F6. 텍스트 대부분 #FFFFFF(One-button/White/Normal만 `bg-primary` #F7F8F9)
- Alternative Action(Two-button): bg `static/white`(Dark #222426) + border 1px `line/normal/neutral`→rgba(87,94,98,0.16), 텍스트 `label/secondary/normal`(Light #434648 / Dark #CDD3D7)
- 배경 그라디언트(Contents 영역 상단→하단): White·Default `linear-gradient(180.23deg, rgba(255,255,255,0) 0.91%, rgba(255,255,255,0.53) 24.99%, bg-secondary #FFFFFF 50.0%)` / Dark `linear-gradient(180.34deg, rgba(22,25,26,0) 0.91%, rgba(22,25,26,0.68) 16.49%, bg-primary(dark) #191A1B 36.55%)`. Default 그라디언트는 `[Figma에서 확인 불가]`
- Home-bar 배경: White `bg-secondary`(#FFFFFF) / Dark `bg-primary(dark)`(#191A1B) / Default `bg-alternative`(#F1F3F4, 미조회). Slider bg `bg-inverse`(#434648)
- Interaction 오버레이(opacity 0) 채움색: White One-button/Normal `label/primary/normal`(#222426), White Two-button/Normal·Wide 메인 `label/normal`(#171719), Dark Strong #CDD3D7

**Usage**
Figma dev 주석: "변경 전: Two Button / 변경 후: One Button + Text Button" — Two-button/White/Strong 폐기 예정을 시사하는 것으로 보이나 정확한 대상은 `[Figma에서 확인 불가]`

---

## Figma References

파일: `[SBS] OCR 프로젝트_디자인` (`ese9l01OJiDfirO8Q6XXIY`), "🔵 디자인시스템" 페이지.

| 컴포넌트 | Node ID |
|---|---|
| Badge(섹션 전체) | 324:9408 |
| Content-badge | 324:9396 |
| Category-badge(섹션 전체) | 375:8105 |
| Category-badge — Round/personal-card/Light/Default | 375:7985 |
| Category-badge — Round/personal-card/Light/Selected(신규) | 3433:67880 |
| Category-badge — Round/personal-card/Dark/Default | 1540:30581 |
| Category-badge — Round/personal-card/Dark/Selected(신규) | 3433:67954 |
| Category-badge — Round/corporate-card/Light/Default | 375:7984 |
| Category-badge — Round/corporate-card/Light/Selected(신규, Default와 시각적 동일) | 3433:67931 |
| Category-badge — Round/corporate-card/Dark/Default | 1540:30584 |
| Category-badge — Round/corporate-card/Dark/Selected(신규) | 3433:68005 |
| Category-badge — Square/personal/Light/Default | 1959:44234 |
| Category-badge — Square/personal/Light/Selected(신규) | 3433:68064 |
| Category-badge — Square/personal/Dark/Default | 1959:44186 |
| Category-badge — Square/personal/Dark/Selected(신규) | 3433:68068 |
| Category-badge — Square/corporate/Light/Default | 1959:44235 |
| Category-badge — Square/corporate/Light/Selected(신규) | 3433:68107 |
| Category-badge — Square/corporate/Dark/Default | 1959:44185 |
| Category-badge — Square/corporate/Dark/Selected(신규) | 3433:68135 |
| Progress(섹션 전체) | 2112:92010 |
| Progress-bar | 427:17502 |
| Action-Area(섹션 전체) / Action-area | 196:7993 |
| Action-area — White / One-button / Normal | 300:9499 |
| Action-area — White / Two-button / Normal | 208:10254 |
| Action-area — White / Two-button / Wide | 300:10696 |
| Action-area — White / Two-button / Strong | 196:8039 |
| Action-area — Default / One-button / Normal | 300:9505 |
| Action-area — Default / Two-button / Neutral | 208:10431 |
| Action-area — Default / Two-button / Wide | 300:10702 |
| Action-area — Default / Two-button / Strong | 208:9979 |
| Action-area — Dark / One-button / Normal | 1858:42701 |
| Action-area — Dark / Two-button / Neutral | 1858:42706 |
| Action-area — Dark / Two-button / Wide | 1858:42712 |
| Action-area — Dark / Two-button / Strong | 1858:42718 |
