# notes.md — 2026-09-29-suite-merge-001

Five files, all three pieces of the brief in one response. Four are
inside the forecast (`nisaba-seed.md`, `registers/README.md`,
`registers/queue-protocols.md`, `registers/ledger-protocols.md`); one is
not, below. No probe, no light block, no clarification round. Both
context tarballs matched the brief's description (MASTER.md 12,476
lines, headings at 1/22/44/133/5622/8714/9729/12038/12461; office-src's
doctrine, catalogs and templates present). No compaction.

## Out of forecast: one path

- **`blueprints/drafting-table.md`** (created, new top-level directory).
  The goal's third piece is this file: office-src's design for the
  drafting-table, which the brief places in a new `blueprints/`
  directory the forecast could not name. Nothing else lands outside
  `nisaba-seed.md` and `registers/`. Also recorded in the manifest's
  `forecast_departures`.

A doc-inventory note, since DOCS.md §1 says not to invent categories
silently: nisaba-src has no `claude/` tree and no `INDEX.md`, and a
design blueprint for another repo fits no DOCS.md category cleanly (an
explainer is the nearest). I followed the brief's path and name, and
listed it in `registers/README.md`'s file list so it is findable from
the registers it derives from. If nisaba-src grows an INDEX, this is
one of its first entries.

## What to look at closely

**1. I changed two ledger anchors.** The ratified grammar is the
ledger audit's, but two of its own cells broke it: "In-place amendment
of an earlier ruling" had a second place that was prose ("6 dated
markers (…)"), and "Citation of evidence by number" had prose after its
range (", cited from every section"). Both now parse; the prose moved
into the note, and the first gained the three line numbers of the
markers that fall outside L8801–8816 (L8936, L9318, L9564), found in
the copy. No other ledger cell changed; `validation.sh` proves it by
reversal. The brief said "anchors only" of the queue register and did
not say the ledger was frozen; I read "both registers parse under it"
as licensing this. Revert both and loosen the grammar if you'd rather.

**2. The grammar is stricter than either audit's validator** in one
way: each range must lie inside the lines its token covers (`§3 L5650`
fails), which is why `registers/README.md` carries the named copy's
token table. Both registers passed it without a change beyond (1).
Other pins you may want to argue with: `, ` separates ranges within a
place and `; ` separates places; a later place may drop its token and
inherit; a note is one balanced parenthetical at the end of a place.

**3. Queue anchors.** Every one of the 38 rows changed; the recast
ones keep the audit's own line numbers. Where a cell named rows,
watches or phrases with no lines, I parsed ranges from the copy: row
spans run from the row's header to its last non-blank line; "(Rider
item N.)" and "Sequencing for the next desk" and "close recorded by"
occurrences are grep hits (examples, marked as such); three rows
("Dated bracket annotation", "Bracket verb vocabulary",
"Cross-reference pointer grammar") anchor to whole sections because
the protocol is spread through them. Each register's preamble gained
one dated paragraph saying what was normalized; no row's other cells
moved.

**4. Seed.** Pure insertions, 45 + 7 + 43 + 7 lines, nothing else
touched: the §6 note between the table and the extraction plan, the
dated answer beneath Q-4, Q-10 to Q-14 after Q-9, and the §10 line
beneath the road. I did not annotate any N-entry; none needed it. The
quotes in the §6 note are the workers' words from the brief's
Appendix B, joined across line breaks.

**5. Blueprint decisions that are mine, not the brief's** — each is
argued in the blueprint where it lands:

- *Filed means append-only* (§0 rule 1), read from OFFICE.md §15 plus
  the notepad's own practice. Everything else in the ledger design
  rests on it, and it makes the close-by-reversal check the simple
  prefix case. It is a proposed doctrine line, not a reading I can
  cite.
- *Ruling ids are `YYYY-MM-DD-slug`*, not numbers: continuity with
  MASTER.md's "§5, this date" citations, the office's date-and-slug
  identity, no counter to collide when two repos' rulings merge.
  Evidence keeps numbers.
- *`spaces.toml`'s `filed` takes a list*, as `hung` already does,
  because the drafting-table is part live, part filed.
- *`office digest` is a script, not a session kind.* This departs from
  the seed's §5 table. Everything on the page is computed, so it is
  `office survey`'s pattern. If you want the seed's session kind, it
  can sit on top of the script's page later.
- *Desk moves.* To keep a sitting's forecast to `drafting-table/` and
  `notepad/` (Q-4 as answered) while folder numbers stay minted by the
  office command alone, a sitting writes its folder decisions as data
  on `drafting-table/moves.md` and `office moves` applies them. This is
  the one piece of new machinery I'm least sure about; the alternative
  is a sitting that also forecasts `desk/`, which is simpler but gives
  the desk two writers of numbers.
- *`blueprint close` is a sitting scoped to one blueprint*, not a new
  kind.
- *Two more departures from the seed's §5 table*, both flagged in the
  blueprint: a sitting's bundles are delivered, not landed in the
  office; and `check` and `retry` are declared attended until
  twine-src gives their landings a path, because "no declared landing,
  no unattended spawn" forbids otherwise.
- Smaller calls: status collapses thirteen spellings into seven;
  ratification of judgment calls is per session, not per call; no
  implicit "stands as shipped" default; no bucket rows; eye-watches
  untouched for three sittings are flagged.

**6. The four missing watch data.** The queue audit named two (a HOLD
cause class for watch 15; "a real round" for watch 24). The other two
are my reading of the watch text: watch 17 needs a marker that tells a
deliberate amendment accept from an oracle override, and watch 13
needs the unused forecast entries per applied session (computable only
if telemetry records applied paths beside the forecast, which is the
ledger audit's open question too). The blueprint says so and asks for
a probe of bale's stats JSON before any slip is filed. I did not have
bale's telemetry schema, so none of the `bale stats` queries is named
past its catalog name; see `includes_missing`.

**7. An independent read** of the finished blueprint, by a separate
agent against the brief, found no missing section items but a dozen
internal contradictions, all fixed before packing. The ones that
changed the design: the append-only rule now covers filed *pages*
only, because filed folders already take lines from `office sessions`
today; the History verb `landed` is gone, since it restated bale; the
desk no longer orders by decomposition-line order, only by gates; and
the landing order now puts the read side (session 3) before the verbs
(session 4), whose desk, one-writer rule and watches check all read
the registry. Two queue anchors were also harmonized with the audit's
own spans for the same rows (rows 45 and 104).

## Reading, for the record

manifest.json; AGENT.md core; README.md (the brief); the seed and the
three register files; TARBALL.md §1, §2, §5 (skipping 5.6–5.10), §7,
§10.1; DOCS.md whole (documentation is the work); OFFICE.md whole; the
three catalogs and eight templates. MASTER.md for spot-checks only:
the headings, the header, the 25 watch bullets' first lines, the seven
machine-evaluable watches read whole (about 100 lines, to name their
data), §4's row headers by parsing, and greps for the phrases the
queue anchors cite. CODE.md and PLANNER.md were not read; nothing here
authors a pack or touches code layout. I read the two tools' headers
and their write paths before running them.

## validation.sh

Nine assertions, no project checks (nisaba-src has none). Run on the
tree with the change: nine PASS. Run on the request's unchanged tree:
eight FAIL, and the ninth — N1–N10 and §11 byte-identical, by
extracting each span by heading and hashing it against the request's
copy — passes on both, as a guard must; the mutation runs show it
bites. Three assertions are reversals in the ledger audit's sense:
remove the seed's declared additions (line ranges) and hash to the
request's `base_files` sha256; restore each register's declared old
anchors, drop its declared paragraph, and hash likewise.

Mutation runs, each against the changed tree: a doubled space inside
N6 fails the span check and the seed reversal; the request's queue
register under the new README fails the parse on every recast anchor;
a range pushed past §3's end fails the parse; one word changed in a
non-anchor queue cell fails the register reversal; a protocol name
dropped from the blueprint fails the name check and the trace. The
script writes only `.validation-logs/<timestamp>/` and runs python
with `-B`. Claims are `observed`.

`model_identity` is the configured identifier this surface reports
(`anthropic:claude-opus-5-5`); the surface says the serving model can
differ, and nothing attests it.

## Proposals

- **What:** File the four watch data as bale-src items, after one probe
  of `bale stats --json` (and the telemetry record schema) confirms
  which are really missing. **Why:** `office watches check` cannot
  evaluate watches 13, 15, 17 and 24 without them, and two of the four
  are my inference from the watch text, not an audit finding.
  **Scope hints:** bale-src's telemetry schema and stats verb; the
  blueprint's §3.2 table is the list. Until the Nisaba office exists,
  bale-src's own fold-in registry is where they wait.
- **What:** Give nisaba-src a small project check that parses every
  register under `registers/README.md`'s grammar (the parser in this
  session's `validation.sh`, lifted into a script the repo keeps).
  **Why:** three sessions have now each written a register parser in
  their `validation.sh`; a fourth register, or a re-anchoring to a
  later MASTER.md copy, would write it again. **Scope hints:**
  `registers/`; a new script and a line in `registers/README.md`.
- **What:** At the next sitting, rule on the blueprint's departures
  from the seed's first pass — `digest` as a script, and desk moves as
  the sitting's way to reach the desk — and annotate the seed's §5 if
  they stand. **Why:** the seed's §5 table still lists `digest` as a
  session kind; left alone, the seed and the blueprint disagree about
  it. **Scope hints:** `nisaba-seed.md` §5 (a dated note beneath the
  table); `blueprints/drafting-table.md` §3, §5.3.
