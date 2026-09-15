# Assets

Figma MCP의 `download_assets` 도구로 실제 Figma 파일에서 직접 export한 원본 SVG 파일들이다. 임의로 새로 그리거나 대체한 파일은 없다 — 전부 Figma에서 받은 벡터 데이터 그대로다.

> 출처: `[SBS] OCR 프로젝트_디자인` (fileKey `ese9l01OJiDfirO8Q6XXIY`), 대부분 "🔵 디자인시스템" 페이지의 **Icon** 라이브러리(node 91:1111) 하위.
>
> **정리 작업 참고**: Figma가 내려주는 원본 export에는 아이콘과 무관한 캔버스 배경(`#F5F5F5`, `#FAFAFA`)과 일부 항목엔 보라색 점선 가이드 박스(`#9747FF`)가 함께 포함되어 있었다. 이 배경/가이드 요소만 제거했고, 실제 벡터 path는 전혀 손대지 않았다.

## 아이콘 (16/20/24/28px)

| 파일 | Figma node | 용도(DESIGN.md 근거) |
|---|---|---|
| icon-chevron-left-24.svg | 91:1100 | §5.4 Header(Back), phone-auth 뒤로가기 |
| icon-chevron-right-24.svg | 91:1098 | 참고용(미사용 화면 있으면 대비) |
| icon-chevron-up-24.svg | 91:1096 | 참고용 |
| icon-chevron-down-24.svg | 91:1102 | 참고용 |
| icon-home-24.svg | 91:1077 | 참고용(Header Home 타입은 실제로 로고를 씀, home 아이콘 자체는 미사용 확인) |
| icon-close-24.svg | 164:31155 | §5.4 Header(Close) |
| icon-search-24.svg | 91:1047 | §13.2 Image-viewer 확대 버튼(M, 24px) |
| icon-alert-circle-24.svg | 91:1106 | Icon 라이브러리 기본형(§12.2와는 다른 asset, 아래 img-alert-circle-24 참고) |
| img-alert-circle-24.svg | 2151:104111 | §12.2 Card-item-recipt-error 우측 아이콘 |
| icon-check-circle-24.svg | 1140:22510 | 참고용 |
| icon-check-circle-solid-24.svg | 1140:22511 | 참고용 |
| icon-calendar-24.svg | 207:10524 | 참고용 |
| icon-chevron-down-20.svg | 192:6951 | §7.3 Program-select(닫힘 상태) — ⚠️ 원본 export가 배경만 있고 실제 path가 비어 있어서, 개별 벡터 레이어(svgAssets)에서 다시 받았다. viewBox가 20×20이 아니라 실제 도형 bbox(11.8×21.8)로 타이트하게 잡혀 있음 — 사용 시 컨테이너 크기만 맞추면 정상 동작. |
| icon-chevron-up-20.svg | 192:6954 | §7.3 Program-select(열림 상태) — 위와 동일한 이유로 개별 벡터 레이어 사용, viewBox 11.8×21.8 |
| icon-chevron-left-20.svg | 192:6952 | 참고용 |
| icon-chevron-right-20.svg | 192:6953 | §8.3 Check-box/item, 홈 화면 "전체보기" |
| icon-check-20.svg | 192:6950 | 참고용 |
| icon-close-20.svg | 1358:33757 | 참고용 |
| icon-close-circle-20.svg | 192:6956 | 참고용 |
| icon-close-circle-solid-20.svg | 192:6957 | §7.1 Textfield / phone-auth 입력값 지우기 버튼 |
| icon-check-circle-20.svg | 148:10545 | 참고용 |
| icon-check-circle-solid-20.svg | 149:8919 | §7.1 Textfield(Positive), phone-auth 인증완료 체크 |
| icon-alert-circle-20.svg | 192:6959 | 참고용 |
| icon-alert-circle-solid-20.svg | 192:6960 | §7.1 Textfield(Negative/에러) |
| icon-calendar-20.svg | 207:10533 | §9.1 Date-picker/Selectbox |
| icon-search-20.svg | 1140:22262 | §13.2 Image-viewer 확대 버튼(S, 20px) |
| icon-alert-circle-16.svg | 192:6766 | §12.3 Card-Warning |
| icon-calendar-16.svg | 1774:49893 | 참고용 |
| icon-functional-check.svg | 336:14252 | §8.1 Check-box/24(체크됨) |

## 카드 종류 아이콘 (24px)

| 파일 | Figma node | 용도 |
|---|---|---|
| card-personal-light-24.svg | 2203:64252 | §11.2 / §12.1 개인카드 배지 |
| card-coporate-light-24.svg | 2203:64253 | §11.2 / §12.1 법인카드 배지 |
| card-personal-dark-24.svg | 2240:53797 | 다크모드용(현재 미사용, 참고 보관) |
| card-coporate-dark-24.svg | 2240:53796 | 다크모드용(현재 미사용, 참고 보관) |

## 메인 홈 화면 전용

| 파일 | Figma node | 용도 |
|---|---|---|
| img-gallery-48-light.svg | 2304:81461 | 메인 홈 "앨범에서 선택" 카드 아이콘 |
| img-file-48-light.svg | 2304:81472 | 메인 홈 "파일에서 선택" 카드 아이콘 |
| nav-home-activated-24.svg | 2240:69996 | 하단 네비게이션 "홈" 탭(선택됨) |
| nav-home-disabled-24.svg | 2240:69998 | 하단 네비게이션 "홈" 탭(선택안됨) |
| nav-list-activated-24.svg | 2240:69997 | 하단 네비게이션 "영수증 내역" 탭(선택됨) |
| nav-list-disabled-24.svg | 2240:69999 | 하단 네비게이션 "영수증 내역" 탭(선택안됨) |
| logo-scan-mark.svg | 2203:48107 | 헤더 로고 마크("스캔" 부분) |
| logo-wise-wordmark.svg | 2150:103469 | 헤더 로고 워드마크("WiSE" 부분) |

## ⚠️ 직접 export하지 못해 Figma에서 수동으로 받아야 하는 것들

아래는 이번 조사에서 명확한 canonical node ID를 찾지 못했다 — 화면 인스턴스 안에서 조합된 형태로만 확인되어(instance override ID만 존재), `download_assets`가 요구하는 단일 node ID로 특정할 수 없었다. **임의로 대체 SVG를 만들지 않았다** — 아래 목록을 Figma에서 직접 선택해 "Export"로 받아야 한다.

- **상태바 아이콘 3종** — 셀룰러 신호 / Wi-Fi / 배터리 (`Status-bar` 컴포넌트, node 161:30744 내부). 모든 화면에서 인스턴스 오버라이드로만 나타나 개별 base 컴포넌트를 특정하지 못했다.
- **Tab-item 안읽음 점 표시 인디케이터** ("Frame 1707483812" 에셋, Tab-item·Card-Item/Receipt에서 공용으로 쓰임) — 마찬가지로 인스턴스 참조만 확인됨.
- **Content-Badge(카드 종류) 아이콘의 "48px 배지 내부" 버전과 "Round style" 버전** — 이번엔 24px "Square 배지 안에 들어가는" 버전만 받았다. Round(pill) 배지에 쓰이는 별도 asset이 있다면 추가 확인 필요.
