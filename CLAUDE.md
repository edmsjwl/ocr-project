# SBS OCR Project

## 1. Project Overview

SBS 사내 개인카드 영수증 처리 업무를 개선하기 위한 OCR 기반 앱/웹 프로젝트다.

사용자가 개인카드 영수증을 등록하면 OCR을 통해 정보를 인식하고, 웹에서 등록된 영수증을 조회·확인하여 전표 처리 업무로 연결한다.

이 프로젝트는 일반 소비자용 서비스가 아닌 **사내 업무용 시스템**이다.

UI를 설계하거나 구현할 때 시각적 장식보다 다음을 우선한다.

1. 업무 효율성
2. 정보 가독성
3. 상태의 명확한 구분
4. 오류 방지
5. 빠른 탐색과 처리
6. 기존 업무 흐름과의 일관성

---

## 2. Source of Truth

UI 작업 시 다음 우선순위를 따른다.

1. Figma 원본 디자인
2. `DESIGN.md`
3. 기존 프로젝트 컴포넌트 및 코드
4. 이 문서(`CLAUDE.md`)
5. 일반적인 UI 패턴

Figma와 `DESIGN.md`가 충돌하는 경우 **Figma를 기준으로 판단**한다.

확인할 수 없는 디자인 규칙이나 요구사항을 임의로 만들어내지 않는다.

---

## 3. Figma

Figma MCP가 연결되어 있다.

디자인 관련 작업을 수행할 때 필요한 경우 Figma MCP를 사용하여 실제 디자인을 확인한다.

특히 다음 정보는 추측하지 말고 Figma에서 확인한다.

- Variables
- Color tokens
- Typography
- Spacing
- Radius
- Layout
- Components
- Component properties
- Variants
- States

Figma의 기존 naming을 가능한 한 그대로 유지한다.

Figma에 존재하지 않는 token, component, variant 또는 state를 임의로 추가하지 않는다.

---

## 4. Design System

모든 UI 구현은 `DESIGN.md`를 따른다.

UI 작업 전 관련 디자인 시스템 정의가 있는지 먼저 확인한다.

### 기본 원칙

- 기존 design token을 우선 사용한다.
- 임의의 HEX color를 생성하지 않는다.
- 임의의 font size를 생성하지 않는다.
- 임의의 spacing 값을 생성하지 않는다.
- 임의의 radius 값을 생성하지 않는다.
- 기존 component를 우선 재사용한다.
- 동일한 UI 패턴을 새로운 component로 중복 구현하지 않는다.
- semantic token이 존재한다면 primitive token보다 semantic token을 우선 사용한다.

필요한 디자인 정의가 `DESIGN.md`에 없다면 임의로 추가하지 말고 Figma에서 먼저 확인한다.

---

## 5. Product Scope

현재 주요 범위는 **개인카드 영수증 처리**다.

### App

주요 흐름:

사용자 인증  
→ 영수증 촬영 / 앨범 / 파일 등록  
→ OCR 인식  
→ 인식 결과 확인 및 수정  
→ 영수증 등록

주요 정책:

- 개인카드 영수증을 대상으로 한다.
- 등록 개수 제한은 없다.
- 임시저장 기능은 제공하지 않는다.
- 프로그램 코드를 입력한다.
- 적요는 사용자가 직접 입력할 수 있다.

---

## 6. Web

웹은 등록된 개인카드 영수증을 조회하고 전표 처리 업무로 연결하기 위한 업무용 인터페이스다.

주요 기능:

- 개인카드 영수증 조회
- 기간 조회
- 프로그램 코드 검색
- 상태별 조회
- 영수증 상세 확인
- OCR 결과 확인
- 전표 생성 및 검증
- 중복 제출 확인

---

## 7. Receipt Status

현재 주요 상태는 다음과 같다.

- 전체
- 완료
- 처리중
- 작성중
- 중복

상태를 표현할 때는 `DESIGN.md`에 정의된 Status token과 Component를 사용한다.

색상만으로 상태를 전달하지 않는다.

가능하면 다음 요소를 함께 사용한다.

- Label
- Color
- Icon 또는 Shape

상태 색상을 일반적인 장식이나 카테고리 구분 목적으로 남용하지 않는다.

---

## 8. Card Types

카드 유형은 다음과 같이 구분한다.

- 개인카드
- 법인카드

카드 유형은 처리 상태가 아니라 **Category / Type 정보**다.

따라서 Status UI와 시각적 의미가 혼동되지 않도록 한다.

관련 UI가 디자인 시스템에 정의되어 있다면 해당 Component와 token을 그대로 사용한다.

---

## 9. Data Table

웹의 핵심 인터페이스 중 하나는 영수증 데이터 Table이다.

Table 설계 및 구현 시 다음을 우선한다.

### Priority

1. 사용자 식별 정보
2. 사용 일자
3. 가맹점
4. 금액
5. 사용 목적
6. 적요
7. 처리 상태

정보 밀도가 높은 업무용 화면이므로 불필요한 장식보다 **빠른 스캔과 비교**를 우선한다.

### Table Rules

- 숫자는 비교하기 쉽게 정렬한다.
- 금액의 표현 형식을 일관되게 유지한다.
- 날짜 형식을 일관되게 유지한다.
- Column alignment를 임의로 변경하지 않는다.
- Row Hover와 Selected 상태를 명확히 구분한다.
- Status Chip이 Disabled UI처럼 보이지 않도록 한다.
- 중요한 정보와 보조 정보의 시각적 위계를 구분한다.
- 불필요한 Column을 임의로 추가하지 않는다.

---

## 10. Filters

주요 조회 조건에는 다음이 포함될 수 있다.

- 상태
- 기간
- 프로그램 코드
- 가맹점
- 금액
- 사용 목적
- 중복 제출건

필터 UI는 현재 Figma에 정의된 구조를 우선한다.

필터가 많아져도 모든 요소를 동일한 시각적 강도로 표현하지 않는다.

필수 조회 조건과 보조 조건의 위계를 유지한다.

---

## 11. Duplicate Receipts

중복 제출은 사용자가 중요하게 확인해야 하는 예외 상황이다.

관련 UI에서는:

- 중복 여부를 명확하게 표시한다.
- 사용자가 중복 제출건만 필터링할 수 있도록 한다.
- 중복 건수를 표시할 경우 기존 Count / Badge 규칙을 따른다.
- 일반적인 처리 상태와 혼동되지 않도록 한다.

---

## 12. Forms

입력 화면에서는 사용자가 빠르게 업무를 완료할 수 있도록 한다.

### Rules

- Label은 명확하고 구체적으로 작성한다.
- 필수/선택 항목을 명확하게 구분한다.
- Placeholder를 Label 대신 사용하지 않는다.
- 오류 발생 시 문제와 해결 방법을 함께 제공한다.
- Disabled와 Read-only 상태를 구분한다.
- 동일한 데이터를 반복 입력하게 하지 않는다.
- 입력 형식이 정해져 있다면 가능한 경우 시스템이 이를 보조한다.

---

## 13. UX Writing

업무용 서비스에 적합한 간결하고 명확한 한국어를 사용한다.

### Prefer

- 무엇이 발생했는지
- 사용자가 무엇을 해야 하는지
- 처리 결과가 무엇인지

를 명확하게 전달한다.

### Avoid

- 불필요하게 친근한 표현
- 감탄사
- 장황한 설명
- 의미가 모호한 CTA
- 개발 용어를 그대로 노출하는 것
- 사용자가 이해할 필요가 없는 시스템 내부 용어

CTA는 가능한 한 행동을 직접 표현한다.

예:

- 확인
- 등록
- 수정
- 삭제
- 조회
- 전표 생성

---

## 14. Component Rules

새로운 UI를 구현하기 전에 기존 Component가 있는지 확인한다.

다음 순서를 따른다.

1. 기존 Component 재사용
2. 기존 Component의 Variant 활용
3. 기존 Component 조합
4. 필요한 경우에만 새로운 Component 생성

새 Component를 만들 때는 특정 화면의 모양이 아니라 **역할과 의미를 기준으로 naming**한다.

예:

- `Status Badge`
- `Category Badge`
- `Checkbox Filter`
- `Receipt Upload`
- `Empty State`

화면 이름이나 임시 텍스트를 Component 이름으로 사용하지 않는다.

---

## 15. Accessibility

업무용 시스템이더라도 기본적인 접근성을 유지한다.

- 텍스트와 배경 간 충분한 대비를 유지한다.
- 색상만으로 정보를 구분하지 않는다.
- Interactive element는 충분한 클릭 영역을 확보한다.
- Focus state를 제거하지 않는다.
- Disabled state와 Enabled state를 명확히 구분한다.
- Icon-only button에는 접근 가능한 이름을 제공한다.

---

## 16. Implementation Rules

UI를 구현할 때 다음 원칙을 따른다.

### Reuse First

새 코드를 작성하기 전에 기존:

- Components
- Styles
- Tokens
- Utilities
- Patterns

를 확인한다.

### Minimal Change

요청받지 않은 영역을 임의로 수정하지 않는다.

하나의 UI 변경을 위해 관련 없는 구조를 대규모로 리팩터링하지 않는다.

### No Guessing

디자인 값이 불분명한 경우:

1. `DESIGN.md` 확인
2. Figma 확인
3. 기존 구현 확인

순서로 조사한다.

그래도 확인되지 않으면 임의로 결정하지 않는다.

---

## 17. DESIGN.md Maintenance

Figma 디자인 시스템이 변경되면 `DESIGN.md`도 동기화되어야 한다.

`DESIGN.md`를 업데이트할 때:

- Figma를 source of truth로 사용한다.
- 기존 Figma naming을 유지한다.
- 실제 존재하지 않는 token을 생성하지 않는다.
- 실제 존재하지 않는 component variant를 생성하지 않는다.
- 추측한 값을 사실처럼 기록하지 않는다.

Figma와 `DESIGN.md`를 비교할 때 차이가 있다면 Figma 기준으로 수정한다.

---

## 18. Before UI Implementation

UI 관련 요청을 받으면 다음 순서로 작업한다.

1. 요청 범위를 파악한다.
2. 기존 코드와 Component를 확인한다.
3. `DESIGN.md`에서 관련 token과 component를 확인한다.
4. 필요한 경우 Figma MCP로 원본 디자인을 확인한다.
5. 기존 Component를 최대한 재사용한다.
6. 최소한의 변경으로 구현한다.
7. 구현 결과를 Figma와 비교한다.
8. 임의로 생성한 디자인 값이 없는지 확인한다.

---

## 19. Do

- Follow the existing Figma design system.
- Reuse existing components.
- Use semantic design tokens.
- Preserve established naming conventions.
- Keep information hierarchy clear.
- Optimize for work efficiency and readability.
- Keep UI behavior predictable and consistent.
- Verify uncertain design decisions against Figma.

## 20. Don't

- Do not invent design tokens.
- Do not introduce arbitrary colors.
- Do not introduce arbitrary spacing.
- Do not introduce arbitrary typography.
- Do not create unnecessary component variants.
- Do not redesign existing UI without being asked.
- Do not add decorative gradients or shadows without design-system support.
- Do not make every container a card.
- Do not overuse rounded or pill-shaped UI.
- Do not use status colors as decorative colors.
- Do not change established terminology without a clear reason.
- Do not assume missing product requirements.