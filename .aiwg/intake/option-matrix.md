# Option Matrix (Project Context and Priorities)

| Field | Value |
|---|---|
| Derived from | `AGENTS.md`, ADRs 0003, 0008, 0009, 0013, 0014 |
| Source state | `184371f`, 2026-10-28 |

## Project Reality

- A prototype: the codename stays internal and branding is undecided (`AGENTS.md`).
- The proving ground for the studio's crates (bevy_markup, bevy_mcp_harness) and its agent-playtesting method.
- Product direction elsewhere in the studio: single-player titles with verified leaderboards (infrastructure ADR 0011, 0016); this prototype stays multiplayer.

## Priorities (weights sum to 10)

| Priority | Weight | Evidence |
|---|---|---|
| Correct, authoritative multiplayer (server decides; prediction optional) | 3 | ADR 0003, 0004, 0008, 0017 |
| Agent-driven QA on the real game | 3 | ADR 0009–0012, 51 playtests |
| Steam Deck as min-spec, identical content across hardware | 2 | `AGENTS.md` Platform targets |
| Post-release debuggability (determinism, replay) | 2 | ADR 0013 |

## Trade-offs Already Made

- bevy_ahoy's KCC over a custom controller (ADR 0008); prediction off by default.
- System fonts over bundled CJK fonts (ADR 0016 superseding 0002).
- Join-burst input corrections accepted, not fixed (`AGENTS.md`).

## Sources

- @AGENTS.md
- @docs/agents/adr/0003-room-based-interest-management.md
- @docs/agents/adr/0008-adopt-bevy-ahoy-character-controller.md
- @docs/agents/adr/0009-agent-tool-api-via-brp.md
- @docs/agents/adr/0013-server-determinism-and-session-replay.md
- @docs/agents/adr/0016-system-fonts.md
