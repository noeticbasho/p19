# Test Strategy

| Field | Value |
|---|---|
| Template | `test/test-strategy-template.md` (condensed) |
| Derived from | `AGENTS.md` ("Known gaps", "Commands", "Agent tool API and headless modes"), `.github/workflows/ci.yml`, playtest index, `docs/agents/skills/playtest.md` |
| Source state | `184371f`, 2026-10-28 |

## Context and Objectives

Quality here comes from agents playtesting the real game: a server plus headless clients driven over the agent tool API, each run filed as a playtest report (51 so far) and each defect as a bug report (11, all fixed). Automated tests are few by circumstance, not design (`AGENTS.md` Known gaps).

## Test Levels and Scope

| Level | What | Where | When |
|---|---|---|---|
| Unit | player name generation (4), token server-address fallback (3) | `p19_shared::player`, `p19_server::networking` | `cargo test --workspace` (not in CI) |
| Build | server; shippable steamrt4 client | CI | every push |
| Agent playtest | connect, lobby, levels, movement, combat, UI, options; screenshots and UI dumps | `--mcp` / `--no-render` clients over BRP/MCP; `docs/agents/playtests/` | per change |
| Replay | deterministic server replay of recorded sessions | `server --replay` | on demand (movement mismatch open) |
| Platform | Steam Deck build and run | steamrt4 toolbox | by hand |

**In scope:** the three crates. **Out of scope:** dependencies (forks tracked in `AGENTS.md`).

## Automation Strategy

CI builds only. The first step is a scripted headless smoke run in CI (risk R-003), then the migration's regression check (@.aiwg/planning/bevy-0.20-migration.md).

## Defect Management

Bug reports in `docs/agents/bug_reports/` per `docs/agents/skills/bugreport.md`; playtest reports per `docs/agents/skills/playtest.md`, newest first in `docs/agents/playtests/index.md`. Index: @.aiwg/testing/defect-register.md.

## Requirements and Risk Coverage

Most requirements in @.aiwg/requirements/supplementary-spec.md are covered by playtests only; automated: NFR-SEC-001 (token address), NFR-SUP-003 (names), NFR-PLAT-003 (steamrt4 build).

## Sources

- @AGENTS.md
- @docs/agents/playtests/index.md
- @docs/agents/skills/playtest.md
- @docs/agents/skills/bugreport.md
