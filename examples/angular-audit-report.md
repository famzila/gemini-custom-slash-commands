# Angular Audit Report (MCP-aligned + Modern Syntax Compliance)

##  Code Quality
- `NgClass` used in `src/app/shared/components/stepper.html` (prefer `[class.*]` binding).
- `CommonModule` imported in `src/app/features/breathing/breathing.ts` (import only required standalone features).
- `CommonModule` imported in `src/app/features/reflection/reflection.ts` (import only required standalone features).
- `CommonModule` imported in `src/app/features/timer/timer.ts` (import only required standalone features).
- `CommonModule` imported in `src/app/shared/components/quote.ts` (import only required standalone features).
- `CommonModule` imported in `src/app/shared/components/stepper.ts` (import only required standalone features).
- `standalone: true` declared in `src/app/app.ts` — redundant in Angular 20.
- `standalone: true` declared in `src/app/features/breathing/breathing.ts` — redundant in Angular 20.
- `standalone: true` declared in `src/app/features/checklist/checklist.ts` — redundant in Angular 20.
- `standalone: true` declared in `src/app/features/reflection/reflection.ts` — redundant in Angular 20.
- `standalone: true` declared in `src/app/features/sounds/sounds.ts` — redundant in Angular 20.
- `standalone: true` declared in `src/app/features/timer/timer.ts` — redundant in Angular 20.
- `standalone: true` declared in `src/app/features/welcome/welcome.ts` — redundant in Angular 20.
- `standalone: true` declared in `src/app/shared/components/layout.ts` — redundant in Angular 20.
- `standalone: true` declared in `src/app/shared/components/navigation.ts` — redundant in Angular 20.
- `standalone: true` declared in `src/app/shared/components/quote.ts` — redundant in Angular 20.
- `standalone: true` declared in `src/app/shared/components/stepper.ts` — redundant in Angular 20.

##  Performance & Best Practices
(MCP-based findings, unchanged)
- All components are standalone.
- Signals are used for state management.
- Lazy loading is implemented for all feature routes.
- `ChangeDetectionStrategy.OnPush` is used in `sounds.ts` and `timer.ts`. It should be applied to all components.
- `input()` and `output()` functions are used instead of decorators.
- Native control flow (`@if`, `@for`, `@switch`) is used.

##  Best Practices & Modern Angular
- Legacy structural directives have been successfully replaced with modern control-flow blocks.
- Leverage control-flow blocks, signals, OnPush, etc.
- Remove redundant `standalone: true` to reduce boilerplate.

##  Actionable Improvement Plan
- [ ] **High** — Remove `NgClass` and replace with `[class.*]` bindings in `src/app/shared/components/stepper.html`.
- [ ] **High** — Remove `CommonModule` imports from standalone components; import only needed features.
- [ ] **Medium** — Remove redundant `standalone: true` from all components (Angular 20 default).
- [ ] **Medium** — Apply `ChangeDetectionStrategy.OnPush` to all components to improve performance.
- [ ] **Low** — No `NgStyle` usages found.
