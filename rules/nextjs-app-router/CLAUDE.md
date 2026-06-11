# Next.js App Router (TypeScript)

## File structure

- All routes live under `app/`
- Server Components by default; mark Client Components with `"use client"` at the top of the file
- Page files: `app/route/page.tsx`
- Layout files: `app/route/layout.tsx`
- Loading states: `app/route/loading.tsx`
- Error boundaries: `app/route/error.tsx` (must be Client Component)
- API routes: `app/api/route/route.ts` with named exports for `GET`, `POST`, etc.
- Shared components: `components/`
- Utilities: `lib/`
- Types: colocate with usage, or `types/` for cross-cutting

## Components

- **Default to Server Components.** Only use `"use client"` when you need: state, refs, browser APIs, event handlers
- Server Components can be `async` and fetch data directly. Don't add `useEffect` to fetch data on the server side
- Client Components cannot import Server Components as children, but can receive them as props (`children`)
- Never import server-only code (database clients, secrets) into a Client Component

## Data fetching

- Fetch in Server Components, not via `useEffect`
- Use `fetch()` directly; Next.js extends it with caching options
- For mutations, use Server Actions (`"use server"`) over API routes when possible
- Wrap mutations in `try/catch` and return typed error objects, not throw

## Styling

- Tailwind for utility-first; use `clsx` or `cn` helper for conditional classes
- Don't use CSS Modules unless specifically requested
- Don't use inline `style={{}}` objects unless the value is dynamic

## TypeScript

- `strict: true` in tsconfig (enable all strict flags)
- No `any`. Use `unknown` and narrow
- Prefer `type` for unions, `interface` for object shapes
- Component props: `interface ComponentNameProps`
- Avoid default exports for components (named exports help with refactoring)

## Imports

- Absolute imports via `@/` prefix (configured in tsconfig)
- Group: external packages, internal absolute, relative, separated by blank line
- No barrel files (`index.ts` re-exports), they break tree-shaking

## Don't do this

- Don't use `getServerSideProps` or `getStaticProps` (Pages Router APIs)
- Don't use `next/router` (use `next/navigation`)
- Don't use `<a>` for internal links (use `<Link>`)
- Don't use `<img>` for static images (use `<Image>`)
- Don't put secrets in `NEXT_PUBLIC_*` variables (they ship to the browser)
- Don't use `useEffect` to set state from props
