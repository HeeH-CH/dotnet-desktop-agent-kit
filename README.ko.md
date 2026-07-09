# dotnet-desktop-agent-kit

.NET 데스크톱 애플리케이션을 WinUI/WPF, MVVM, MVI 스타일 상태 흐름, Clean Architecture, Roslyn MCP 기반 코드 분석과 함께 개발하고 리팩토링하기 위한 실전형 에이전트 실행 킷입니다.

이 프로젝트의 목적은 AI 코딩 에이전트가 C# 데스크톱 애플리케이션을 다룰 때 더 안전한 아키텍처 판단을 내리고, 계획, 제한된 구현, 감사, 검증까지 이어서 수행하도록 돕는 것입니다.

[English README](README.md)

## 이 프로젝트가 집중하는 것

- WinUI/WPF View와 비즈니스 로직 분리
- ViewModel을 깨끗하고 상태 중심이며 테스트 가능하게 유지
- Intent -> UseCase -> Result -> ViewState 흐름 사용
- 데스크톱 애플리케이션에 맞는 Clean Architecture 경계 강제
- Microsoft Graph, 파일 시스템, 인증, 로컬 저장소, 외부 API를 Adapter 뒤로 격리
- Roslyn MCP 도구를 활용한 의미 기반 코드 탐색, 의존성 분석, 죽은 코드 탐지, 리팩토링 감사
- Codex, Claude, 규칙, 스킬, 워크플로, 전문 에이전트, MCP 도구 라우팅을 높은 수준에서 연결

## 왜 이 프로젝트가 필요한가

대부분의 .NET 에이전트 킷과 Clean Architecture 예제는 ASP.NET Core, Minimal API, EF Core, 백엔드 시스템에 최적화되어 있습니다. 하지만 데스크톱 애플리케이션에는 다른 압력이 있습니다.

- XAML과 code-behind에 애플리케이션 로직이 조용히 쌓입니다.
- ViewModel이 서비스 컨테이너처럼 비대해질 수 있습니다.
- UI 상태가 여러 mutable flag로 흩어지기 쉽습니다.
- 외부 SDK가 Presentation 계층으로 직접 새어 들어올 수 있습니다.
- 리팩토링은 매 단계마다 빌드 가능성과 UI 동작 보존을 신경 써야 합니다.

이 킷은 AI 코딩 에이전트에게 이런 데스크톱 특유의 문제를 명시적으로 다루는 기준을 제공하기 위해 만들어졌습니다. 단순한 스캐폴드가 아니라 실제 작업 순서와 검증 기준까지 다루는 실행 킷을 목표로 합니다.

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

## 실행 표면

이 킷은 서로 연결된 표면으로 사용합니다.

- `AGENTS.md`와 `.codex/AGENTS.md`는 Codex와 다른 코딩 에이전트의 운영 규칙을 정의합니다.
- `CLAUDE.md`는 Claude Code가 같은 지침을 읽기 위한 가벼운 진입점입니다.
- `rules/`는 데스크톱 코드에 항상 적용할 아키텍처 제약을 담습니다.
- `workflows/`는 리팩토링, 검증, 런타임 확인을 위한 반복 가능한 절차를 담습니다.
- `skills/`는 자주 반복되는 데스크톱 아키텍처 작업을 호출 가능한 작업 가이드로 정리합니다.
- `agents/`는 아키텍처, 리팩토링, 품질 감사, 빌드 수정을 맡는 전문 에이전트를 정의합니다.
- MCP와 도구 라우팅은 Roslyn MCP, Microsoft Learn/docs 도구, Context7, WinUI 플러그인 스킬, CommunityToolkit.Mvvm 스킬을 언제 우선할지 알려줍니다.

## 업그레이드 표면

현재 업그레이드는 저장소를 더 완성된 실행 킷으로 확장합니다. 계획되고 문서화되는 표면은 다음과 같습니다.

- 규칙: `rules/app-edge-boundaries.md`, `rules/result-taxonomy.md`, `rules/parallel-wave.md`, `rules/error-learning.md`
- 워크플로: `workflows/parallel-wave.md`, `workflows/runtime-smoke.md`, `workflows/verify-change.md`, `workflows/refactor-screen.md`
- 스킬: `skills/winui-app-edge-boundaries/`, `skills/mvi-reducer-store/`, `skills/desktop-result-taxonomy/`, `skills/desktop-composition-di/`
- 전문 에이전트: `agents/dotnet-desktop-architect.md`, `agents/mvvm-mvi-refactorer.md`, `agents/quality-auditor.md`, `agents/build-fix-agent.md`

이 표면들은 일반적인 .NET 데스크톱 프로젝트에 재사용 가능해야 합니다. 특정 제품의 tenant, workspace, 내부 URL, secret, 고객 세부사항은 넣지 않습니다.

## 사용 방법

사용 중인 AI 코딩 도구와 프로젝트에 맞는 파일을 복사해서 사용합니다.

- `AGENTS.md`를 프로젝트 수준의 메인 에이전트 가이드로 사용합니다.
- Codex CLI에는 `.codex/AGENTS.md`를 사용합니다.
- Claude Code에는 `CLAUDE.md`를 사용합니다.
- `rules/`, `skills/`, `agents/`, `workflows/` 중 필요한 파일을 프로젝트에 가져갑니다.
- 예시는 실제 프로젝트 구조에 맞게 수정합니다.
- 넓은 리팩토링은 관련 워크플로에서 시작하고, 필요한 규칙과 스킬을 읽은 뒤, 필요할 때만 전문 에이전트에 나누어 맡기고, 가장 좁지만 의미 있는 검증으로 마무리합니다.

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

현재는 초기 v0.1 실행 킷입니다. 지금의 목표는 규칙, 워크플로, 스킬, 전문 에이전트, MCP/도구 라우팅을 통해 데스크톱 에이전트 작업을 반복 가능하게 만드는 것입니다. 특히 다음 영역의 기여를 환영합니다.

- WinUI 3 패턴
- WPF 패턴
- CommunityToolkit.Mvvm 사용법
- MVI 스타일 데스크톱 상태 처리
- 데스크톱 앱을 위한 Clean Architecture
- Roslyn MCP 워크플로
- Microsoft Graph Adapter 경계

## 라이선스

MIT
