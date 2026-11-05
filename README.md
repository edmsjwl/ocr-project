
# SBS OCR Design System

SBS 영수증전자화 서비스의 디자인 시스템 및 UI 구현 명세를 관리하는 저장소입니다.

Figma 디자인 시스템을 Markdown으로 문서화하여 개발자와 AI 코딩 도구가 일관된 기준으로 UI를 구현할 수 있도록 지원합니다.

## Overview

이 저장소는 디자인 토큰, 컴포넌트, 레이아웃 명세와 AI 기반 UI 설계 지침을 제공합니다.

- **Design Specification** — UI 구현을 위한 디자인 시스템 상세 명세
- **AI Instructions** — Claude Code 작업 규칙 및 UI 설계 판단 기준
- **Design Source** — [Figma 디자인 원본](https://www.figma.com/design/ese9l01OJiDfirO8Q6XXIY/-SBS--OCR-프로젝트_디자인?node-id=39-2)

## Repository Structure

| 파일 / 폴더 | 역할 |
|---|---|
| `README.md` | 프로젝트 소개 및 문서 사용 안내 |
| `DESIGN.md` | 디자인 시스템 명세 목차 및 참조 가이드 |
| `CLAUDE.md` | Claude Code 작업 규칙 및 디자인 소스 참조 기준 |
| `Skills.md` | 정보 구조, 시각적 위계, 레이아웃 등 UI 설계 지침 |
| `docs/design-system/` | 디자인 토큰·컴포넌트·레이아웃 상세 명세 |
| `assets/` | 이미지·아이콘 등 디자인 리소스 |
| `test/` | UI 생성 및 디자인 시스템 검증용 프로토타입 |

## Getting Started

### UI 구현

1. [DESIGN.md](DESIGN.md)에서 디자인 시스템 구조를 확인합니다.
2. [docs/design-system/](docs/design-system/)에서 필요한 토큰과 컴포넌트 명세를 참조합니다.
3. 정의된 Variant, State, Layout 규칙에 따라 UI를 구현합니다.

### AI 기반 UI 구현

1. [CLAUDE.md](CLAUDE.md)의 작업 규칙을 따릅니다.
2. `DESIGN.md`와 `docs/design-system/`의 명세를 기준으로 UI를 구현합니다.
3. [Skills.md](Skills.md)의 정보 위계 및 레이아웃 설계 지침을 적용합니다.
4. 신규 UI 생성 시 Figma 화면을 참조하지 않고 문서화된 명세만 사용합니다.

> `Skills.md`는 현재 일반 Markdown 지침이며 Claude Code Skill로 등록되어 있지 않습니다.

## Design Specification

| 문서 | 내용 |
|---|---|
| [Foundation](docs/design-system/foundation.md) | Color, Typography, Elevation |
| [Icon](docs/design-system/icon.md) | Icon |
| [Layout](docs/design-system/layout.md) | Grid, Status Bar, Header, Navigation |
| [Actions & Inputs](docs/design-system/actions-inputs.md) | Button, Textfield, Check-box, Date-picker |
| [Containers & Overlays](docs/design-system/containers-overlays.md) | Bottom-sheet, Card, Image-input, Modal |
| [Display & Feedback](docs/design-system/display-feedback.md) | Badge, Progress, Action-Area |

## Source of Truth

- **Figma:** 디자인 시스템 원본 및 문서 갱신 기준
- **docs/design-system/:** UI 구현을 위한 상세 명세
- **CLAUDE.md / Skills.md:** AI 작업 규칙 및 UI 설계 기준

디자인 시스템 명세가 누락되거나 불명확한 경우 임의의 값을 생성하지 않고 확인이 필요한 항목으로 기록합니다.
