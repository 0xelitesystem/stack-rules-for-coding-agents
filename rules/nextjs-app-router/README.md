# Next.js App Router rules

## Stack version

- Next.js 14.x or 15.x
- TypeScript 5.x
- React 18+ / 19+
- Node 20+

## What this optimizes for

- Following App Router conventions (so the framework features just work)
- Type safety
- Server-first architecture (smaller client bundles)
- Avoiding common foot-guns from the Pages Router era

## What this is NOT for

- Pages Router projects (the rules contradict that style)
- Static-only sites (the data-fetching rules are overkill)
- Library code (these rules assume an application, not a published package)

## Tested in

- Cursor (Composer + tab autocomplete)
- Claude Code

## Customize for your team

Common things teams override:
- Replace Tailwind with your styling solution
- Add team-specific conventions for state management (Zustand vs Redux vs context)
- Add specific testing framework rules (Vitest, Playwright, etc.)
