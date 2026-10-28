# Use-Case Briefs

| Field | Value |
|---|---|
| Template | `requirements/use-case-brief-template.md` (one brief per section) |
| Derived from | `AGENTS.md` ("What this is", "Known gaps", "Commands", "Agent tool API and headless modes"), ADRs 0003–0017 |
| Source state | `184371f`, 2026-10-28 |

Status: **Built** or **Planned**. IDs are stable.

## Actors

| Actor | Who |
|---|---|
| Player | Plays on desktop, Steam Deck or in VR |
| Host | Runs `p19-server` (UDP 6000, token endpoint HTTPS 6001) |
| Agent | AI agent playtesting through the agent tool API (`--mcp` / `--no-render` clients) |
| Developer | Debugs a recorded session with `server --replay` |

## Built

### UC-001 — Player joins a game

- **Main success scenario:** the client fetches a per-client netcode token over TLS (TOFU-pinned), connects over UDP, lands in the lobby room, picks a level; the server loads it and moves the player's character into the game room.
- **Notes:** a disconnected player's character is never cleaned up; a rejoining client then never gets control. Sources: ADR 0003, 0004, 0014, `AGENTS.md` Known gaps.

### UC-002 — Player moves

- **Main success scenario:** BEI actions replicate to the server; bevy_ahoy's KCC moves the character authoritatively; with prediction on, the client runs the KCC too and lightyear rolls back on corrections; look is client-owned absolute input.
- **Notes:** no ground friction; join bursts can delay inputs for ~10 ticks. Sources: ADR 0008, 0017, bug_0004, bug_0009–0011.

### UC-003 — Player fights and spawns objects

- **Main success scenario:** the client sends attack/kill attempts and spawn requests; the server resolves them and replicates the results within rooms.
- **Sources:** bug_0001–0003, `AGENTS.md`.

### UC-004 — Player uses the menus

- **Main success scenario:** main menu, lobby, pause and options screens in bevy_markup (HTML/CSS/Fluent, system fonts, gamepad-first navigation, Steam Deck glyphs).
- **Sources:** ADR 0001, 0015, 0016, playtests 0050–0051.

### UC-005 — Player plays in VR

- **Main success scenario:** with `vr = true` in the client config, OpenXR drives the camera; VR locomotion mocks the movement action.
- **Notes:** grip poses likely never track (bevy_xr_utils 0.6.0); not re-verified on a headset. Source: `AGENTS.md` Known gaps.

### UC-006 — Agent playtests the game

- **Main success scenario:** the agent launches the server and a `--mcp` (offscreen) or `--no-render` client, drives it over BRP/MCP (state, UI tree, screenshots, device-level input, p19's `game/select`/`game/trigger`/`game/levels`), and files a playtest report and bug reports.
- **Sources:** ADR 0009–0012, `docs/agents/skills/playtest.md`, 51 playtest reports.

### UC-007 — Developer replays a session

- **Main success scenario:** the server records a session; `server --replay` re-runs it deterministically.
- **Notes:** replayed movement covers far less distance than live. Source: ADR 0013.

## Planned (from Known gaps)

### UC-101 — Disconnected players are cleaned up

- **Status:** missing; characters persist (`Lifetime::Persistent`).

### UC-102 — Players spawn apart

- **Status:** missing; one spawn point.

### UC-103 — Switch levels without a restart

- **Status:** missing; the server never unloads a level.

### UC-104 — NPCs act through an input path

- **Status:** missing; `Fire<A>` injection is the likely path.

### UC-105 — Character authoring pipeline

- **Status:** designed, mostly unimplemented (`AGENTS.md`).

## Sources

- @AGENTS.md
- @docs/agents/adr/0003-room-based-interest-management.md
- @docs/agents/adr/0004-decouple-player-character-from-connection-entity.md
- @docs/agents/adr/0008-adopt-bevy-ahoy-character-controller.md
- @docs/agents/adr/0012-no-render-agent-client-mode.md
- @docs/agents/adr/0013-server-determinism-and-session-replay.md
- @docs/agents/adr/0014-multiplayer-hardening-netcode-tokens-and-portable-builds.md
- @docs/agents/adr/0015-client-ui-on-bevy-markup.md
- @docs/agents/adr/0017-client-owned-absolute-look-input.md
- @docs/agents/skills/playtest.md
