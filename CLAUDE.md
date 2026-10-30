# great-archival-forge — Grand Archive in the browser

Unofficial, non-commercial fan reproduction of the **Grand Archive TCG** (Weebs of the Shore),
played vs AI in the browser. **Decisions live in `PLAN.md` (read it first).** The shared
knowledge base from the owner's earlier ports is the submodule `docs/knowledge-base/`
(`git submodule update --init`; private): start with its `README.md` and `card-games.md`, and
update its `great-archival-forge.md` entry at the end of every milestone (KB README rule 19).

## Hard rules
1. Plain browser JS, no build step, no dependencies. Every file is an IIFE on `globalThis.GA`.
   `index.html`'s script list is the load order; `tests.html` loads the same engine files in the
   same order (`tools/check-pages.mjs`).
2. Engine surface (contract frozen in M2, `docs/ENGINE-API.md`): `GA.legalActions` /
   `GA.apply` (never mutates) / `GA.isTerminal` / `GA.whoActs` / `GA.view(state, seat)`. Every UI
   affordance derives from `legalActions`; every number the UI shows comes from an engine function.
3. One door per rule (damage, life, draw, memory/reserve payment, zone moves, level-up,
   element access, characteristics, the stack, choices). Never write a champion's damage or a
   card's zone outside its door.
4. Never assume a choice: no auto-pick for a single candidate.
5. No silent fallbacks: no `if (!GA.x)` and no `GA.x || {}` in UI code; a missing module throws.
6. Seeded RNG; every shuffle and random pick happens inside `apply`.
7. Hidden information (hand, deck order, memory, face-down cards) is only visible through
   `GA.view(state, seat)`; the sim runs a leak test.
8. A card that doesn't play as printed goes in `data/defects.js`, never quietly into a deck.
9. Cite the source in engine comments: `(CR 3.2.1)` comprehensive-rules section, `(FAQ …)`,
   `(R-012)` ruling. Tests are named for the rule or card they assert.
10. Rules text, UI copy and lore are **our own words**. Official PDFs, API dumps and card images
    stay in gitignored `docs/sources/`; never commit official art, logos or audio.
11. Art prompts never contain franchise, publisher, studio or artist names or text-magnet words
    (lint in the art pipeline, M5).
12. The look is PLAN D2 (living archive vault). Never copy a sibling's skin (palette, type,
    frames, card backs, title, motion); the donor supplies structure only.
13. Commit messages describe the mechanism by card, CR section or ruling. UI commits say what
    was checked in the real page. Commit with explicit paths while agents run
    (`git commit -m … -- <paths>`), and gate the commit in a clean worktree, not the working tree.
14. Never put the owner's real name or a home path in any file; credit **evilgouki**. Enable the
    hook once per clone: `git config core.hooksPath .githooks` (private patterns go in
    `$(git rev-parse --git-common-dir)/privacy-patterns`, never in the repo).
15. Before committing a document, `ls` every path it claims exists.
16. Agents write their hand-back summary to `tools/out/agents/<name>.md` (gitignored); read that,
    not the transcript.

## Commands
```
node tools/fetch-cards.mjs      # official card pool -> docs/sources/api (gitignored)
node tools/serve.mjs            # local server (no-store cache)
node tools/test.mjs --quiet     # headless tests (tests.html's script list under node:vm)
node tools/gate.mjs             # every gate, one line each
node tools/stamp-assets.mjs     # re-stamp index.html ?v= hashes before every deploy commit
```
