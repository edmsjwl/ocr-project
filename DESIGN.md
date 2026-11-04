# SBS OCR Design System

## Purpose

SBS OCR 서비스의 디자인 시스템 구현 명세다. 개발자와 Claude Code가 동일한 디자인 규칙을 참조하기 위한 문서다.

## Documentation

실제 스펙(수치·토큰·상태)은 아래 문서에 있다. 이 문서는 목차 역할만 한다.

| 문서 | 내용 |
|---|---|
| [Foundation](docs/design-system/foundation.md) | Typography, Color(Atomic / Semantic Light / Semantic Dark), Elevation |
| [Icon](docs/design-system/icon.md) | Icon |
| [Layout](docs/design-system/layout.md) | Layout (Status-bar, Home-bar, Header, Tab, Navigation 등) |
| [Actions & Inputs](docs/design-system/actions-inputs.md) | Button, Textfield, Check-box, Date-picker |
| [Containers & Overlays](docs/design-system/containers-overlays.md) | Bottom-sheet, Card, Image-input, Modal |
| [Display & Feedback](docs/design-system/display-feedback.md) | Badge, Progress, Action-Area |

## Source of Truth

- **Design System Source:** [Figma Design Source](https://www.figma.com/design/ese9l01OJiDfirO8Q6XXIY/-SBS--OCR-프로젝트_디자인?node-id=39-2)
  - 디자인 시스템 문서의 작성·업데이트·검증 시 기준으로 사용

- **Design System Specification:** `docs/design-system/`
  - Figma를 기반으로 문서화된 디자인 시스템 상세 명세
  - 신규 UI 생성 시 디자인 기준으로 사용

- **AI Working Instructions:** [CLAUDE.md](CLAUDE.md)
  - Claude의 디자인 소스 참조 범위 및 작업 규칙 정의