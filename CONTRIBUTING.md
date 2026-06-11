# Contributing a Rules File

Thanks for considering a contribution. Here's how to add one.

## Structure

```
rules/
  your-stack-name/
    .cursorrules         (for Cursor)
    CLAUDE.md            (for Claude Code)
    README.md            (rationale, what this optimizes for, version pinning)
```

The folder name should describe the stack precisely. Good: `nextjs-app-router`, `rails-7`, `fastapi`. Bad: `next` (which version? router?), `python` (too broad).

## What makes a good rules file

- **Short.** Aim for under 200 lines. AI assistants have context budgets; a 1000-line rules file dilutes the rest of the prompt.
- **Specific.** Rules like "write good code" don't help. Rules like "always use Server Components by default; only use Client Components when you need state, refs, or browser APIs" do.
- **Stack-versioned.** Pin the framework version your rules target. Rules for Next.js 14 may not apply to Next.js 12.
- **Negative examples included.** Show what NOT to do alongside what to do. AI assistants pattern-match; negative examples are how you steer them.
- **No filler.** Don't restate things the framework's own docs cover. Focus on team-specific patterns.

## Required sections

The README in your stack folder should include:

1. **Stack version**, exact versions you tested with (e.g. "Next.js 14.2, TypeScript 5.4, Node 20")
2. **What this optimizes for**, speed of shipping? type safety? convention over configuration? Be honest.
3. **What this is NOT for**, list contexts where these rules would be wrong (e.g. "Don't use these rules for a static marketing site; they assume an interactive app")
4. **Tested in**, at least one tool you've validated this with (Cursor, Claude Code, etc.)

## Quality checklist

- [ ] Rules file is under 200 lines
- [ ] Stack version is pinned in the folder README
- [ ] At least 5 specific rules (not generic advice)
- [ ] Includes both "do this" and "don't do this" examples
- [ ] No hardcoded secrets, internal URLs, or company-specific references
- [ ] Tested in at least one AI coding tool
- [ ] Added a row to the table in the top-level README

## PR title format

`add rules: stack-name` (e.g. `add rules: remix-2`)

## What gets rejected

- Rules files for tools that aren't actually used (no traction = no maintenance)
- Rules that just rephrase the framework's official getting-started guide
- Rules that hardcode a single team's idiosyncratic preferences without rationale
- Rules with broken or outdated framework version pinning
