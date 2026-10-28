# Supplementary Specification (Non-Functional Requirements)

| Field | Value |
|---|---|
| Template | `requirements/supplementary-spec-template.md` |
| Derived from | `AGENTS.md` ("What this is", "Platform targets", "Commands", "Dependency layout"), ADRs 0003, 0013, 0014, 0016 |
| Source state | `184371f`, 2026-10-28 |

Numbered, testable statements with what verifies each ("—" = no automated check; "playtest" = covered by agent playtest reports, not automated). `AGENTS.md` is authoritative.

## Correctness (multiplayer)

| ID | Requirement | Source | Verified by |
|---|---|---|---|
| NFR-MP-001 | The server is authoritative; the client sends intent and never decides outcomes | `AGENTS.md` | playtest |
| NFR-MP-002 | A client receives only entities in rooms its connection belongs to | ADR 0003, bug_0003 | playtest |
| NFR-MP-003 | Rollback restores all KCC state (no ghost jumps after corrections) | bug_0004 | playtest |
| NFR-MP-004 | The camera and the server agree on look (no walking at an angle) | ADR 0017, bug_0009–0011 | playtest |
| NFR-MP-005 | A recorded session replays deterministically on the server | ADR 0013 | — (movement mismatch open) |

## Security

| ID | Requirement | Source | Verified by |
|---|---|---|---|
| NFR-SEC-001 | Each client gets its own netcode token over TLS; the token names the server's address, not the client's | ADR 0014, bug_0005, bug_0006 | `networking::host_header_ip_wins`, `loopback_host_header`, `missing_host_falls_back_to_default_route_then_peer` |
| NFR-SEC-002 | Production uses a CA-signed certificate (TOFU self-signed is dev-only) | `AGENTS.md` Known gaps | — (not met) |
| NFR-SEC-003 | The agent tool API exists only with the `dev-tools` feature, on localhost | ADR 0009 | — |
| NFR-SEC-004 | Machine-local keys and pins (`network/`) are never committed | `AGENTS.md` Commands | `.gitignore` |

## Performance and Platform

| ID | Requirement | Source | Verified by |
|---|---|---|---|
| NFR-PLAT-001 | Runs within Steam Deck's ~4 GB VRAM; KTX2/BC6H assets | `AGENTS.md` Platform targets | — |
| NFR-PLAT-002 | The world's content is identical across hardware; only fidelity scales | `AGENTS.md` Platform targets | — |
| NFR-PLAT-003 | Shippable client builds come from the steamrt4 toolbox | `AGENTS.md` Commands | CI "Build client (steamrt4, shippable)" |
| NFR-PLAT-004 | Text renders with the system's fonts; no font files ship | ADR 0016 | — |

## Supportability

| ID | Requirement | Source | Verified by |
|---|---|---|---|
| NFR-SUP-001 | A fresh clone with Git LFS runs end to end with nothing else provisioned | `AGENTS.md` Commands | playtest 0039 |
| NFR-SUP-002 | Every defect gets a bug report; every agent run a playtest report | `AGENTS.md` Rules | — (convention) |
| NFR-SUP-003 | Player names are two words, unique with numeric suffixes | `AGENTS.md` | `player::generated_name_has_two_words`, `colliding_base_gets_suffix_two`, `suffix_increments_past_existing_suffixes`, `different_seeds_tend_to_differ` |
| NFR-SUP-004 | Renaming a crate or moving Skein-authored types requires re-exporting the `.glb`s (reflected type paths) | `AGENTS.md` Dependency layout | — |

## Design Constraints

| ID | Requirement | Source |
|---|---|---|
| NFR-DES-001 | Bevy 0.19.1; lightyear 0.30 with `input_bei` (without it the client panics at connect) | `AGENTS.md` Dependency layout |
| NFR-DES-002 | Every replicated component and message is registered in `SharedReplicationPlugin`, on the one `OrderedReliable` channel | `AGENTS.md` |
| NFR-DES-003 | `docs/humans/` is human-only; agents never write there | `AGENTS.md` Rules |

## Sources

- @AGENTS.md
- @docs/agents/adr/0003-room-based-interest-management.md
- @docs/agents/adr/0013-server-determinism-and-session-replay.md
- @docs/agents/adr/0014-multiplayer-hardening-netcode-tokens-and-portable-builds.md
- @docs/agents/adr/0016-system-fonts.md
- @docs/agents/adr/0017-client-owned-absolute-look-input.md
- @docs/agents/bug_reports/bug_0004.md
- @docs/agents/bug_reports/bug_0005.md
