# Containers & Overlays

> 상위 문서: [DESIGN.md](../../DESIGN.md)
> Figma: `[SBS] OCR 프로젝트_디자인` 🔵 디자인시스템 페이지

Bottom-sheet, Card, Image-input, Modal.

---

## Bottom-sheet

프리셋 내부의 padding·gap·radius·color 세부값은 `[Figma에서 확인 불가]`(조회 범위 밖) — 확인된 것은 구성과 크기뿐이다.

**Properties / Size & Layout**

| 프리셋 | 구성 | 크기 |
|---|---|---|
| Bottom-sheet-datepicker | `Status=시작일,Calendar=True` · `Status=Default,Calendar=False` · `Status=종료일,Calendar=True` · `Status=Month-picker,Calendar=True` | 375×705(Default만 375×708) |
| Component 3 | `Status=Default` · `Status=Dropdown` · `Status=Current` | 각 375×522 |
| Bottom-sheet-time-selected | `Header`(375×56) + `Time-picker/Open` 인스턴스(335×252, 세부 스펙 `[Figma에서 확인 불가]`) + 숨김 `Date-picker/Calendar`(335×318, hidden) + `Action-area`(375×109) | 375×453 |

Bottom-sheet-datepicker는 `Bottom-sheet` 프레임 하위에 있고, Component 3·Bottom-sheet-time-selected는 같은 캔버스의 독립 배치다.

---

## Card

Card-item-receipt-list, Card-item-recipt-error, Card-info, Uploader-file 4종.

### Card-item-receipt-list

영수증 내역 리스트 행.

**Properties**
`Card` = 개인카드 | 법인카드, `Type` = 대기 | 처리중 | 완료 | 반려, `Red dot` = True | False (16개 조합)

**Size & Layout**
- W 375, H 49. Auto Layout horizontal, padding X `Padding/20`(20px), 바깥 gap `Padding/8`(8px), 배지-텍스트 gap `Padding/12`(12px). Radius·Border 없음
- 텍스트 블록 gap `Padding/2`(2px): 1행(거래처명 + 금액, 행 gap `Padding/20`), 2행(날짜·시간 gap `Padding/6` + 상태 배지)
- 상태 배지: padding X 6 / Y 3, radius 8
- Red dot(안읽음): 좌상단 left 12 / top 1, 6×24 이미지 에셋

**Tokens**
- bg `bg-secondary`(#FFFFFF)
- 좌측 Category-badge Square(48×48, radius 16): 개인 bg `#EFF8FF`, 법인 bg `#F1F3F4`(→ [06-display-feedback.md → Category-badge](06-display-feedback.md#category-badge))
- 거래처명: `Body05/Medium` 15/22/-0.045px `label/secondary/normal`(#434648, 말줄임)
- 금액: `Body05/Bold` 15/22 `label/primary/normal`(#222426), "128,000" + "원"(gap `Padding/2`)
- 날짜·시간: `Body06/Medium` 14/20/-0.042px `label/secondary/weak`(#A2A9AE)
- 상태 배지(`Caption01/Semibold` 13/19): 대기 bg `status/pending/subtle` 텍스트 #03A9F4 / 처리중 bg `status/processing/subtle` 텍스트 #43A047 / 완료 bg `status/completed/subtle` 텍스트 #8C9499 / 반려 bg `status/rejected/subtle` 텍스트 #F44336

**States**
대기/처리중/완료/반려 × 안읽음(Red dot) on/off — 8가지 조합 전수 확인

### Card-item-recipt-error

이름의 "recipt"는 Figma 원본 오타 그대로. 영수증 인식 실패 카드.

**Size & Layout**
W 335 × H 58, padding X `Padding/20`(20px) / Y `Padding/16`(16px), radius `Radius/14`(14px), border 1px `line/normal/neutral`→rgba(87,94,98,0.16). Info 영역 W 293(justify-between), 파일명 W 253

**Tokens**
- bg `static/white`(#FFFFFF)
- 파일명: `Body06/Medium` 14/20/-0.042px `label/secondary/normal`(#434648, 말줄임) — 예 "스타벅스_영수증_20260918.jpg"
- 우측 `Img-warning/24`(24×24)

**States**
단일 상태(에러 전용 카드, variant 없음)

**Usage**
Figma 주석: Container "아이콘 수정되었습니다." / 아이콘 "영수증 등록 인식 실패 화면에 사용되는 카드 ui입니다."

### Card-info

Red(경고)/Blue(정보) 겸용. 예전 이름 "Card-warning"이었으나 실제로는 경고 전용이 아니다.

**Properties**
`Size` = S | M, `Color` = Red | Blue — 존재 조합: S/Red, M/Red, M/Blue(S/Blue 없음)

**Size & Layout**
- S/Red: W 310 × H 36 / M/Red·M/Blue: W 335 × H 44
- padding X `Padding/14`(14px) / Y `Padding/12`(12px, M만), gap `Padding/8`(8px), 아이콘 좌측 16px

**Tokens**

| Color | bg | radius | 아이콘 | 텍스트 색 |
|---|---|---|---|---|
| Red | `status/rejected/subtle` | `Radius/10`(10px, 미재조회) | `alert-circle/16` | `label/primary/normal`(#222426) |
| Blue(M) | `status/pending/subtle` | `Radius/12`(12px, 실측) | `Icon/info-solid/16` | `label/secondary/selected`(#8C9499) |

타이포: M `Body06/Semibold` 14/20/-0.042px / S `Caption01/Semibold` 13/19/-0.026px

### Uploader-file

**Properties**
`Focus` = False | True

**Size & Layout**
W 335, 세로 gap `Padding/10`(10px), padding `Padding/12`(12px), radius `Radius/14`(14px). 내부 Row gap `Padding/6`(6px), 파일명-용량 gap `Padding/8`(8px)

**Tokens**
- bg `static/white`(#FFFFFF)
- Border: False 1px `line/normal/neutral` / True 2px `label/brand/normal`(#2A7FEC)
- `Icon/file-upload/24`(20px로 배치) + 파일명(`Body04/Medium` 16/24/-0.048px `label/primary/normal`(#222426), "파일명"에 밑줄 + ".pdf", max-W 228, 말줄임) + 용량 "300KB"(`Caption01/Medium` 13/19/-0.026px `label/secondary/selected`(#8C9499))

---

## Image-input

Thumbnail, Image-viewer ×2, Img-thumbnail, File-attachment 5종.

### Thumbnail-375*541

**Size & Layout**
W 375 × H 541, object-cover 이미지. 색상·타이포 없음

### Image-viewer-343*140

확대 미리보기(리스트용, M/S 2사이즈).

**Properties**
`Size` = M | S

**Size & Layout**
- M 343×140 / S 311×126, radius `Radius/20`(20px), border M 1px(S 0.907px)
- 우측 중앙 확대 버튼: radius 64, padding 10, M 52×52(아이콘 24px) / S 44×44(아이콘 20px)

**Tokens**
- border `line/normal/normal`→rgba(87,94,98,0.24)
- 이미지 위 Dim `rgba(0,0,0,0.08)`
- 확대 버튼 bg `static/white`(#FFFFFF), 아이콘 `search`

**Usage**
Figma 주석: "Image preview — 실제 영수증이 들어간 예시 화면입니다."

### Image-viewer-375*591

이름은 591이지만 실제 크기는 W 375 × H 541([01-foundation.md → 명명 불일치](01-foundation.md#명명-불일치) 참고).

**Size & Layout**
W 375 × H 541. 내부에 Thumbnail-375*541을 꽉 채워 배치

**Tokens**
bg `foreground/normal/disabled-normal`(#CDD3D7)

### Img-thumbnail

파일 선택 후 썸네일.

**Properties**
`State` = Default | Selected

**Size & Layout**
76×76, radius `Radius/12`(12px), 이미지 object-cover

**Tokens**

| State | Border | 오버레이 |
|---|---|---|
| Default | 1px `line/normal/normal`→rgba(87,94,98,0.24) | `rgba(0,0,0,0.08)` |
| Selected | 2px `line/brand/normal`(#2A7FEC) | `rgba(42,127,236,0.14)` |

### File-attachment

**Size & Layout**
W 343, radius `Padding/20`(20px), padding X `Padding/32`(32px) / Y `Padding/20`(20px), 가운데 정렬, 세로 gap `Padding/10`(10px). 이름-배지 gap `Padding/4`(4px)(max-W 279), 이름 행-용량 gap `Padding/2`(2px)

**Tokens**
- bg `bg-secondary`(#FFFFFF)
- `Icon/file/24` + 파일명 `Body05/Medium` 15/22/-0.045px `label/primary/normal`(#222426, max-W 238, 말줄임) — 예 "파일명이 들어갑니다"
- 확장자 배지("PDF"): bg `foreground/normal/weak`(#F1F3F4), padding X 6 / Y 3, radius 8, `Caption01/Semibold` 13/19/-0.026px `label/primary/selected`(#575E62)
- 용량 "300KB": `Caption01/Medium` 13/19/-0.026px `label/secondary/selected`(#8C9499)

---

## Modal

Modal-button, Modal-list-item, Modal-영수증상태, Modal/권한 4종.

### Modal-button

일반 확인/취소 모달.

**Properties**
`Type` = One-button | Two-button, `Variant` = Normal | Strong | Wide. 존재 조합 4개: One-button/Normal, Two-button/Normal, Two-button/Wide, Two-button/Strong. Booleans `description`, 텍스트 props `title`, `text`

**Size & Layout**
- W 343, radius `Radius/20`(20px), padding-top `Padding/36`(36px), Container 세로 gap `Padding/20`(20px)
- Text 영역: padding X `Padding/32`(32px), gap `Padding/12`(12px), 가운데 정렬
- Action-area: padding top `Padding/10`(10px) / X `Padding/20`(20px) / bottom `Padding/20`(20px)(Strong은 `Padding/22` 22px)

**Tokens**
- bg `foreground/normal/normal`(#F7F8F9), `drop-shadow(0 0 5px rgba(134,134,134,0.32))`
- 제목: `Body03/Bold` 18/26/-0.3%(실제 -0.054px) `label/primary/normal`(#222426)
- 설명(옵션): `Body04/Medium` 16/24/-0.048px `label/primary/alternative`(#A2A9AE)

**States(Variant별 버튼 구성)**

| Variant | 구성 |
|---|---|
| One-button/Normal | Solid 버튼 1개, H 52, radius 14, padding X 28/Y 14, bg #2A7FEC, 텍스트 #FFFFFF, 가로 전체 폭 |
| Two-button/Normal | Outlined(bg #FFFFFF, border 1px `line/normal/normal`, 텍스트 #434648) + Solid, 각 flex 1, gap 10px, H 52 |
| Two-button/Wide | Outlined(flex 1) + Solid(폭 180 고정), gap 10px, Container H 158 |
| Two-button/Strong | Solid(가로 전체) 아래 Button-text(S, Alternative, 아이콘 없음), 세로 gap `Padding/16`(16px) |

### Modal-list-item

사진/파일 선택 액션시트 항목.

**Properties**
`Type` = Photo | File

**Size & Layout**
세로 Auto Layout, padding Y `Padding/4`(4px), 내부 행 가로 gap 15px, 아이콘-라벨 gap 10, 라벨 내부 gap 2px

**Tokens**
- 아이콘 `Img-upload/32`(32×32, Gallery|File, light)
- 라벨: `Body03/Medium` 18/26/-0.3%(실제 -0.054px) `label/primary/normal`(#222426) + "[필수]" `label/brand/normal`(#2A7FEC)
- 설명: `Body04/Medium` 16/24/-0.048px `label/secondary/selected`(#8C9499) — Photo "앨범에서 영수증 이미지 첨부" / File "파일에서 영수증 이미지 첨부"

### Modal-영수증상태

영수증 상태 안내 모달.

**Size & Layout**
- W 311, radius `Radius/20`(20px), padding-top `Padding/24`(24px). Container 세로 gap `Padding/16`(16px), 안쪽 그룹 gap `Padding/28`(28px)
- 목록 padding X `Padding/20`(20px), 세로 gap `Padding/12`(12px). 각 행: 배지 열 W 50 + 설명(padding X `Padding/3`), gap `Padding/10`(10px)
- Action-area: padding top 10 / X 20 / bottom 20

**Tokens**
- bg `bg-secondary`(#FFFFFF), `drop-shadow(0 0 5px rgba(134,134,134,0.32))`
- 제목 "영수증 상태": `Body02/Bold` 20/28/-0.4%(실제 -0.08px) `label/primary/normal`(#222426)
- 설명: `Body05/Medium` 15/22/-0.045px `label/secondary/normal`(#434648), 2줄
- Action-area 버튼: Solid H 52(radius 14, padding X 28/Y 14, bg #2A7FEC), 텍스트 "닫기" `Body04/Semibold` 16/24 #FFFFFF, 가로 전체 폭

**States(행별 배지)**

| 상태 | 배지 bg | 배지 텍스트 | 폭 | 설명 |
|---|---|---|---|---|
| 반려 | `status/rejected/subtle` | #F44336 | 39 | "반려된 내역입니다. 상세에서 사유를 확인할 수 있습니다." |
| 대기 | `status/pending/subtle` | #03A9F4 | 39 | "증빙으로 사용되기 전이며 수정할 수 있습니다." |
| 처리중 | `status/processing/subtle` | #43A047 | 50 | "증빙으로 사용되어 수정할 수 없습니다." |
| 완료 | `foreground/normal/weak`(#F1F3F4) | `label/primary/selected`(#575E62) | 39 | "정산이 완료된 내역입니다."(행 세로 가운데 정렬) |

배지 공통: padding X 6 / Y 3, radius 8, `Caption01/Semibold` 13/19/-0.026px

### Modal/권한

앱 접근 권한 안내. A·B·D·E 4개 변형(C 없음).

**Size & Layout**
- 각 W 343 × H 428, radius 20, padding-top `Padding/36`(36px), Container 세로 gap `Padding/16`(16px)
- Text 영역: padding X `Padding/32`(32px), gap `Padding/10`(10px), 가운데 정렬
- 목록: padding X `Padding/20`(20px), 세로 gap `Padding/4`(4px). 항목 padding X `Padding/16`(16px) / Y `Padding/10`(10px), 가로 gap `Padding/20`(20px)
- 안내문: padding X `Padding/28`(28px)
- Action-area: padding top 10 / X 20 / bottom 20

**Tokens**
- bg `foreground/normal/normal`(#F7F8F9), `drop-shadow(0 0 5px rgba(134,134,134,0.32))`
- 제목: `Body02/Bold` 20/28/-0.4%(실제 -0.08px) `label/primary/normal`(#222426)
- 설명: `Body04/Medium` 16/24/-0.048px `label/primary/selected`(#575E62), 2줄
- 목록 항목: 아이콘 `Img-upload/32`(Gallery|File, light), 1행 "사진"/"파일" `Body04/Semibold` 16/24/-0.048px #222426 + 태그, 2행 설명 `Body06/Medium` 14/20/-0.042px `label/secondary/selected`(#8C9499, W 201) — Gallery "앨범에서 영수증 이미지 첨부", File "파일에서 영수증 이미지 첨부"
- 안내문: `Body06/Medium` 14/20/-0.042px `label/primary/alternative`(#A2A9AE) "영수증 등록을 위해 필요한 필수 권한이며, 권한을 / 허용하지 않을 경우 서비스 이용이 제한될 수 있어요."
- Action-area 버튼: Solid H 52(radius 14, bg #2A7FEC), 텍스트 `Body04/Semibold` 16/24 #FFFFFF, 가로 전체 폭

**States(변형별 문구)**

| 변형 | 제목 | 설명 | 태그 | 버튼 |
|---|---|---|---|---|
| A | 앱 접근 권한 안내 | 더 나은 서비스 이용을 위해 / 아래의 접근 권한 허용이 필요해요. | [필수] `label/brand/normal`(#2A7FEC) | 확인했어요 |
| B | 앱 접근 권한 안내 | 필수 권한이 일부 해제되어 있어요. / 설정에서 권한 허용 후 다시 시도해주세요. | [허용됨] `status/processing/normal`(#43A047) | 확인했어요 |
| E | 설정에서 권한을 허용해주세요 | 필수 권한이 꺼져 있어요. 기기 설정에서 / 권한을 허용한 뒤 돌아와주세요. | [허용됨] #43A047 | 설정으로 이동 |
| D | 필수 권한이 꺼져있어요 | 서비스를 계속 이용하려면 / 권한을 허용해주세요. | [허용됨] #43A047 | 확인했어요 |

---

## Figma References

파일: `[SBS] OCR 프로젝트_디자인` (`ese9l01OJiDfirO8Q6XXIY`), "🔵 디자인시스템" 페이지.

| 컴포넌트 | Node ID |
|---|---|
| Bottom-sheet(섹션 전체) | 307:9223 |
| Bottom-sheet-datepicker(상위) | 1141:23221 |
| Bottom-sheet-datepicker — 시작일 | 300:9777 |
| Bottom-sheet-datepicker — Default | 2078:70148 |
| Bottom-sheet-datepicker — 종료일 | 1141:21405 |
| Bottom-sheet-datepicker — Month-picker | 1141:22837 |
| Component 3(상위) | 1162:25378 |
| Component 3 — Default | 998:26027 |
| Component 3 — Dropdown | 998:26026 |
| Component 3 — Current | 998:26024 |
| Bottom-sheet-time-selected | 998:26025 |
| Card(섹션 전체) | 324:9692 |
| Card-item-receipt-list(상위 그룹) | 1983:62318 |
| Card-item-receipt-list(인스턴스 예시) | 1983:62173 |
| Card-item-recipt-error | 2098:60164 |
| Card-info(상위 그룹) | 2170:116883 |
| Card-info — S/Red | 1569:44491 |
| Card-info — M/Red | 336:11617 |
| Card-info — M/Blue | 2600:64964 |
| Uploader-file | 1518:60716 |
| Image-input(섹션 전체) | 354:19324 |
| Thumbnail-375*541 | 431:15767 |
| Image-viewer-343*140 | 1456:23785 |
| Image-viewer-375*591 | 431:15771 |
| Img-thumbnail | 1379:38004 |
| File-attachment | 2571:64604 |
| Modal(섹션 전체) | 614:12775 |
| Modal-button(상위) | 614:12076 |
| Modal-button — One-button/Normal | 614:12067 |
| Modal-button — Two-button/Normal | 614:11915 |
| Modal-button — Two-button/Wide | 614:12106 |
| Modal-button — Two-button/Strong | 614:12164 |
| Modal-list-item | 922:17832 |
| Modal-영수증상태 | 2729:73043 |
| Modal/권한(상위 컨테이너) | 2170:116782 |
| Modal/권한 — A | 856:27290 |
| Modal/권한 — B | 942:15890 |
| Modal/권한 — E | 942:15893 |
| Modal/권한 — D | 942:15892 |
