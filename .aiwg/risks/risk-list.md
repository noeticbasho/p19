# Risk List

| Field | Value |
|---|---|
| Template | `management/risk-list-template.md` |
| Derived from | `AGENTS.md`, ADRs 0008, 0013, 0014, bug ledger, the dependency survey (2026-10-28) |
| Source state | `184371f`, 2026-10-28 |
| Owner | Project owner (all risks) |

Scales High / Medium / Low; Exposure = Impact × Likelihood. Never renumber.

## Register

| Risk ID | Description | Impact | Likelihood | Exposure | Mitigation Strategy | Owner | Status | Residual Risk |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| R-001 | A Bevy version behind the studio: the studio's crates move on 0.20 (bevy_markup 0.4 → 0.7 has 4 breaking changes; bevy_mcp_harness 0.3.1 → 0.4) and the gap grows; the character controller (bevy_ahoy) and audio (bevy_seedling) have no 0.20 release. | High | High | HxH=High | The migration plan: remove unused dependencies now; migrate when the blockers release, or fork them. | Owner | Open | Medium |
| R-002 | Disconnected players are never cleaned up; a rejoining client never gets control until a server restart. | High | High | HxH=High | Clean up on disconnect (non-persistent `ControlledBy` lifetime or an explicit despawn). | Owner | Open | Low |
| R-003 | No gameplay tests: 7 unit tests, CI builds only; regressions surface only in agent playtests. | Medium | High | MxH=High | A scripted headless smoke run through the agent tool API in CI. | Owner | Open | Medium |
| R-004 | Netcode tokens use a TOFU-pinned self-signed certificate: unfit for a public build. | High | Low | HxL=Medium | CA-signed certificate on a real backend before any public release (ADR 0014). | Owner | Accepted | Low |
| R-005 | Session replay doesn't reproduce movement (~1 vs ~12.7 units over 60 ticks), so post-release debugging (ADR 0013) can mislead. | Medium | Medium | MxM=Medium | Fix the injected `Fire<A>` timestamps (the leading suspect). | Owner | Open | Low |
| R-006 | Owner forks to maintain: bevy_mod_outline (skinned-motion fix), gltf (`KHR_texture_basisu`), fluent-syntax; each Bevy bump means rebasing them. | Medium | Medium | MxM=Medium | Upstream the patches; track in `AGENTS.md` "Dependency layout". | Owner | Open | Medium |
| R-007 | VR is unverified: grip poses likely never track (bevy_xr_utils 0.6.0); VR crates have no 0.20 release. | Low | High | LxH=Medium | Re-verify on a headset; feature-gate VR during the migration. | Owner | Open | Low |
| R-008 | Only one level, and it renders black (no lights); no level switching. | Medium | High | MxH=High | Lights in `minimal.level.ron`; level unloading on the server. | Owner | Open | Low |
| R-009 | Repository on the personal `nchashch` account; the studio's other repositories are on `noeticbasho`. | Medium | Low | MxL=Low | Transfer when convenient. | Owner | Open | Low |

## Sources

- @AGENTS.md
- @docs/agents/adr/0008-adopt-bevy-ahoy-character-controller.md
- @docs/agents/adr/0013-server-determinism-and-session-replay.md
- @docs/agents/adr/0014-multiplayer-hardening-netcode-tokens-and-portable-builds.md
- @.aiwg/planning/bevy-0.20-migration.md
