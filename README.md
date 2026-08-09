# cursor-rules-collection

Curated `.cursorrules` and `CLAUDE.md` files for popular stacks. Drop one into your project and your AI coding assistant stops fighting the conventions.

This is for Cursor, Claude Code, Continue, Cline, and any other AI coding tool that reads project-level rules files.

## Why a curated collection

There are sprawling "awesome" lists with hundreds of entries; most are unmaintained or written by someone unfamiliar with the stack. This repo keeps it small and opinionated:

- Each rules file is for a real, current stack version
- Each is tested by someone shipping in that stack
- Each comes with a short rationale explaining what it optimizes for
- Files get pruned when stacks shift; no dead entries

## Use a rules file

Pick a stack. Copy the rules file into your project root:

```bash
# For Cursor:
cp rules/nextjs-app-router/.cursorrules .

# For Claude Code:
cp rules/nextjs-app-router/CLAUDE.md .

# For both: keep both files, both tools read their own.
```

Most rules files are small (50-150 lines). Read it before committing, you may want to delete or modify rules that don't fit your team.

## Rules in this collection

| Stack | Rules file |
|---|---|
| Next.js (App Router, TypeScript) | [nextjs-app-router](./rules/nextjs-app-router) |
| Rails 7 (Hotwire / Stimulus) | [rails-7](./rules/rails-7) |
| Django 5 (REST framework) | [django-5](./rules/django-5) |
| SvelteKit | [sveltekit](./rules/sveltekit) |
| FastAPI (Python 3.11+) | [fastapi](./rules/fastapi) |
| Go (standard library, no frameworks) | [golang-stdlib](./rules/golang-stdlib) |
| Rust (Axum + Tokio) | [rust-axum](./rules/rust-axum) |
| TypeScript (strict mode, library author) | [typescript-strict-library](./rules/typescript-strict-library) |
| Python (uv + pyproject.toml) | [python-uv](./rules/python-uv) |
| General Claude Code (any stack) | [claude-code-general](./rules/claude-code-general) |

More stacks welcome. See [CONTRIBUTING.md](./CONTRIBUTING.md).

## What goes in a rules file

The rules files in this repo focus on the things AI assistants get wrong without context:

- **File structure conventions** the framework expects
- **Naming and casing** the team uses (snake_case vs camelCase, Component naming, file naming)
- **Patterns to prefer** (functional components vs class components, dependency injection vs globals)
- **Patterns to avoid** (deprecated APIs, anti-patterns common in old tutorials)
- **Testing approach** (test framework, test file location, test naming)
- **Imports and dependencies** (package manager, lock file, import style)
- **Error handling style**
- **Commit and PR conventions**

What rules files DON'T need to specify:

- Things the linter/formatter already enforces (Prettier, Black, gofmt). Defer to those.
- Things that are universally true regardless of stack (e.g. "don't hardcode secrets")
- Personal preferences the team hasn't agreed on

## .cursorrules vs CLAUDE.md vs others

These are different files for different tools:

- **`.cursorrules`**, Cursor reads this for project context
- **`CLAUDE.md`**, Claude Code reads this in the project root and walks up the tree
- **`continue.config.json`** with system prompt, Continue uses this
- **`.cline/rules.md`**, Cline reads this

Most rules in this collection are stack-specific advice that applies regardless of tool. The folders contain both a `.cursorrules` and a `CLAUDE.md` (the content is nearly identical; format differs slightly to match each tool's conventions).

## Contribute

Got a rules file for a stack we're missing? PR welcome. See [CONTRIBUTING.md](./CONTRIBUTING.md).

## More

Part of a catalog of single-file browser tools and plain-language references, all MIT licensed and dependency-free: [0xelitesystem.github.io](https://0xelitesystem.github.io/). Built by [elitesystem.ai](https://elitesystem.ai).

## License

MIT. Each rules file is independent, copy one into your project without inheriting the rest.

## Related

- [claude-skills-collection](https://github.com/0xelitesystem/claude-skills-collection), task-specific skills for Claude
- [prompt-templates](https://github.com/0xelitesystem/prompt-templates), production prompts for Claude API
- [claude-mcp-starter](https://github.com/0xelitesystem/claude-mcp-starter), MCP server starter templates
