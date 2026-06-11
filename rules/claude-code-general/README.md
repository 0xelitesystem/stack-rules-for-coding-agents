# Claude Code (general) rules

## Stack version

Stack-agnostic. Designed for any project type.

## What this optimizes for

- Reading context before writing code
- Matching existing codebase conventions instead of imposing AI defaults
- Predictable, conservative behavior (don't refactor unrelated code, don't add unrequested features)
- Test discipline

## What this is NOT for

- Replacing stack-specific rules. This is meant to be combined WITH a stack-specific rules file in larger projects.
- Greenfield projects with no existing conventions (some rules assume there's an existing codebase to match)

## Tested in

- Claude Code (works as `CLAUDE.md`)
- Cursor (works as `.cursorrules`)

## Customize for your team

- Adjust the "tests" section if your project doesn't have automated tests
- Add specific commit message convention if you use Conventional Commits
- Add team-specific rules around PR/code review process
