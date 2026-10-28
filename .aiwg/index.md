# SDLC Index — prototype_19

_Generated: 2026-10-28 — 10 pages · consumer `sdlc-complete` · workspace `noetic-basho-technologies` (root: `../aiwg`)_

Derived pages cite their sources with `@path` mentions; provenance records are in `.aiwg/research/provenance/records/`. Authoritative: `AGENTS.md`, `docs/agents/adr/`, `docs/agents/bug_reports/`, `docs/agents/playtests/`, `docs/agents/skills/`. `docs/humans/` is human-only.

## Intake (3)
- [Project intake](intake/project-intake.md) — always-multiplayer Bevy 0.19 prototype: authoritative server, prediction, rooms, tokens over TLS; agent playtesting's origin
- [Solution profile](intake/solution-profile.md) — production-shaped architecture, strong agent QA, few automated tests
- [Option matrix](intake/option-matrix.md) — priorities: authoritative multiplayer, agent QA, Steam Deck, replay

## Requirements (2)
- [Use-case briefs](requirements/use-cases.md) — UC-001–007 built (join, move, fight, menus, VR, agent playtest, replay); UC-101–105 planned (Known gaps)
- [Supplementary specification](requirements/supplementary-spec.md) — multiplayer correctness, security, platform, supportability requirements with their checks

## Risks (1)
- [Risk list](risks/risk-list.md) — R-001–009; highest: a Bevy version behind, no disconnect cleanup, no gameplay tests, one black level

## Testing (2)
- [Test strategy](testing/test-strategy.md) — 7 unit tests, CI builds, 51 agent playtests
- [Defect register](testing/defect-register.md) — bug_0001–0011, all fixed; open gaps in `AGENTS.md`

## Planning (1)
- [Bevy 0.20 migration](planning/bevy-0.20-migration.md) — waiting on bevy_ahoy and bevy_seedling; six unused dependencies to remove now

## Architecture (1)
- [Architecture](architecture/README.md) — pointer to `AGENTS.md` and ADRs 0001–0019
