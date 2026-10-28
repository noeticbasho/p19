# Bevy 0.20 Migration Plan

| Field | Value |
|---|---|
| Derived from | `Cargo.toml`, `crates/*/Cargo.toml`, `Cargo.lock`, source references, crates.io and upstream repositories (queried 2026-10-28), `AGENTS.md` "Dependency layout" |
| Source state | `184371f`, 2026-10-28 |
| Status | **Waiting** — the character controller and audio crates have no Bevy 0.20 release |

The rest of the studio is on Bevy 0.20 (bevy_markup 0.5+, bevy_mcp_harness 0.4, vtuber, asset_inspector); this repository is on 0.19.1 with bevy_markup 0.4.0 and bevy_mcp_harness 0.3.1. Re-run the survey (crates.io `max_stable_version` and its `bevy` requirement per dependency) before starting.

## Dependency survey (2026-10-28)

| Crate | In use? | Now | Bevy 0.20 | Upstream state |
|---|---|---|---|---|
| bevy_ahoy | yes (14 files; the KCC, ADR 0008) | 0.2.0 | **no** | default branch still 0.19, last push 2026-08-06 |
| bevy_seedling | yes (4 files; audio) | 0.8.0 | **no** | default branch still 0.19, last push 2026-08-09 |
| bevy_hanabi | yes (3 files; VFX) | 0.19.0 | unreleased | "Migrate to Bevy 0.20 and WESL shaders" (#576) merged 2026-10-15; a git dependency works until a release |
| bevy_mod_outline | yes (2 files) | 0.13.0, owner's fork `fix/skinned-motion-outline` | **no** | upstream idle since 2026-07-09; the fork needs migrating itself |
| bevy_mod_openxr, bevy_mod_xr, bevy_xr_utils | yes (VR) | 0.6.0 | **no** | "Update to bevy 0.20 + openxrs 0.22" (bevy_oxr #212) open |
| lightyear (+ `lightyear_avian3d`, `lightyear_inputs_bei`) | yes | 0.30 | 0.31.0 | released 2026-10-21; review its changelog (netcode, inputs) |
| avian3d | yes | 0.7.0 | 0.8.0 | released 2026-10-20 |
| bevy_enhanced_input | yes | 0.26.0 | 0.27.2 | released |
| bevy_skein | yes | 0.6.0 | 0.7.0 | released; Skein-authored `.glb`s may need re-export (reflected type paths) |
| bevy_asset_loader, bevy_common_assets | yes | 0.27 / 0.17 | 0.28.1 / 0.18.0 | released |
| noiz | yes | 0.5.0 | 0.6.0 | released |
| bevy_markup | yes (every UI surface) | 0.4.0 | 0.7.0 (+ unreleased) | studio crate; 4 breaking changes in 0.5–0.7 (form submit, `RemSize`, Markdown interpolation, `<img>` sizing) plus Bevy 0.20 |
| bevy_mcp_harness | yes (`dev-tools`) | 0.3.1 | 0.4.0 | studio crate; `physics_debug` removed in 0.4.0 — avian3d 0.8 now supports 0.20, so the harness can restore it |
| vleue_navigator | **no** (0 references) | 0.16 | 0.17.0 | remove |
| bevy_simple_text_input | **no** | 0.15.0 | no | remove |
| bevy_vrm1 | **no** | 0.9.5 | studio fork has a `bevy-0.20` branch | remove |
| bevy_vello | **no** | 0.14.0 | no | remove |
| audionimbus | **no** (direct only; `bevy_seedling` doesn't use it) | 0.16.0 | no | confirm, then remove |
| bevy-steamworks | **no** (declared for Steam integration) | 0.17.0 | no | remove until Steam integration starts |

## Plan

**Phase 0 — now, on Bevy 0.19 (no regret).**

1. Remove the six unused dependencies above, and `Character`'s duplicate replication registration and the other dead code `AGENTS.md` lists. Fewer crates to wait for.
2. bevy_mcp_harness: restore `physics_debug` on avian3d 0.8 and release (the client enables `bevy_mcp_harness/physics_debug`).
3. A scripted headless smoke run (server + `--no-render` client: connect, lobby, pick a level, move, attack) through the agent tool API, so the migration has a regression check beyond playtests (R-003).

**Phase 1 — start when bevy_ahoy and bevy_seedling release for Bevy 0.20** (the two hard blockers; or decide to migrate them on owner forks, as with bevy_mod_outline and bevy_vrm1).

1. Bevy 0.19.1 → 0.20 and the released crates together: lightyear 0.31, avian3d 0.8, bevy_enhanced_input 0.27, bevy_skein 0.7, bevy_asset_loader 0.28, bevy_common_assets 0.18, noiz 0.6.
2. bevy_hanabi from git (`main`, after #576) until a release.
3. Migrate the bevy_mod_outline fork (the `fix/skinned-motion-outline` patch on top of a 0.20 port).
4. bevy_markup 0.4 → 0.7: the four breaking changes, then a UI playtest of every screen.
5. bevy_mcp_harness 0.3.1 → 0.4 (+ `physics_debug`).
6. VR: if bevy_oxr #212 hasn't landed, feature-gate VR off for the migration rather than wait.
7. Re-export Skein-authored `.glb`s if reflected type paths changed; check the gltf fork (`KHR_texture_basisu`) against 0.20's gltf version.

**Verification:** the Phase 0 smoke run, then a full agent playtest (connect → lobby → level → movement with and without prediction → combat → spawning, two clients), a Steam Deck build in steamrt4, and `AGENTS.md` updated in the same change. Record the migration in an ADR (bevy_markup's 0.5.0 and vtuber's ADR 0002 are the studio's previous 0.20 migrations).

## Sources

- @AGENTS.md
- @docs/agents/adr/0008-adopt-bevy-ahoy-character-controller.md
- @docs/agents/adr/0015-client-ui-on-bevy-markup.md
- @docs/agents/skills/playtest.md
