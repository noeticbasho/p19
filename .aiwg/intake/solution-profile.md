# Solution Profile (Current System)

| Field | Value |
|---|---|
| Derived from | `AGENTS.md`, ADRs 0001–0019, bug ledger, playtest index, CI workflow |
| Source state | `184371f`, 2026-10-28 |

## Current Profile

**Pre-release prototype with a production-shaped architecture.** The networking model (authoritative server, prediction, rollback, interest management, tokens over TLS) and the agent QA practice (51 playtests, 11 bugs all fixed) are well beyond prototype norms; automated testing is not (7 unit tests, CI builds only). Idle since 2026-10-09 and a Bevy version behind the rest of the studio.

| Dimension | Level | Evidence |
|---|---|---|
| Security | Dev-grade | TOFU-pinned self-signed TLS for tokens (`AGENTS.md`) |
| Reliability | Medium | known gaps: no disconnect cleanup, single spawn point, no level switching |
| Testing & quality | Low automated, high exploratory | 7 unit tests; 51 agent playtests; no gameplay tests in CI |
| Process rigor | High | 19 ADRs, bug and playtest skills, AGENTS.md as current state |

## Recommended Profile Adjustments

- Turn the most-used playtest flows (connect, lobby, move, attack) into a scripted headless smoke run in CI, through the agent tool API (R-003).
- Remove the five unused dependencies before the Bevy 0.20 migration (the plan).

## Improvement Roadmap

1. Disconnect cleanup and per-player spawn points (the most visible gaps).
2. Bevy 0.20 migration when its blockers clear (@.aiwg/planning/bevy-0.20-migration.md).
3. A CA-signed token endpoint before any public build.

## Sources

- @AGENTS.md
- @docs/agents/adr/0014-multiplayer-hardening-netcode-tokens-and-portable-builds.md
- @docs/agents/bug_reports/README.md
- @docs/agents/playtests/index.md
