# dotnet-desktop-agent-kit 업그레이드 계획

작성일: 2026-07-09  
기준 경험: InnoBoard WinUI 3 앱의 MVVM, MVI, Clean Architecture, Microsoft 365/Graph 경계 정리 작업  
목표: 특정 앱의 세부 구현 지식을 제거하고, 재사용 가능한 .NET 데스크톱 에이전트 킷 규칙과 워크플로로 일반화한다.

## 1. 방향

이 업그레이드는 새 아키텍처 철학을 추가하는 작업이 아니다. 기존 키트가 가진 WinUI/WPF, MVVM, MVI 스타일 상태 흐름, Clean Architecture, Roslyn MCP 방향을 유지하되, 실제 앱 리팩터링에서 검증된 실행 규율을 보강한다.

핵심 변경 방향은 다음과 같다.

- 선언형 원칙보다 작업 순서, 감사 기준, 검증 기준을 강화한다.
- WinUI 3와 Windows App SDK에서 반복적으로 문제가 되는 App-edge 권한을 명시한다.
- ViewModel, reducer, store, use case, adapter의 책임을 더 구체적으로 나눈다.
- `bool`, raw exception, user-facing string 중심 결과 대신 typed result taxonomy를 권장한다.
- Codex, winui plugin, CommunityToolkit.Mvvm skills, Microsoft Learn MCP, Roslyn MCP, Context7 MCP 라우팅을 명시한다.
- 넓은 리팩터링은 plan -> parallel discovery/audit -> scoped implementation -> re-audit -> verification 흐름으로 진행한다.

## 2. 적용 범위

이번 업그레이드는 다음 파일군을 대상으로 한다.

- `AGENTS.md`: 전체 운영 규칙과 도구 라우팅 보강
- `.codex/AGENTS.md`: Codex에서 사용하는 스킬, 플러그인, MCP 라우팅 보강
- `README.md`, `README.ko.md`: 사용 방법과 포함된 규칙/스킬 소개 갱신
- `rules/`: 항상 적용할 경계 규칙 추가
- `workflows/`: 병렬 wave, 런타임 smoke, 검증 흐름 추가
- `skills/`: 반복 가능한 작업 단위 스킬 추가
- `agents/`: specialist agent가 새 규칙을 읽도록 보강
- `templates/AGENTS.winui.md`: 실제 WinUI 3 프로젝트에 붙여 넣을 수 있는 실전 템플릿으로 확장

## 3. 일반화할 InnoBoard 경험

다음 내용은 특정 앱 이름, tenant, Microsoft 365 workspace 세부사항 없이 일반화한다.

### 3.1 App-edge 권한

WinUI 3 앱에서 다음 권한은 App/View host boundary에 남긴다.

- `Window`, `XamlRoot`, `AppWindow`, `DispatcherQueue`, raw HWND, DWM/User32 interop
- dialog, flyout, focus, pointer capture, keyboard routing, tray, storyboard, timer
- clipboard, file picker, process launch, local OS integration
- MSAL/WAM parent-window routing and interactive authentication surfaces

ViewModel, Application, Domain은 위 타입이나 권한을 직접 소유하지 않는다.

### 3.2 MVI purity

MVI reducer/store 경계는 다음 규칙을 따른다.

- reducer는 기존 state와 intent로 다음 state만 만든다.
- store는 dispatch와 publication만 담당한다.
- reducer/store는 async, file I/O, HTTP, Graph, database, WinUI control mutation을 수행하지 않는다.
- async side effect는 controller/effect/use case boundary에서 실행하고, 결과를 intent/result로 되돌린다.

### 3.3 Result taxonomy

사용자에게 보이는 action result는 단순 `bool`, raw `Exception`, `exception.Message`로 표현하지 않는다.

권장 result는 다음 정보를 가진다.

- action kind
- status or severity
- machine-readable failure reason
- retry/reload hint
- optional diagnostics log reference
- optional stale/cancelled/partial-success classification

Infrastructure는 외부 SDK 예외를 application-owned failure reason으로 변환한다. Presentation 또는 App-edge presenter가 failure reason을 사용자 표시 문구로 매핑한다.

### 3.4 Composition and DI

ViewModel과 use case는 생성자 주입을 기본으로 한다.

- service locator는 마지막 수단으로만 사용한다.
- `BuildServiceProvider()`는 앱 시작 시 한 번만 실행한다.
- Window-scoped dependency는 명시적인 scope, provider, factory로 드러낸다.
- Graph/auth/window handle처럼 App-edge가 필요한 dependency는 Application/Domain으로 밀어 넣지 않는다.
- static builder는 compatibility facade나 App-edge composition helper 수준으로 제한한다.

### 3.5 Error learning

반복 가능성이 있는 오류를 고쳤다면 agent-facing note를 남긴다.

기록 형식은 다음을 포함한다.

- symptom
- root cause
- fix
- verification command
- remaining risk, if any

프로젝트마다 위치는 다를 수 있지만, 권장 위치는 `.devs/` 또는 agent-facing docs 폴더다.

## 4. 도구와 스킬 라우팅

에이전트는 다음 라우팅을 기본으로 사용한다.

- WinUI 3, Windows App SDK, XAML, packaging, UI testing: `winui` plugin skills
- CommunityToolkit.Mvvm ViewModel, `[ObservableProperty]`, `[RelayCommand]`: `mvvm-toolkit`
- CommunityToolkit.Mvvm DI, `Microsoft.Extensions.DependencyInjection`: `mvvm-toolkit-di`
- CommunityToolkit.Mvvm Messenger: `mvvm-toolkit-messenger`
- Microsoft Learn, Windows App SDK, MSAL, Microsoft Graph, .NET SDK docs: `microsoft-docs`, `microsoft-code-reference`, `microsoft-learn` MCP
- C# semantic analysis, symbol/reference navigation, diagnostics, safe refactoring impact checks: `roslyn` MCP
- External library or API documentation: Context7 MCP

이 라우팅은 도구가 있을 때 우선순위다. 도구가 없으면 공식 문서, 기존 프로젝트 패턴, targeted text search 순서로 대체한다.

## 5. 새 파일과 변경 묶음

### Bundle A. 운영 규칙과 Codex 라우팅

소유 파일:

- `AGENTS.md`
- `.codex/AGENTS.md`
- `templates/AGENTS.winui.md`

목표:

- 설치된 스킬과 플러그인을 언제 사용하는지 명시한다.
- WinUI 3 프로젝트에서 WPF guidance를 기본값으로 오해하지 않도록 한다.
- App-edge 권한과 result taxonomy를 project-level rule로 추가한다.

### Bundle B. Rules and workflows

소유 파일:

- `rules/app-edge-boundaries.md`
- `rules/result-taxonomy.md`
- `rules/parallel-wave.md`
- `rules/error-learning.md`
- `workflows/parallel-wave.md`
- `workflows/runtime-smoke.md`
- `workflows/verify-change.md`
- `workflows/refactor-screen.md`

목표:

- 반복 가능한 리팩터링 절차를 문서화한다.
- 병렬 구현과 병렬 감사 기준을 명확히 한다.
- runtime smoke는 자동화 검증이 아니라 수동/interactive 검증 기준으로 둔다.

### Bundle C. Skills and agents

소유 파일:

- `skills/winui-app-edge-boundaries/SKILL.md`
- `skills/mvi-reducer-store/SKILL.md`
- `skills/desktop-result-taxonomy/SKILL.md`
- `skills/desktop-composition-di/SKILL.md`
- `agents/dotnet-desktop-architect.md`
- `agents/mvvm-mvi-refactorer.md`
- `agents/quality-auditor.md`
- `agents/build-fix-agent.md`

목표:

- 새 규칙을 실제 작업 스킬로 호출할 수 있게 한다.
- specialist agent가 어떤 rule/skill을 먼저 읽어야 하는지 갱신한다.

### Bundle D. README and contribution surface

소유 파일:

- `README.md`
- `README.ko.md`
- `CONTRIBUTING.md`

목표:
