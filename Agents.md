# AGENTS.md

This repository is an Expo app built with TypeScript.

Codex should use this file as the default working agreement for all changes in this repo.

## Product and stack

- Framework: Expo
- Language: TypeScript
- Routing: Expo Router
- Server state: TanStack Query
- Client/UI state: Zustand
- Forms: React Hook Form
- Secure local secrets: expo-secure-store
- Optional local persistence: expo-sqlite

## Primary goals

When making changes, optimize for:

1. Correctness
2. Small, focused diffs
3. Readability and maintainability
4. Mobile-first UX
5. Type safety
6. Reuse of existing patterns before introducing new abstractions

## Non-goals

Unless explicitly requested, do not:

- rewrite large parts of the app
- replace core libraries
- introduce a new state management library
- add heavy dependencies for small problems
- create overly generic abstractions too early
- modify native iOS/Android project files if the issue can be solved in Expo/JS/TS land

## How to work

- First inspect existing patterns in the repository before adding new ones.
- Prefer editing existing files over creating new ones unless a new file is clearly warranted.
- Keep changes minimal and local to the task.
- Preserve public APIs unless the task explicitly requires changing them.
- If a requirement is ambiguous, choose the simplest solution that matches current project conventions.
- If you must make a tradeoff, document it briefly in your final summary.

## Project structure expectations

Use these conventions unless the repository already uses a different pattern:

- `app/`: Expo Router routes and layouts
- `components/`: reusable presentational components
- `features/`: feature-focused UI, hooks, and business logic
- `store/`: Zustand stores
- `lib/`: shared utilities, API clients, constants, helpers
- `hooks/`: reusable React hooks
- `types/`: shared TypeScript types
- `assets/`: static assets

If the repo already has a different structure, follow the existing structure instead of forcing this one.

## Routing rules

- Use Expo Router conventions.
- Keep route files focused on screen composition.
- Put reusable logic outside route files when possible.
- Do not move routes or rename route segments unless required.
- Preserve deep-link compatibility when changing navigation structure.

## Data fetching rules

- Use TanStack Query for server data, caching, invalidation, and async request state.
- Do not store server-fetched collections in Zustand unless there is a clear reason.
- Query keys should be stable, specific, and colocated with the related feature when practical.
- After mutations, prefer targeted invalidation or cache updates over broad refetching.
- Handle loading, error, and empty states explicitly in screens that fetch data.

## Zustand rules

Use Zustand only for client-side state such as:

- UI toggles
- filters
- onboarding/session flags
- ephemeral app state not owned by the server

Do not use Zustand as a replacement for TanStack Query.

## Forms and validation

- Use React Hook Form for user input flows with meaningful validation or submission state.
- Keep validation close to the form.
- Show clear error messages.
- Avoid overly complex controlled-input wiring when a simpler pattern works.

## Styling rules

- Follow the styling approach already present in the repo.
- If the repo uses NativeWind, continue using NativeWind.
- If the repo uses `StyleSheet`, continue using `StyleSheet`.
- Do not mix multiple styling systems in the same feature without a good reason.
- Prefer simple, predictable layouts over deeply nested wrappers.
- Build mobile-first UI and consider small screens by default.

## Platform rules

- Preserve cross-platform compatibility for iOS, Android, and web where the existing codebase supports it.
- Avoid platform-specific code unless necessary.
- If platform-specific behavior is required, isolate it clearly.
- Do not assume browser-only APIs are available in native environments.
- Do not assume native-only APIs are available on web.

## Secure storage and persistence

- Store tokens or secrets in `expo-secure-store`, not plain AsyncStorage.
- If local structured persistence is needed, prefer the project’s existing persistence solution.
- If adding persistence, keep serialization formats explicit and stable.

## TypeScript rules

- Prefer explicit types at module boundaries.
- Avoid `any`. Use `unknown` when needed and narrow properly.
- Reuse existing domain types before introducing new duplicate types.
- Keep function signatures narrow and honest.
- Prefer discriminated unions or precise interfaces over loose object shapes.

## Component rules

- Keep components small and composable.
- Separate presentational concerns from data-fetching concerns when reasonable.
- Avoid giant screen files that mix routing, fetching, transformations, forms, and UI all together.
- Extract repeated UI only after repetition is real, not hypothetical.

## Error handling

- Fail gracefully in user-facing flows.
- Surface actionable messages for expected errors.
- Do not swallow errors silently.
- Keep logging useful but not noisy.
- Preserve existing error handling patterns if present.

## Accessibility and UX

- Use clear labels for interactive elements.
- Respect loading and disabled states during async actions.
- Prevent duplicate submissions.
- Prefer obvious interactions over clever ones.
- Maintain reasonable accessibility defaults for React Native components.

## Performance

- Avoid unnecessary re-renders in large lists or complex screens.
- Memoize only when it solves a real problem.
- Prefer FlatList/SectionList for non-trivial lists.
- Do not prematurely optimize at the cost of readability.

## Dependency policy

Before adding a dependency:

1. Check whether Expo, React Native, or an existing library already solves the problem.
2. Prefer small, well-maintained libraries with a clear need.
3. Avoid adding overlapping libraries.

If you add a dependency, explain why it is needed in your final summary.

## File edit policy

Do not make unrelated edits.

Avoid:

- mass reformatting
- renaming unrelated files
- moving files without need
- changing import order project-wide
- broad “cleanup” unrelated to the task

## Testing and verification

Before finishing, run the smallest relevant checks you can.

Prefer, in order:

1. targeted typecheck
2. targeted test
3. targeted lint
4. app-level verification only if needed

If the repo exposes scripts, use them. Typical commands may include:

- `npm run lint`
- `npm run typecheck`
- `npm run test`
- `npx expo start --web`

Use the package manager already used by the repo. Do not switch package managers.

## Definition of done

A task is done when:

- the requested change is implemented
- the diff is minimal and consistent with local patterns
- TypeScript remains sound
- relevant checks were run when feasible
- the final summary explains what changed, any caveats, and any follow-up work if needed

## Final response format

When reporting back after coding work, include:

1. what changed
2. which files were touched
3. what checks were run
4. any caveats or assumptions

Keep the summary concise and factual.

## When unsure

When uncertain, prefer:

- existing repo conventions over new patterns
- simple solutions over clever abstractions
- narrowly scoped edits over broad refactors
- explicit code over implicit magic
