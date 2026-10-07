# OCR Design System

OCR 앱·웹의 디자인 시스템과 개발 명세를 관리하는 저장소입니다.

## Documents

- DESIGN.md — 구현 명세 목차·표기 규칙 (실제 스펙은 docs/design-system/ 참고)
- docs/design-system/01-foundation.md — Color · Typography · Elevation
- docs/design-system/02-icon.md — Icon
- docs/design-system/03-layout.md — Layout(Grid·Status-bar·Header·Navigation 등)
- docs/design-system/04-actions-inputs.md — Button · Textfield · Check-box · Date-picker
- docs/design-system/05-containers-overlays.md — Bottom-sheet · Card · Image-input · Modal
- docs/design-system/06-display-feedback.md — Badge · Progress · Action-Area
- CLAUDE.md — Claude Code 작업 규칙

## Screens (Prototypes)

docs/design-system/ 스펙을 근거로 만든 정적 HTML 프로토타입입니다. 전부 iOS 375px 프레임 기준입니다.

- screen-home.html — 메인 홈
- screen-home-v2.html — 메인 홈(재구현판) — screen-home.html과 내용은 동일하나, Figma를 다시 참조하지 않고 docs/design-system/만 근거로 별도로 새로 작성
- screen-mypage.html — 마이페이지
- screen-notifications.html — 알림 내역
- screen-phone-auth.html — 휴대폰 인증(상태 전환 가능한 인터랙티브 프로토타입)
- screen-receipt-history.html — 영수증 내역(월별 조회·상태 필터·처리 상태 안내 모달)
- screen-receipt-detail.html — 영수증 상세내역(반려·대기 상태일 때 삭제·수정하기 CTA 노출)
- screen-receipt-register-fail.html — 영수증 등록 실패
- design-system-test.html — 디자인 시스템 컴포넌트 테스트 페이지

## Source of Truth

Figma → 디자인 원본
DESIGN.md → 개발 구현 명세
GitHub → 문서 변경 이력