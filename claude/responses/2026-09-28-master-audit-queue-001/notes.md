# notes.md — 2026-09-28-master-audit-queue-001

One file landed, `registers/queue-protocols.md`, inside the forecast.
No probe, no light block, no clarification round; both context
tarballs matched the brief's description (MASTER.md 12,476 lines, the
headings at 133, 5622 and 8714; office-src's doctrine, catalogs and
templates present). No compaction.

## What I found that the seed did not say

The register's prose carries the corrections in full; the ones you
should read first:

1. **§4 has 133 rows.** The seed's 343 is the whole-file count of
   `^[0-9]+\. \*\*` — 133 board rows plus 210 numbered evidence
   entries in §6. Your sibling ledger audit will want that: the seed
   also gives §6 219 entries, and the header pattern finds 210, so
   either nine entries use another shape or the count is off there
   too. I did not look; it is the ledger's territory.
2. **§3 is mostly sitting-close narrative.** Of §3's 5,489 lines,
   3,645 are forty `Landed <date>, the <name> sitting …` blocks — the
   per-sitting narrative the header's going-forward convention says
   no longer accretes in §2. It accretes in §3 instead. I registered
   the blocks as `content` and the one rule they state ("this block
   carries only what has no row home") as `judgment`; the mechanical
   parts they carry (landings, claims counts, deltas, light-block
   tallies) are `bale-already` rows. The seed did not see these
   blocks at all.
3. **What/Why/Scope hints and rides/consumed are registry shapes.**
   On the board they are rare (21 labels on 9 rows; one "rides row";
   two "consumed at"). In the fold-in registry they are the norm (75
   labels; 83 "rides"; 59 "consumed"). The board row's real field set
   is number, title, status, date, a class parenthetical, a source,
   sids, and dated brackets.
4. **The fold-in registry is not the suggestion box.** OFFICE.md §5
   makes a slip a friction report; a registry entry is small work
   with a named carrier. I proposed a riders page on the
   drafting-table plus a `Riders` section in `folder.md`, and left
   the choice open. Push back if you meant the suggestion box as a
   general inbox — the doctrine as written does not read that way.
5. **The in-flight bullets are stale** (dated 2026-08-10/13 in a doc
   last landed 2026-09-24). That is the argument for rendering the
   in-flight view from bale's registry rather than writing it.
6. **The ordering paragraph is false of its own section.** "Ordering
   is the recommended sequence; small sessions first" — rows are
   appended in queue order, and sequencing lives in per-row gates
   (`after row N`, `serializes after`, `consumer S6`) and a
   "Sequencing for the next desk" line at close. Registered as a
   judgment row with the recommendation to drop the paragraph.

## Where to look closely

- **The kind column.** The README admits one of four; the seed's
  "shape + judgment", "mostly exists" and "drop (bale's docs)" do not
  fit, so the watch became five rows and "drop" became
  `bale-already`. If you would rather have compound kinds, the
  README is the file to change, and this register would follow.
- **Office homes are candidates.** Several rows name things that do
  not exist: `office watches check`, `drafting-table/watches.md`,
  `drafting-table/riders.md`, `drafting-table/rulings-pending.md`, a
  `status` / `class` / `lane` / `gate` / `waits for` / `Riders` /
  history line in `folder.md`, a `board:` id. Each is named as such.
  The existing verbs I leaned on are `office desk`, `office
  sessions`, `office open` + `office close`, `office note`, and the
  seed's `office digest` and `cleanup` kinds.
- **Bracket verbs.** The tally is over the first word after the date
  in 209 brackets; about a third open with prose. The closed set in
  the row is a proposal for the merge session, not a finding that the
  set exists.
- **Line ranges.** Every anchor is from the copy that traveled with
  the request; the register says to re-derive before trusting. The
  watch spans and the close-block line numbers were computed by
  parsing, not by eye.

## Reading discipline, for the record

The brief said ten rows whole, stop at thirty. I read rows 1–11 (the
short DONE shapes and the two long early ones), 37, 41, 45, 67, 73
(head), 104 (head) and 129–133 — nineteen rows, eight of them the
one-to-three-line DONE pointers — plus the 25 watches, the ruling
queue, two runs of registry entries (397–469, 1107–1180) and three
close blocks (2029–2058, 2688–2765, 5509–5621). Everything else was
grep, awk and a short Python profile over the bullets and headers.
The counts in the register's last section came from those passes.

## validation.sh

Three session-specific assertions, no project checks (nisaba-src has
none): the stub is gone; the register parses (one table, the README's
seven columns, every row seven cells, kind in the four, every anchor a
heading or a `lines NNN–NNN` run inside §3 or §4, unique protocol
names, at least twenty rows, the brief's minimum protocols present, no
second table); and the header agrees cell for cell with the README's
column table. Run on the tree with the change: three PASS. Run on the
unmodified tree (the stub): three FAIL. A mutation run (one kind set to
`mixed`, one stray `|`) fails the parse naming both. The claims
reconciliation epilogue is the crafter's, pasted as emitted. The
script writes nothing.

`model_identity` is the configured identifier this surface reports
(`anthropic:claude-fable-5-1`); the surface says the serving model
can differ, and nothing attests it.

## Proposals

- **What:** Have the ledger audit re-count §6 by structure before it
  trusts the seed's 219. **Why:** the row-header pattern finds 210
  numbered entries in §6; the seed's 343 for §4 was the whole-file
  count, so the seed's counts were taken once over the file rather
  than per section. **Scope hints:** `registers/ledger-protocols.md`;
  no change to this register.
- **What:** When the merge session drafts `office watches check`,
  start from the seven machine-evaluable watches the register names
  and their `bale stats` queries, and make the missing fields (a HOLD
  cause class; "a real round") slips for bale-src. **Why:** four of
  the seven conditions need a datum bale does not stamp today; the
  seed's plan has the check reading bale stats, and a check that
  guesses at a cause class would be an office workaround of a bale
  gap (OFFICE.md §10). **Scope hints:** office-src's drafting-table
  blueprint; bale-src's telemetry schema, only after the merge names
  the fields.
- **What:** Decide Q-4 (sittings write to the office directly) before
  the merge session, or let the merge session carry it as its first
  ruling. **Why:** two rows here ("The close is a session", "Sitting-
  close block") resolve differently depending on it — with Q-4 yes,
  the nineteen-session close ceremony retires and the blocks become
  notepad pages plus cleanup; with Q-4 no, the close session stays and
  needs a home on the drafting-table. **Scope hints:** nisaba-seed.md
  §8; no file in this register.
