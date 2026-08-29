# citadel-cli — agent primer

LLMs: read this first. `CLAUDE.md` contains `@AGENTS.md` — **edit `AGENTS.md`, never `CLAUDE.md`**. Humans: [HUMANS.md](HUMANS.md). Commits: [CONTRIBUTING.md](CONTRIBUTING.md).

## Repository shape

```
main.go              Cobra entry
cmd/                 Subcommands
internal/clicfg/     XDG config
internal/completion/ Shell completion cache
internal/mcpclient/  MCP HTTP client
specs/active|parked/ SDD specs
.github/workflows/   ci.yml, cli-release.yml
Makefile             build / verify
```

Spec lifecycle: `mcp__citadel-sdd__*` MCP tools only (table below). Releases on `v*` tags.

## Invariants

- Generic Git rules: `~/.claude/CLAUDE.md`. **Commit freely; push only on explicit instruction.**
- Specs MUST pass `mcp__citadel-sdd__spec_lint` before commit. Task bullets `- [ ]` / `- [x]`; priority headings only in `tasks.md`.
- **Never hand-edit** spec status, DTG stamps, or `tasks.md` checkboxes — use MCP tools.

| What | Tool |
| --- | --- |
| Claim | `spec_claim` |
| Approve | `spec_approve` |
| Close | `spec_close` |
| Block / unblock | `spec_block` / `spec_unblock` |
| Reopen | `spec_reopen` |
| Hand off | `spec_handoff` |
| Check task | `spec_task_check` |
| Add task | `spec_task_add` |
| Lint | `spec_lint` |
| List / read | `spec_list` / `spec_read` |
| Health | `sdd_doctor` |

Hand-edit only: new spec scaffold (then `spec_claim`), body prose, parking (`specs/parked/` + PARKED stamp).

## Test conventions

`go test -race ./...` / `make verify`. Live tests env-gated; safe in CI when unset.

## Pre-push

`make verify` before push.
