# PLAN

**This file owns every project decision.** No other file states one; they point here. The
Status is rewritten (not appended) every session.

---

## Status — 2026-10-30 (M0 in progress)

Kickoff done; owner approved the plan and the overnight run (M0-M7, then ten competitive
decks). M0 agents running: rules primer, rights + card data + decklists, scaffold.

---

## Decisions

| # | Decision | By | Date |
|---|---|---|---|
| D1 | **First slice: four starter decks**, `.asphodel/paradise Starter Decks` (API prefix `PRDSD`, 2026-08-21: Dante, Lorraine) and `Distorted Reflections Starter Decks` (`DTRSD`, 2025-07-25: Ciel, Diana). Standard format, 1v1 vs AI. The first playable ships when one pairing works end to end; the other champions join as their cards pass tests. Lists: `data/decklists.json`. | owner | 2026-10-30 |
| D2 | **Look: a living archive vault.** The board is a vaulted archive: zones are lit catalogue drawers and index tabs, catalogue numbers in a monospace face, one ink colour per element, each level-up staged as a new volume sealed onto the lineage shelf. **Must not look like:** lorecannae (enchanted storybook: gold filigree frames, star card backs, serif type, centred menu dialog, hand fan), Shadowforge (lorecannae re-coloured), Xross Forge (neon esports broadcast: scoreboard HUD, lower thirds, stage beams). Gate before the first playable ships: title, deck picker and mid-game board screenshots side by side with lorecannae's and Xross Forge's (KB README rule 21). | owner | 2026-10-30 |
| D3 | **Public repo, deployed to GitHub Pages** by an Actions workflow from `main` (the private KB submodule is never fetched by CI). The owner enables Settings → Pages → Source: GitHub Actions (said yes, 2026-10-30). Rights findings and any concern: `docs/rights.md`, stated once. | owner | 2026-10-30 |
| D4 | **Art and audio are rendered on the owner's PC's local studios** (Flux Studio, Audio Studio) through a Remote Control session; the pipelines are built and proven in the cloud first with `--dry-run`, `--mock` and a fake server (Xross Forge D18 pattern). | owner | 2026-10-30 |
| D5 | **Ten competitive decks after M7**: Standard, the best-placing recent tournament list for each of **ten different champion lineages**; sources and any swaps recorded in `docs/competitive-decks.md`. | owner | 2026-10-30 |
| D6 | **Budget: about 9M tokens** for the overnight run (M0-M7 plus the ten decks). Sonnet implements; Opus only for the rules agent and independent reviewers. | owner | 2026-10-30 |
| D7 | **IP posture (Mallet posture):** real card, champion and set names; all rules text, UI copy and lore in our own words; no publisher art, logos, icons or audio; art is our own generated depiction. Official PDFs, API dumps and card images stay in gitignored `docs/sources/`. "Unofficial, non-commercial fan project" in README and UI. | default (KB rule 3) | 2026-10-30 |
| D8 | **Scaffold from Xross Forge** (`d849223`, itself lorecannae's infrastructure): plain browser JS, no build step, no dependencies, namespace `GA`, Node 22 tools. Structure and modules only; no Xross skin (D2). Porting map: `docs/PORTING.md`. | default | 2026-10-30 |
| D9 | Authority order for rules: comprehensive rules > official FAQ / errata / rulings > other official documents > community summaries. Ambiguities are logged in `docs/rulings.md` as RULINGs and never block. | default | 2026-10-30 |
| D10 | Work happens on `claude/build`; each gated milestone fast-forwards `main`, which deploys. | default | 2026-10-30 |
| D11 | Credit **evilgouki**. Never the owner's real name or a home path in any file (pre-commit hook; patterns kept outside the repo). | owner (standing) | 2026-10-30 |

## Milestones

| | Milestone | Where | State |
|---|---|---|---|
| M0 | Hygiene, KB submodule, sources, rules primer, rights, card fetch, decklists, scaffold, porting map | cloud | in progress |
| M1 | Card data for the four starters: schema, build, our-words text, validation (mutation self-test), `defects.js`, art and sound manifests declared empty and failing | cloud | |
| M2 | Engine: frozen contract `docs/ENGINE-API.md` first; pure `apply`/`legalActions`, seeded RNG, one door per rule, `view(state, seat)`, one behaviour test per card, auditor, sim with invariants, replay; independent rules review | cloud | |
| M3 | Playable on Pages vs a random bot, in the D2 look: every public zone viewable, hover zoom, prompts that say what they decide, why-not, presentation director, how to play, deck picker | cloud | |
| M4 | AI (worker, tiers): beats random ≥ 95% in both seats on holdout seeds; scored against do-nothing; empty-turn, missed-lethal, level-up and fallback counters | cloud | |
| M5 | Art: audition, one STYLE, identity table, every card face, card backs, board, title | cloud pipeline, rendered on the owner's PC (D4) | |
| M6 | Audio: SFX on log tags, music scenes, `sounds.html` | cloud pipeline, rendered on the owner's PC (D4) | |
| M7 | Polish: phone/touch, save/continue, settings, bug report, end screen | cloud | |
| C | Ten competitive decks (D5) | cloud | |

## Cut order (if the run runs short)
Cut first: tutorial depth, music tiers beyond calm/tense/victory/defeat, deck-builder polish,
spectate controls. **Never cut:** per-card behaviour tests, the defects gate, open-information
viewers, the log, prompts that say what they are about, the rulings log.
