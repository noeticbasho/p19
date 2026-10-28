# Defect Register

| Field | Value |
|---|---|
| Derived from | `docs/agents/bug_reports/README.md`, bug_0001–0011, `AGENTS.md` Known gaps |
| Source state | `184371f`, 2026-10-28 |

An index; the bug reports are authoritative. All eleven are fixed; most were found in agent playtests.

| Bug | Status | Area |
|---|---|---|
| bug_0001 combat caster resolution dropped every attack/kill | Fixed `6d2fb0a` | combat |
| bug_0002 killing a player panicked the victim's `--no-render` client | Fixed `9377b41` | client, agent mode |
| bug_0003 spawned cubes/NPCs bypassed room filtering | Fixed `6d59fa0` | interest management |
| bug_0004 KCC state not rollback-registered (ghost jumps) | Fixed `c2c4b76` | prediction |
| bug_0005 connect token embedded the client's own IP | Fixed `89e44cc` | netcode tokens |
| bug_0006 netcode server rejected all tokens (wildcard bind vs whitelist) | Fixed `89e44cc` | netcode |
| bug_0007 dev console / pause modal didn't lock movement | Fixed | input |
| bug_0008 `--no-common-assets` client panicked on the pause modal | Fixed | client |
| bug_0009 look input in a menu-opening tick turned the server but not the camera | Fixed | look |
| bug_0010 standing on a spinning cube turned the server's look but not the camera | Fixed | look |
| bug_0011 the server's look pitch mirrored the client's | Fixed | look |

Open defects are recorded as `AGENTS.md` Known gaps rather than bug reports (disconnect cleanup, single spawn point, replay movement, no ground friction, VR grip poses).

## Sources

- @docs/agents/bug_reports/README.md
- @docs/agents/bug_reports/bug_0001.md
- @docs/agents/bug_reports/bug_0004.md
- @docs/agents/bug_reports/bug_0011.md
- @AGENTS.md
