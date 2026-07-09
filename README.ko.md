# dotnet-desktop-agent-kit

.NET 데스크톱 애플리케이션을 WinUI/WPF, MVVM, MVI 스타일 상태 흐름, Clean Architecture, Roslyn MCP 기반 코드 분석과 함께 개발하고 리팩토링하기 위한 실전형 에이전트 스킬 킷입니다.

이 프로젝트의 목적은 AI 코딩 에이전트가 C# 데스크톱 애플리케이션을 다룰 때 더 안전한 아키텍처 판단을 내리도록 돕는 것입니다.

[English README](README.md)

## 이 프로젝트가 집중하는 것

- WinUI/WPF View와 비즈니스 로직 분리
- ViewModel을 깨끗하고 상태 중심이며 테스트 가능하게 유지
- Intent -> UseCase -> Result -> ViewState 흐름 사용
- 데스크톱 애플리케이션에 맞는 Clean Architecture 경계 강제
- Microsoft Graph, 파일 시스템, 인증, 로컬 저장소, 외부 API를 Adapter 뒤로 격리
- Roslyn MCP 도구를 활용한 의미 기반 코드 탐색, 의존성 분석, 죽은 코드 탐지, 리팩토링 감사

## 왜 이 프로젝트가 필요한가

대부분의 .NET 에이전트 킷과 Clean Architecture 예제는 ASP.NET Core, Minimal API, EF Core, 백엔드 시스템에 최적화되어 있습니다. 하지만 데스크톱 애플리케이션에는 다른 압력이 있습니다.

- XAML과 code-behind에 애플리케이션 로직이 조용히 쌓입니다.
- ViewModel이 서비스 컨테이너처럼 비대해질 수 있습니다.
- UI 상태가 여러 mutable flag로 흩어지기 쉽습니다.
- 외부 SDK가 Presentation 계층으로 직접 새어 들어올 수 있습니다.
- 리팩토링은 매 단계마다 빌드 가능성과 UI 동작 보존을 신경 써야 합니다.

이 킷은 AI 코딩 에이전트에게 이런 데스크톱 특유의 문제를 명시적으로 다루는 기준을 제공하기 위해 만들어졌습니다.

## 권장 애플리케이션 아키텍처

```text
App / Presentation
  WinUI/WPF Views, XAML, ViewModels, ViewState, Commands, Intent dispatching

Application
  UseCases, Ports, DTOs, orchestration, validation, application-level Result models

Domain
  Pure business concepts, value objects, domain rules, framework-independent models

Infrastructure
  Microsoft Graph, authentication, local storage, file access, external APIs, adapter implementations
```

의존성 방향은 안쪽을 향해야 합니다.

```text
App -> Application -> Domain
Infrastructure -> Application / Domain
Domain -> no external dependencies
```

## MVI 스타일 데스크톱 흐름

```text
View
 -> Command / Intent
 -> ViewModel
 -> UseCase
 -> Port
 -> Infrastructure Adapter
 -> Result
 -> Reducer / State update
 -> ViewState
 -> View
```

## 저장소 구조

```text
AGENTS.md                     # 메인 에이전트 운영 가이드
CLAUDE.md                     # Claude Code용 선택적 진입점
.codex/AGENTS.md              # Codex CLI 친화적 진입점
rules/                        # 항상 적용되는 아키텍처 규칙
skills/                       # 재사용 가능한 작업 스킬
agents/                       # 전문 서브에이전트 정의
workflows/                    # 단계별 개발 워크플로
templates/                    # 복사해서 쓸 수 있는 프로젝트 템플릿
docs/adr/                     # 아키텍처 결정 기록
```

## 사용 방법

사용 중인 AI 코딩 도구와 프로젝트에 맞는 파일을 복사해서 사용합니다.

- `AGENTS.md`를 프로젝트 수준의 메인 에이전트 가이드로 사용합니다.
- Codex CLI에는 `.codex/AGENTS.md`를 사용합니다.
- Claude Code에는 `CLAUDE.md`를 사용합니다.
- `rules/`, `skills/`, `agents/`, `workflows/` 중 필요한 파일을 프로젝트에 가져갑니다.
- 예시는 실제 프로젝트 구조에 맞게 수정합니다.

## Roslyn MCP 권장 사항

C# 프로젝트에서는 가능한 경우 단순 텍스트 검색보다 의미 기반 분석을 우선합니다. 유용한 Roslyn MCP 작업은 다음과 같습니다.

- 심볼과 참조 찾기
- port/interface 구현체 찾기
- 프로젝트 의존성 그래프 확인
- 순환 의존성 탐지
- 진단 정보 확인
- 죽은 코드 탐지
- public API surface 확인

## 현재 상태

현재는 초기 v0.1 스캐폴드입니다. 지금의 목표는 구조와 용어를 잡는 것입니다. 특히 다음 영역의 기여를 환영합니다.

- WinUI 3 패턴
- WPF 패턴
- CommunityToolkit.Mvvm 사용법
- MVI 스타일 데스크톱 상태 처리
- 데스크톱 앱을 위한 Clean Architecture
- Roslyn MCP 워크플로
- Microsoft Graph Adapter 경계

## 라이선스

MIT
