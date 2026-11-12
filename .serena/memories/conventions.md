# Conventions

Authoritative rules live in `.claude/rules/*.md` (read them; not duplicated here). Key points specific to this repo:

- TS style: const over let, explicit return types on exports, `unknown` over `any`, Result pattern for expected failures, `@/` alias imports, tests as `it('should ... when ...')`
- Git: Conventional Commits, branches `feat/<ticket>-desc` / `fix/...`, never push to `main`, stage files by explicit path (parallel sessions share the worktree)
- Solidity: NatSpec (`@title/@notice/@param/@dev`) on contracts and externals, 4-space indent, solhint zero warnings
- Existing tests are Mocha/Chai (`describe`/`it`), not Vitest, despite the generic testing rule mentioning `vi.fn()`
- Browser automation: prefer Chrome DevTools MCP (see `.claude/rules/development.md`)
- Rules are partly in Japanese; user-facing replies to the user in Japanese
