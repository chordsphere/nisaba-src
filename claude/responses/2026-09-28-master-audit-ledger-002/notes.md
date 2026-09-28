# notes.md — 2026-09-28-master-audit-ledger-002

One file landed, inside the forecast: `registers/ledger-protocols.md`,
39 rows. Both context tarballs matched the brief's description to the
line (12,476 lines; headings at 1/22/44/133/5622/8714/9729/12038/12461;
36 `New, ratified` blocks; entries 10–219 numbered, 1–9 as a
paragraph), so no probe was needed. No light block, no clarification.

## What I read, and how far

Header, §1, §2 and §8 whole. §5, §6 and §7 by grep and sed: the block
openers, the bullet leads, the batch headers, the citation forms, the
dated markers, the bullet openers of §7. Entries and rulings read whole:
the first two §5 blocks (2026-07-13, 07-15) and the openers of
2026-08-16, 2026-09-14, 2026-09-22 and 2026-09-23/24; §6 entries 10–15
and the neighborhood of 99 and 143–145; about a dozen §7 bullets. Well
under the brief's thirty-entry ceiling. Everything else in the register
is a count or a pattern, and the counts are in the register's preamble
so the merge can re-derive them.

## Where the seed's table was wrong

Said in the register's prose too; the short form:

- **§6 is not append-only at the body level.** Nineteen dated
  `[YYYY-MM-DD: …]` appendices and eleven running occurrence counts
  are written into entries at later sittings. Numbers are append-only.
  This matters for the office because §15 forbids exactly that edit;
  an occurrence has to be a new record that points at the entry.
- **Condensation reached the ledgers.** §5 opens with a `Carried
  forward:` paragraph of pre-v4 rulings with no dates and no sources;
  §6's entries 1–9 are one paragraph. The seed only had §2 condensing.
  This is the strongest concrete argument for "never condense" the
  audit found, and the provenance is recoverable only from v3 in git.
- **§7 is a third environment facts.** The rest is version landmarks
  (bale-already) and desk-practice rules that accreted there — include
  rules, forecast rules, dispatch checks, "one-apply-behind held for"
  instances. Registered as content with project-facing homes.
- **Rulings have no ids.** 117 bold leads, cited by name in prose. The
  seed's `amendment_target` for exchange answers has nothing stable to
  point at until they do.
- **§8's dispositions are edited in place** (finding 1b carries an ADR
  status dated three weeks after the register). A filed page cannot do
  that; the read side derives it.

## Things I want you to look at

- **The anchor grammar.** The brief said "a heading or a line range";
  I fixed it as `header`/`§N` plus `L<start>–<end>` ranges, `;`-separated
  when a protocol shows in several places, and `validation.sh` enforces
  that. If the queue audit picked a different grammar, the merge will
  want them aligned; the README could pin it.
- **The close-by-reversal row.** It is written in §5 as close practice,
  not as a ledger rule, but it is the one MASTER.md protocol already
  running as code (a close's `validation.sh` hashes back to
  `provenance.base_files`). I registered it because it is the office's
  §15 for sessions, and the cheapest thing to inherit.
- **Kind for the condensation row.** I kept `shape` per the README's
  vocabulary and put "office's rule is stronger, home is none" in the
  cells, as the seed's row did. If the merge would rather see such rows
  as `content` (nothing to build), that is a one-word change per row.
- **One anchor outside my sections:** the lift row cites `§4 L5857`,
  the board's `[2026-08-16: lifted to §5.]` note, as the other end of
  the lifecycle. Reference only; the queue audit owns that side.

## Validation

`validation.sh` parses the register (header equals the README's seven
columns; separator; every row seven cells, none empty; `kind` in the
four values; anchor opens with a heading token; every `L` range inside
1..12476 and not reversed), asserts ≥ 20 rows with unique protocol
names, and asserts the stub is gone and the `## The register` section
exists. Rehearsed on the changed tree (all pass) and on the request's
stub (the three change-assertions fail, as they should). A fourth check,
"registers/README.md lists ledger-protocols.md", passed on both trees,
so I dropped it per TARBALL.md §7.2; the README-column agreement lives
inside the parse check instead. Claims are `observed`.

## Proposals

- **What:** pin the register anchor grammar in `registers/README.md`
  (heading token plus `L<start>–<end>` ranges of a named copy) so both
  registers and the merge parse the same way.
  **Why:** the brief left it open, and the two audits ran side by side
  with no way to agree; a validator per register that disagrees on the
  anchor shape is friction the merge would absorb.
  **Scope hints:** `registers/README.md`; after both registers land.
- **What:** give §5 rulings stable ids before the drafting-table's
  rulings ledger is designed (a number like §6's, or `<date>/<slug>`).
  **Why:** the seed wants exchange answers to name an
  `amendment_target`, and supersession and amendment both point at
  rulings today by prose name only.
  **Scope hints:** the merge session's blueprint; no change to
  MASTER.md.
- **What:** treat the close-by-reversal check as an office check on
  every ledger write, whichever verb does the writing.
  **Why:** it already exists as code in bale-src's closes and it is
  OFFICE.md §15 restated for sessions; inheriting it costs one
  `validation.sh` fragment.
  **Scope hints:** office-src, after the drafting-table exists; depends
  on Q-4 (whether sittings write the ledgers directly).
