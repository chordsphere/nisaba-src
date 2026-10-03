# The drafting-table — a blueprint for office-src

The design office-src builds the drafting-table from: the space, the
desk's new fields, the verbs, the read side, the sitting kind, and the
three new verb-table columns. It is the merge nisaba-seed.md §6 and §10
call for, derived from the two protocol registers under `registers/`.

Provenance: written by `2026-09-29-suite-merge-001`, packed from
nisaba-src, from `registers/queue-protocols.md` (landed by
`2026-09-28-master-audit-queue-001`) and `registers/ledger-protocols.md`
(landed by `2026-09-28-master-audit-ledger-002`), under the seed's N3,
N7 and N9 and its §8 answers Q-4, Q-10 and Q-11, answered 2026-09-29.
Where this document and the seed disagree, the seed is the ruling and
this document is the defect; where it departs from the seed's first
pass on purpose, it says so in the line that departs.

**Who this is for.** office-src's worker, reading it as context beside
`doctrine/OFFICE.md`, `share/spaces.toml`, `share/verbs.toml` and
`templates/` (office-src 0.2.0). OFFICE.md is cited by section; the
registers by protocol name, in quotes, tagged *(queue)* or *(ledger)*.
Everything named here that office-src 0.2.0 does not have is marked
*new*. Nothing in this document is built, and it moves no MASTER.md
content: content moves after the verbs exist, by office sessions
(seed N3, §10 step 5).

**How the registers were merged.** Every `shape` row has a home in
§1–§6 or a deferral in §7. Every `judgment` row has a doctrine line, a
house rule, or a deferral. `bale-already` and `content` rows are listed
as such, and nothing is built for them. Appendix A traces every row of
both registers to the place that disposes it.

## 0. Four rules the design rests on

Each of these is argued once here and cited from the sections below.

1. **Filed means append-only.** A filed page grows at its end; the bytes
   already there never change. That is how OFFICE.md §15 already works
   for the notepad (`office note` appends a line to the day's page), and
   it is exactly what MASTER.md broke four times: condensation at
   regeneration, in-place amendment of rulings, in-place accretion on
   evidence entries, and in-place disposition updates ("Condensation at
   regeneration", "In-place amendment of an earlier ruling", "In-place
   accretion on an entry", "Dispositions updated in place", all
   *(ledger)*). Under this rule each of those becomes a new record that
   points back, and the read side renders the current state. Proposed
   doctrine line for OFFICE.md §15: *"Appending is not rewriting: a filed
   page grows at its end, and the bytes already filed never change."*
   The rule is for filed *pages* — the drafting-table's ledgers, close
   reports and the notepad. A filed *folder* in the filing cabinet keeps
   §15 as office-src applies it today: it moves whole, and only the
   office command adds lines inside its sections (`office sessions`
   already writes `filing-cabinet/{folder}/folder.md`), which a byte
   prefix cannot express and this blueprint does not change.
2. **Render bale's records; never write them.** What bale records
   (sids, outcomes, claims, versions, rounds, landings) is read and
   rendered, never restated by hand (OFFICE.md §10; §4 below). Nine
   `bale-already` rows in the registers (five queue, four ledger) are
   MASTER.md restating bale by hand.
3. **One home per fact, cited by id.** A fact lands once, in the folder,
   blueprint or ledger record it belongs to; everything else cites it
   by an id from §1's citation grammar ("One-home rule for facts of
   record" *(queue)*; "One-home pointers and "recorded once""
   *(ledger)*). OFFICE.md §5 already says this of the handbook ("a
   chapter points at it rather than restating it"); the doctrine line
   extends it to the drafting-table.
4. **Data, not prose, for anything a verb reads.** Status, gates,
   carriers, watch thresholds and sources are field lines with closed
   vocabularies. MASTER.md's ordering paragraph is false of the section
   it heads ("Board ordering and sequencing" *(queue)*) because it was
   prose describing what the data should have said.

---

## 1. The space

`drafting-table/` is already in the catalog (`share/spaces.toml`,
OFFICE.md §5: "blueprints for work too big for one folder"; a
renovation space, not base). This blueprint gives it contents. In an
office it looks like this:

```
drafting-table/
  README.md             the front page: what lives here, the id forms (§1.7)
  blueprints/
    YYYY-MM-DD-slug/
      blueprint.md      one arc: charter, decomposition, watch list, history
      close.md          the arc's close report, written once at close
  agenda.md             rulings awaiting a sitting
  rulings.md            the rulings ledger
  evidence.md           the evidence ledger
  watches.md            the watches register, one entry per watch
  watch-log.md          every firing, re-arm and closure, one record each
  riders.md             riders with no carrier yet
  moves.md              desk moves a sitting decided, for `office moves`
  digest.md             the sitting-open page, rewritten by `office digest`
```

In `spaces.toml`'s terms, item by item:

| item | base | hung | filed | why |
|---|---|---|---|---|
| the space as a whole | no (renovation) | no | a list (below) | Not every session in the office needs it: a sitting ships it by verb, `office digest` reads it, and a build never ships it ("MASTER.md's own include rule" *(ledger)*: master context, not worker context) |
| `blueprints/*/blueprint.md` | — | no | no | Live until the arc closes; its charter freezes at ratification (§1.1) |
| `blueprints/*/close.md` | — | no | yes | Written once, at close; the arc's summary of record |
| `agenda.md` | — | no | no | Live: items leave when a ruling disposes them |
| `rulings.md` | — | no | yes | Append-only ledger (§0 rule 1) |
| `evidence.md` | — | no | yes | Append-only ledger |
| `watches.md` | — | no | no | Live register; its history is the log |
| `watch-log.md` | — | no | yes | Append-only; every event a new record |
| `riders.md` | — | no | no | Live: a rider leaves the page when a folder carries it |
| `moves.md` | — | no | no | Live: a move is marked applied by the script that applies it |
| `digest.md` | — | no | no | Derived; overwritten every run, never edited by hand, like `floor-plan/survey.md` (OFFICE.md §13) |

**Catalog change (*new*).** `filed` today is a boolean per space. The
drafting-table is the first space that is part live, part filed, so
`filed` takes the same two shapes `hung` already takes: `true` for the
whole space, or a list of paths inside it —

```toml
[spaces.drafting-table]
path = "drafting-table"
filed = ["drafting-table/rulings.md", "drafting-table/evidence.md",
         "drafting-table/watch-log.md", "drafting-table/blueprints/*/close.md"]
```

— and `office upgrade`'s filed-paper check (OFFICE.md §15) reads the
list. The release is additive: an office without a drafting-table has
nothing to read, and the tool never refuses an office for lacking
something optional (OFFICE.md §14).

### 1.1 Blueprints — one arc each

A blueprint is work too big for one folder: an arc of several
sessions and folders ("Arc row and its close report" *(queue)*). Each
lives in its own directory, `drafting-table/blueprints/YYYY-MM-DD-slug/`,
named the way folders are (OFFICE.md §5); the directory name is its id,
cited as `blueprint YYYY-MM-DD-slug`. Template `templates/blueprint.md`
(*new*):

```markdown
# {{title}}

## Charter

What the arc is for and what done means, in the asker's words where
there are words to keep.

- ratified: YYYY-MM-DD, words at notepad/YYYY-MM-DD-slug.md (or a sid)

## Decomposition

One line per piece of work: its one-line goal, and the folder that
carries it once the folder exists.

- the verbs over the new fields → folder 141
- the read side over bale's registry → (new; opened by `office moves`)

## Ordering and dependencies

Rendered, never written: `office desk --blueprint ID` prints the
order from the gates on the member folders (§2.3).

## Watch list

Watches scoped to this arc, by id (entries in watches.md whose scope is
this blueprint).

## History

- YYYY-MM-DD drafted: sitting sid
- YYYY-MM-DD ratified: notepad/YYYY-MM-DD-slug.md
```

- **Charter and its ratified flag.** The `ratified:` line is the
  blueprint-level form of MASTER.md §1's "do not re-litigate" marker
  ("Ratified — do not re-litigate marker on the charter" *(ledger)*).
  Once it is written, the charter section's bytes do not change;
  `office status` checks that against git from the ratifying commit
  on. A charter that must change is a new blueprint whose history
  opens `supersedes: blueprint ID`. The office's own charter stays the
  profile's Purpose (`share/profile-shape.toml`); a project's charter
  is a ratified blueprint charter, and a copy of PLANNER.md §10's floor
  is never made — point, do not copy.
- **Decomposition.** Written by the sitting that drafts the arc. A line
  for work that has no folder yet is a desk move (§5.3); `office moves`
  opens the folder and writes its number onto the line.
- **Ordering and dependencies.** Gates live on the member folders and
  nowhere else (§2.3). The blueprint renders them; it never states them,
  so it cannot contradict them.
- **Watch list.** One watch shape, two scopes: an arc's watch list
  (MASTER.md row 45's five items) is the same entry as a standing
  watch, with `scope: blueprint ID` (§1.4).
- **The close report**, `close.md`, template `templates/close-report.md`
  (*new*), written once by the sitting that closes the arc and filed:

```markdown
# Close: {{title}}

- blueprint: YYYY-MM-DD-slug, closed YYYY-MM-DD by sid

## Partition

- landed: folder N (sids), ...
- ratified: ruling YYYY-MM-DD-slug, ...
- escalated: agenda N, ...
- on watch: watch WN, ...

## Claims

The arc's sessions' claims beside their verdicts, as the read side
renders them at close, with any count the report states printed beside
the records' count; where they part, the records stand and the
difference is written down here.

## Scope

Each decomposition line: consumed (sids) or deferred (to folder N,
rider N, or nothing, with why).

## Residual

The paragraph MASTER.md §2 kept per arc: what stays true after the arc,
in plain words. The arc's folders go to the filing cabinet whole; this
is the only summary.

## Findings

Audit arcs only: | id | finding | disposition |, each disposition a
pointer (folder N, ruling ID, ADR-NNNN, a sid, evidence N).

## Proposals

Every Proposal the arc's workers raised, each with its disposition:
consumed (sid), carried (folder N or rider N), stands as shipped, or
declined — one line each, no default.
```

  The Partition, Claims, Scope and Proposals sections are the upward
  report's shape (the seed's "Upward report" row). The Residual is
  "Per-arc residual summary" *(ledger)*. Findings is MASTER.md §8's
  table ("Findings register table", "Disposition vocabulary and split
  dispositions" *(ledger)*): an audit is an arc, so its findings sheet
  is its close report, filed at close; a disposition's later state is
  never edited in — the read side follows the pointer ("Dispositions
  updated in place" *(ledger)*). The Proposals section answers "Dispositions
  entry, "stands as shipped"" *(queue)*: the default survives as an
  explicit value, never as silence.
- **Closed blueprints stay on the drafting-table.** Nothing condenses
  ("Condensation at regeneration" *(ledger)*: home none; OFFICE.md §15
  is stronger). `office` and `office digest` show open blueprints only;
  a blueprint is closed when its `close.md` exists.

### 1.2 The rulings ledger — `rulings.md`, filed

One record per ruling, appended ("Ruling block: date and source",
"Ruling naming" *(ledger)*). A record (the values are illustrative):

```markdown
## 2026-09-29-kind-vocabulary

- ruled: 2026-09-29
- source: light block 2026-09-28-open-discussion-001 [2]
- words: notepad/2026-09-29-suite-merge.md
- landed: registers/README.md (nisaba-src)
- grounds: evidence N, folder N
- supersedes: YYYY-MM-DD-slug (scope: in words, how far)

**Keep the register's kind vocabulary at four values.** The ruling's
text, bold lead first, as MASTER.md §5 writes it today.
```

**The id: `YYYY-MM-DD-slug`, and why not a number.** The id is the
ruling's date and a short kebab slug of its bold lead, minted by the
writing session and never changed; a second ruling with the same slug
on the same day takes `-2`. Four reasons, in order of weight:

1. It is the citation MASTER.md already uses. Rulings are cited today
   as "§5, this date" ("Cross-reference pointer grammar" *(queue)*); a
   date-led id keeps every existing citation one step from resolving,
   where a number would need a lookup table for 117 rulings.
2. It is the office's identity form. Folders are named by date and
   slug (OFFICE.md §5), and so are sitting pages on the notepad; one
   identity shape across the office means one parser.
3. It needs no counter. The Nisaba office will file rulings from more
   than one stream (bale-src's MASTER.md §5, office-src's own
   sittings); a sequence would collide at the merge, a date and slug
   will not.

   [2026-10-02: "the Nisaba office" here is the home office,
   `~/home-office`, founded 2026-09-30; see the annotation beneath
   `nisaba-seed.md` N8.]

4. It reads in prose. "ruling 2026-08-31-no-packaging-trio" says when
   and what; "ruling 118" says neither. (That id is illustrative: the
   ruling that closed MASTER.md's forecast-precision watch, as it
   might be minted when §5's content is filed.)

Evidence keeps numbers (§1.3) for the opposite reason: 200-odd
existing citations use them.

- **`source`** — a closed vocabulary: a sid; `notepad/…` (words said in
  a sitting or through `office note`); `light block SID [n]` (an
  answer to a worker's light question block, "as assumed" included —
  "Rulings sourced from a light-block reply" *(ledger)*); `brief of
  SID` (a ruling transported in a request's brief, as this session's
  three were).
- **`words`** — the notepad page carrying the occupant's words
  verbatim. The ledger never quotes; the notepad files every sitting's
  words whole (OFFICE.md §5, Notepad), which is stronger than
  MASTER.md's selective VERBATIM marks ("Verbatim capture of the
  operator's words" *(ledger)*).
- **`landed`** — where the ruling took effect: a folder, a sid, or a
  project path and section ("Landing pointer on a ruling" *(ledger)*).
- **`grounds`** — evidence numbers, ADRs, folders ("Grounding citations
  on a ruling" *(ledger)*).
- **`supersedes`** — a ruling id and the scope in words ("Scoped
  supersession" *(ledger)*). The superseded record is never touched;
  the back-pointer is derived by the read side, never written.
- **Amendments** are records too: a record with `amends: ID`, its own
  id minted on its own date, and the amending text. The ruling as
  first minted is never edited ("In-place amendment of an earlier
  ruling" *(ledger)*). `office rulings ID` renders the ruling with its
  amendments in date order and any supersession.
- **What an exchange answer's `amendment_target` points at**: the id
  of a ruling *as first minted* — never an amendment record's id —
  so every amendment of one ruling is found under one key. When the
  planner's answer in an exchange amends a ruling, the sitting that
  receives it appends the `amends:` record and its `source` names the
  exchange round (`SID round N`). If bale's exchange record has no
  field that carries the target, the target lives on the office's
  record alone; that is not a bale-src slip, because what a ruling is
  belongs to the job, not the session (OFFICE.md §10's test).
- **Derivation into doctrine** is an `amends:`-free record kind,
  `derived-into: project path §N`, appended when a ruling's text lands
  in a project doc; the ruling stays ("Derivation into doctrine leaves
  the entry" *(ledger)* — the same rule, for rulings as for evidence).

Who writes it: sittings only (§5). Scripts read it (`office rulings`).
No cleanup session and no script mints a ruling: a ruling is judgment.

### 1.3 The evidence ledger — `evidence.md`, filed

Numbered, append-only, cited by number ("Evidence entry identity and
shape" *(ledger)*). A record is an entry or an occurrence:

```markdown
## 220. Title, as a sentence.

- filed: 2026-10-02 by 2026-10-02-sitting-001
- from: 2026-10-01-board-141-riders-003

Body: what happened, what it shows.

## 13 · occurrence — 2026-10-03

- from: 2026-10-03-retry-002
- attributed-to: planner

What recurred, in a line or two.
```

- **Numbers** are the identity: monotonic, never reused, never
  renumbered. bale-src's pile keeps 10–219 and entries 1–9 get their
  numbers back when content is filed (§7); the next entry is 220.
- **Provenance is per record** (`filed:`), not per batch: a batch
  header is lost the moment an entry is cited alone ("Batch provenance
  header" *(ledger)*).
- **Admission.** An entry names at least one session (`from:` a sid) or
  a notepad page — "earned from live traffic" ("Admission: earned from
  live traffic" *(ledger)*). Doctrine line for the evidence ledger, and
  the writing check refuses a record without one.
- **Occurrences are new records** pointing at the entry, never text
  added to it ("In-place accretion on an entry" *(ledger)*), with
  `attributed-to` from bale's role vocabulary: planner, worker,
  operator, courier ("Occurrence attribution" *(ledger)*, TARBALL.md
  §1's roles). The read side counts them; the three-same-class-events
  threshold is a watch over those counts (§1.4).
- **Derivation** appends `## 13 · derived — DATE` with `into: project
  path §N` ("Derivation into doctrine leaves the entry" *(ledger)*).
- **Citation** is `evidence N`, one spelling ("Citation of evidence by
  number" *(ledger)*). Filed MASTER.md content keeps its `§6 entry N`
  spelling forever; the read side resolves both.

### 1.4 The watches register — `watches.md` live, `watch-log.md` filed

A watch is a named re-trigger with no work attached ("Watch entry
shape" *(queue)*). One entry per watch on `watches.md`:

```markdown
## W13 — Forecast precision

- source: 2026-08-07-board-13b-epoch-ledger-005 (notes)
- scope: office
- condition: unused forecast entries, packer-side, accruing
- evaluates: query unused-forecast-entries
- threshold: 3
- re-trigger: three accruals since the last fired record

What is known, in prose.
```

- **Fields.** `source` is required: a sid, a close report path, a
  notepad page ("Watch provenance" *(queue)*: 17 of 25 carry it today,
  the field makes it uniform). `scope` is `office` or `blueprint ID`.
  `evaluates` is `query NAME` for a condition a script can compute or
  `eye` for one someone has to notice ("Watch condition,
  machine-evaluable" and "Watch condition, judgment" *(queue)*).
  `re-trigger` may be `none` for a watch kept for its record.
- **The ids** are `W1`, `W2`, …, minted in order, never reused.
- **State is never edited into the entry.** Every event is a record on
  `watch-log.md`:

```markdown
- 2026-09-10 W15 fired: evidence 109; 2026-09-01 sitting's three fixture defects
- 2026-09-10 W15 re-armed: same threshold
- 2026-08-31 W13 closed: ruling 2026-08-31-no-packaging-trio
```

  (MASTER.md's own events, with illustrative ids.) The verb set is
  closed: `opened`, `fired`, `not-fired`, `re-armed`,
  `reworded`, `closed` ("Watch firing history" *(queue)*). A `fired`
  line names its evidence (a sid or `evidence N`). A watch that fired
  in a shape its condition did not name gets a `fired` line and then a
  `reworded` line carrying the old condition verbatim, while the entry
  takes the new wording — the one live edit an entry allows, and the
  log keeps what it replaced (the open question on watch 25). A
  `closed` line names the ruling that disposed it ("Watch closure in
  place" *(queue)*); the entry stays on the page, and `office watches`
  lists open watches unless asked for all.
- **Observation-only watches are not watches.** Watches 21 and 22 have
  no re-trigger and no action; they become standing lines of the digest
  (§3.1), computed from the same query catalog ("Observation watch, no
  action attached" *(queue)*).
- **Eye-watches that nobody looks at.** `office watches check` prints
  every `eye` watch as "needs an eye", with the number of sittings
  since its last log record; one untouched for three sittings (a
  profile house rule may change the number) is flagged in the digest
  (the open question on "Watch condition, judgment").

### 1.5 Riders — `riders.md` and the folder's Riders section

A rider is small work with a named carrier: the fold-in registry
("Fold-in registry, the list" *(queue)*). Its office home is ruled
(seed Q-11): a riders page on the drafting-table for riders with no
carrier yet, plus a `Riders` section in `folder.md` for riders a
folder's next session carries — not the suggestion box, which stays
friction slips (OFFICE.md §5).

**One home at a time.** A rider is on the page or in exactly one
folder. `office rider carry N --folder M` moves its text into the
folder and leaves one pointer line on the page (`- rider N → folder
M`); a pointer is not a copy. That answers the register's open
question without two homes.

A rider (*new* shape; "Registry entry shape" *(queue)*; values
illustrative):

```markdown
### rider N — the title, as the registry writes it

- source: proposal SID #n
- rides: bin/bale_pack.py
- status: queued

Text verbatim from the source, when the source is a worker's Proposal.

- YYYY-MM-DD queued: from the proposal above
```

- **`rides`** is either a path glob ("rides the next `bin/bale_pack.py`
  touch") or `folder N`. A path carrier is matchable: `office riders
  --forecast PATH…` lists the riders whose glob a pack's forecast
  touches, so the pack line can carry them.
- **Status** is a closed vocabulary: `queued`, `carried` (by folder N),
  `consumed` (at a sid), `moot`, `stands` ("Rider lifecycle: rides →
  carrier → consumed" *(queue)*). Each change is a dated line under the
  rider. A rider in a folder whose folder is `done` with no `consumed`
  line is an orphan; `office desk` reports orphans on every walk-in —
  cheap, and the one place the occupant already looks.
- **Verbatim carry.** When the source is a Proposal, the rider's body
  is the Proposal's What / Why / Scope hints, byte for byte ("Verbatim
  carry from Proposals" *(queue)*; "What / Why / Scope hints"
  *(queue)*, `bale-already` — the shape is bale's, the office keeps it
  as the rider's intake shape). Cleanup files them (§3.2), which needs
  the applied response's `notes.md` to be readable; see §7.
- **No buckets.** MASTER.md row 11's "Deferred/when-ready" bucket
  dissolves into riders, each with an `after:` gate naming its
  precondition ("Deferred / when-ready bucket" *(queue)*).

### 1.6 The agenda — `agenda.md`, live

Rulings awaiting a sitting: decisions, not work ("Ruling queue"
*(queue)*). One entry per question, numbered `agenda N`, with its source
and the folders waiting on it. A sitting that rules on it appends the
ruling to `rulings.md` and removes the entry from the agenda, leaving a
line in the agenda's own dated list at the foot of the page (`-
2026-10-02 agenda 7 → ruling 2026-10-02-riders-home`). A folder that
must wait for a decision gates on it (`after: agenda 7`, §2.3); the
register's either-or (a page, or a `decide first` status) becomes
both, each doing one job.

### 1.7 The citation grammar

One form per kind of thing, so the read side can resolve every pointer
("Cross-reference pointer grammar" *(queue)*; "Citation of evidence by
number" *(ledger)*):

| thing | cited as | resolves to |
|---|---|---|
| a folder | `folder N` | the folder whose `number:` is N, desk or cabinet |
| a blueprint | `blueprint YYYY-MM-DD-slug` | `drafting-table/blueprints/…/` |
| a ruling | `ruling YYYY-MM-DD-slug` | its record in `rulings.md` |
| an evidence entry | `evidence N` | its entry in `evidence.md` |
| a watch | `watch WN` (or `WN` in the log) | its entry in `watches.md` |
| a rider | `rider N` | the page or the folder holding it |
| an agenda item | `agenda N` | `agenda.md`, or the ruling that disposed it |
| a session | the sid, in backticks | bale's registry, per project |
| a notepad page | `notepad/…md` | the page |

MASTER.md's own forms — `row N`, `board N`, `§5, this date`, `§6 entry
N` — survive in filed MASTER.md content and nowhere new; the read side
maps them. `drafting-table/README.md` carries this table for sessions.

---

## 2. The desk's new fields

The board is the desk plus the filing cabinet, once folders carry what
a board row carries. MASTER.md's board row has, in the queue audit's
words, "number, title, status, date, a class parenthetical, a source,
sids, and dated brackets"; `folder.md` gains each as a field line, plus
the gates and the two new sections.

### 2.1 `folder.md` (*changed* template)

Below the title and the template's existing sentence, a field block;
then the existing sections; then two new ones (values illustrative):

```markdown
# {{title}}

- number: 141
- status: queued
- queued: 2026-09-29
- class: meta
- size: small
- lane: office-src: share/, templates/
- source: blueprint 2026-09-29-drafting-table
- blueprint: 2026-09-29-drafting-table
- after: folder 140
- serializes after: folder 138
- consumer: blueprint 2026-10-01-twine-courier

## Asked … ## Next      (unchanged)

## Riders

Riders this folder's next session carries (§1.5), each with its text.

## History

- 2026-09-29 queued: blueprint 2026-09-29-drafting-table, decomposition line 2
```

Field by field, with the register row each answers:

- **title** — the folder's `# {{title}}` line, as today: the board
  row's bold title without its status word, which becomes `status`.
- **`number`** — the identity ("Board row identity, not sequence"
  *(queue)*). Minted by the office command only — `office open` and
  `office moves` — as one more than the highest number on the desk
  and in the filing cabinet; never reused, never renumbered. The
  directory name stays date and slug (OFFICE.md §5); the number is the
  short citation form. MASTER.md's board rows keep 1–133 when their
  content is filed.
- **`status`** — a closed vocabulary of seven, replacing thirteen
  spellings ("Row title status vocabulary" *(queue)*):

  | status | where | reached by | MASTER.md spellings it takes |
  |---|---|---|---|
  | `candidate` | desk | `office open --candidate` | CANDIDATE, seeded |
  | `queued` | desk | `office open`, `office moves` | queued; RATIFIED, queued (the ruling goes on `source`) |
  | `open` | desk | the first sid recorded by `office sessions` | opened |
  | `done` | cabinet | `office close` | DONE; DONE at birth; CLOSED as an arc (the blueprint closes too) |
  | `absorbed` | cabinet | `office close --into N` | ABSORBED into row N; fused with N |
  | `split` | cabinet | `office close --split A,B` | cut in two (104a, 104b) |
  | `retired` | cabinet | `office close --retired "why"` | RETIRED AS MISFRAMED; RESOLVED, not a defect; struck |

  `LINKED sessions, not fused` is a relation, not a state: a `linked:
  folder N` field. `ARC` is a folder whose `blueprint:` names the arc;
  the arc's state is the blueprint's.
- **`queued`** — the date the job entered the desk.
- **`class`** — bale's work class (the request manifest's
  `work_class`), so the read side can join a folder to telemetry for
  the trust ledger (§4). **`size`** — `small`, `medium` or `high`, the
  parenthetical's size word, the desk's tie-break (§2.3). **`lane`** — the
  project and the paths, the parenthetical's lane; a folder's
  forecast in waiting ("Row header line" *(queue)*: 57 free-text shapes
  over 70 queued rows become four fields).
- **`source`** — where the job came from, in one form: `proposal SID
  #n`, `rider N`, `ruling ID`, `blueprint ID`, `notepad/…`, or a person
  (whose words go in Asked) ("Row lineage and source" *(queue)*). The
  Asked section keeps the asker's words, including a Proposal's What
  and Why; its Scope hints become the lane.
- **`blueprint`**, **`linked`** — membership and relation.
- **The gates**, §2.3.
- **Sessions** (*existing* section) — sids, one per line, as `office
  sessions` records them today, plus one `ratified` line per session
  whose worker flagged judgment calls: `- SID ratified 2026-09-30` or
  `- SID ratified 2026-09-30, except: <what was corrected, and where it
  went>` ("Ratified judgment calls list" *(queue)*). Per session, not
  per call: the calls are in the worker's `notes.md` and bale's
  `feedback.self_reported.judgment_calls`; the office records the
  planner's half only, and landing without an exception is the cheap
  default the register pointed at. Written by `office sessions
  --ratified` or by the cleanup kind (a project session such as
  `review` never writes office paper, OFFICE.md §4).
- **History** (*new* section) — the dated brackets, as lines ("Dated
  bracket annotation" *(queue)*). Appended, never rewritten; the body
  above is never rewritten either ("Queued text in git" does not happen
  — the office's rule is stronger). One event per line, `- YYYY-MM-DD
  verb: text`, the verb from a closed set ("Bracket verb vocabulary"
  *(queue)*):

  `queued`, `opened`, `ratified`, `gated`,
  `cleared`, `grown`, `re-scoped`, `corrected` (a premise corrected),
  `ruled` (a ruling now binds it), `carried` (a rider moved in),
  `consumed` (a rider consumed), `done`, `absorbed`, `split`,
  `retired`, `reopened`, and `note` — the one prose verb, so the third
  of MASTER.md's brackets that open with prose has somewhere honest to
  go.

  The status line always agrees with the last state-changing verb;
  `office status` checks it, and the state machine is: `candidate →
  queued → open → done`, any desk status `→ absorbed | split |
  retired`, `done → reopened → open`. "DONE at birth" is `office open
  … --filed --sid SID`: a folder born in the cabinet with its sid, so
  work done inside a sitting still has a citable number ("DONE at
  birth" *(queue)*).
- **Absorption, fusion, split, retirement** ("Absorption, fusion,
  split, retirement" *(queue)*) are statuses whose folder closes whole,
  with a pointer in its History (`absorbed: into folder 104`,
  `split: into folders 142, 143`); the successor gets a `note` line
  pointing back. Nothing is cut to git.
- **A DONE row's paragraph** does not exist in the office: the folder
  lists the sid and the read side renders the outcome ("DONE record: a
  pointer to the sid, not a story" *(queue)*, `bale-already`).

### 2.2 The Riders section

§1.5. Its lines move in from the page by `office rider carry`, and the
rider's status lines stay under it.

### 2.3 Gates, and what `office desk` renders

Dependencies are data on the folder that waits, and nowhere else
("Consumer and gate" *(queue)*):

- **`after: X`** — do not open this before X is done. X is `folder N`,
  `blueprint ID` (its close), `agenda N` (the MASTER.md `decide first`),
  or `ruling ID` when a ruling must exist first.
- **`serializes after: folder N`** — may run before or after N, never
  beside it (their forecasts overlap); when both are ready, N goes
  first.
- **`consumer: X`** — parked for a named consumer that will carry it: a
  blueprint, or a folder. A consumer that has no home yet (MASTER.md's
  `consumer S6`) is a drafted blueprint on the drafting-table, which
  is where "a name with no home" goes to get one.

`office desk` (*changed*) renders, in this order:

1. **In flight** — folders with a session open in bale's registry (§4),
   each with its sid and its age.
2. **Ready** — queued folders whose `after` gates are all satisfied,
   in order: by `serializes after`; then `size` (small first — the
   desk's tie-break, not a rule); then number. A blueprint's own
   sequence is expressed the same way, as `after` gates on its member
   folders; the order of its decomposition lines means nothing. A folder whose gate cleared
   since the last walk-in says so (`gate cleared: folder 61 done
   2026-10-01`).
3. **Parked** — folders grouped under what they wait for, each group
   headed by the gate's own status.
4. **Candidates**, then **orphaned riders** (§1.5) and **pending desk
   moves** (§5.3).

A gate naming nothing that exists, or a cycle among gates, prints as
an error line naming the folders; it never silently drops a folder.
There is no ordering paragraph anywhere: the recommended sequence is
the desk's output, and MASTER.md's paragraph is dropped rather than
carried ("Board ordering and sequencing" *(queue)*, a judgment row
whose doctrine line is: *the desk's order is computed from gates, and
nobody writes one*). The walk-in screen (`office` with no verb) shows
the first three Ready folders and the In-flight list.

---

## 3. The verbs

Every verb below, *new* or *changed*, with its kind, what it ships,
where it writes, and the seed's three new columns — `lands` (what is
guaranteed to exist afterward), `attended` (whether a person must be
present) and `trigger` (§6 fixes the vocabulary). Scripts ship nothing:
they run in seconds, need no session and no network (OFFICE.md §7).
A two-word verb's key in `verbs.toml` is hyphenated: `office watches
check` is `[verbs.watches-check]`.

| verb | kind | ships | writes | lands | attended | trigger |
|---|---|---|---|---|---|---|
| `digest` (*new*) | script | — | `drafting-table/digest.md` | `drafting-table/digest.md` | no | before-sitting, manual |
| `watches` (*new*) | script, read-only | — | — | — | yes | manual |
| `watches check` (*new*) | script | — | nothing; with `--record`, `drafting-table/watch-log.md` | a report; with `--record`, a `fired` record per newly fired watch | no | before-sitting, after-build, manual |
| `blueprint open` (*new*) | script | — | `drafting-table/blueprints/{id}/` | `blueprint.md` from the template | yes | manual |
| `blueprint ratify` (*new*) | script | — | `drafting-table/blueprints/{id}/blueprint.md` | the `ratified:` line and a history line | yes | manual |
| `blueprint close` (*new*) | office session: a sitting scoped to one blueprint (§5) | the blueprint, its member folders, `drafting-table/rulings.md`, `evidence.md`, `watches.md` | `drafting-table`, `notepad` | `drafting-table/blueprints/{id}/close.md`, a notepad page | yes | manual |
| `moves` (*new*) | script | — | `desk`, `filing-cabinet`, `drafting-table/moves.md`, `drafting-table/blueprints/*/blueprint.md` | every pending move applied, or a named refusal | no | after-sitting, manual |
| `rider add` (*new*) | script | — | `drafting-table/riders.md` | the rider | yes | manual |
| `rider carry` (*new*) | script | — | `drafting-table/riders.md`, `desk/{folder}/folder.md` | the rider in the folder, a pointer on the page | yes | manual |
| `rider consumed` (*new*) | script | — | `desk/{folder}/folder.md`, `filing-cabinet/{folder}/folder.md` | the rider's `consumed` line | yes | manual |
| `riders` (*new*) | script, read-only | — | — | — | yes | manual (`--forecast PATH…` when a pack line is written) |
| `agenda add` (*new*) | script | — | `drafting-table/agenda.md` | the agenda entry | yes | manual |
| `rulings` (*new*) | script, read-only | — | — | — | yes | manual |
| `evidence` (*new*) | script, read-only | — | — | — | yes | manual |
| `sitting` (*new*) | office session (§5) | `drafting-table`, `desk`, the hung items, the doctrine | `drafting-table`, `notepad` | a notepad page, `notepad/{date}-{slug}.md` | yes | manual |
| `open` (*changed*) | script | — | `desk` (`filing-cabinet` with `--filed`) | the folder with its number and fields | yes | manual |
| `desk` (*changed*) | script, read-only | — | — | — | yes | manual |
| `sessions` (*changed*) | script | — | the folder's `folder.md` | the sid line; with `--ratified`, the ratified line; with the first sid, `opened` | no | manual, after-build |
| `close`, `reopen` (*changed*) | script | — | `desk`, `filing-cabinet` | the moved folder with its status and history line | yes | manual |
| `status` (*changed*) | script, read-only | — | — | — | yes | manual |
| `cleanup` (*changed*) | office session | `desk`, `notepad`, `suggestion-box`, `handbook`, `drafting-table/riders.md`, bale's records read from the projects (§4) | as today, plus `drafting-table/riders.md` | folders' History, Sessions and Riders lines; Proposals filed as riders | no | after-build, after-sitting, schedule |

`digest` departs from the seed's §5 table, which made it a session
kind: everything the sitting-open page holds is computed, so it is a
script that writes a derived page, like `office survey`. A digest
*session* — one that reads the page and writes a "what to decide"
preface — can be declared later if the page alone proves too thin; it
would land on the agenda.

### 3.1 `office digest` — the sitting-open page

"Digest over dump": a sitting opens on one page, not on the ledgers
("Re-seed by stating progress against the doc" *(ledger)*). It writes
`drafting-table/digest.md`, overwritten every run and never edited by
hand, and prints it. Sections, each computed:

1. **Versions.** Per project, the bale version stamped on its latest
   request and on the latest landing (the provenance version check;
   "Version-position pointer" and "Version landmark" *(ledger)*,
   `bale-already`).
2. **Since the last sitting.** Sessions applied, held, bailed and still
   open per project from bale's registry and telemetry; folders moved;
   rulings, evidence records, watch-log records and riders added — from
   git and bale's records, never a hand list ("Close-time delta
   summary", "Light-block and probe ledger at close" *(queue)*,
   `bale-already`).
3. **Watches.** The digest runs `office watches check` itself (without
   `--record`) and prints its lines: fired, not fired, cannot evaluate,
   needs an eye, and eye-watches unlooked-at for three sittings (§1.4).
4. **Standing lines.** The observation queries (§1.4) and any count a
   past ruling asked to watch: predicted- against observed-basis
   claims; the HOLD rate per work class ("Observation watch, no action
   attached" *(queue)*). A number that can go stale is computed here,
   never written down ("Dated measurements, never standing counts"
   *(ledger)*: judgment; doctrine line in §4).
5. **The desk.** In flight, Ready (the first five), Parked by gate.
6. **The agenda.** Open items, oldest first.
7. **Open blueprints.** Each with its ratified flag and its member
   folders' statuses.

### 3.2 `office watches check`

It starts from the seven machine-evaluable conditions the queue
register names (MASTER.md §3 watches 1, 13, 15, 17, 21, 22 and 24;
"Watch condition, machine-evaluable" *(queue)*; seed Q-13). Five stay
watches; 21 and 22 become the digest's standing lines (§1.4), computed
from the same catalog. Watch 13 is closed (2026-08-31); its query stays
in the catalog as the precedent for the three-event calibration trigger
below (watch 13 was that trigger's first firing), and its datum is the
lowest-priority of the four slips.

**Queries are data, in the install.** A new catalog,
`share/watch-queries.toml` (*new*), names each query once: the bale
surface it reads, the value it extracts, and how it compares. A watch
entry names a query and a threshold; it never carries a command line.
The catalog is written against bale's JSON surfaces, `bale stats` and
its `--since` form first. No entry is written before the installed
bale's JSON shape has been probed (TARBALL.md §4.1: an environment
fact is probed, not guessed); that probe belongs to the read-side
session (§8, session 3), which records what it finds in the
consumption manifest (§4), and the verbs session writes the catalog
from it.

The seven, and what each needs:

| MASTER.md watch | query (catalog name) | condition | threshold | datum today |
|---|---|---|---|---|
| 1, emitter-parser drift | `unparsed-share` | unparsed reconciliation records in `bale stats --since 2026-08-01` | any non-zero share | stamped: the watch already reads it |
| 13, forecast precision (closed 2026-08-31) | `unused-forecast-entries` | forecast entries an applied session's changes did not use, packer-side | 3 accruals since the last `fired` record | **missing**: the unused entries per applied session — computable only if telemetry records the applied paths beside the forecast, the question the ledger register leaves open on "In-place "Last landed by" line" |
| 15, checkpoint-thinness HOLD clustering | `hold-cause-cluster` | HOLDs on planner-fixture defects rather than worker misunderstanding | evidence 95's "at a third" (its denominator is the entry's to state) | **missing**: a HOLD cause class |
| 17, amendment-accept stamps | `stamp-mismatch-accepts` | a HOLD-clustering read counting a deliberate `stamp_matched: false` accept as an oracle override | any | **missing**: a marker telling a deliberate amendment accept from an override |
| 21, thin predicted-basis claims | `claim-basis-split` | predicted- against observed-basis claims | none: a digest standing line | stamped: `claim_basis` |
| 22, HOLD rate per work class | `hold-rate-by-class` | HOLDs per applied session, per work class | none: a digest standing line | stamped: work class and outcome |
| 24, exchange adoption | `unrelayed-rounds` | a fourth `clarification.rounds: 0` against a real round, after MASTER.md rows 74 and 85 land | 4 | **missing**: a real round's self-report (MASTER.md row 85, queued in bale-src) |

**The four missing data are slips for bale-src**, never worked around
office-side (OFFICE.md §10: "Where bale lacks a session-shaped fact,
that is a slip for bale-src, not an office workaround"). The queue
audit named two of them (a HOLD cause class; "a real round"); the other
two are read here from the watch text and should be confirmed by the
same probe before they are filed. Until each lands, its watch stays
`evaluates: query …` with the query marked `needs: <datum>` in the
catalog, and the check prints it as "cannot evaluate: bale does not
stamp <datum> (slip)" — loudly, never as not-fired. A slip goes in the
office's suggestion box naming bale-src (OFFICE.md §5); until the
Nisaba office exists (seed N8), it goes to bale-src's own queue (its
MASTER.md fold-in registry).

[2026-10-02: "the Nisaba office" here is the home office,
`~/home-office`, founded 2026-09-30; see the annotation beneath
`nisaba-seed.md` N8.]

**Behavior.** For each open watch and each standing-line query, per
project the office scopes (§4):
a `query` watch runs its query over the window since its last `fired`
record and compares; an `eye` watch prints "needs an eye" with the
sittings since its last log record. Output is one line per watch or standing line:
`fired`, `not fired`, `cannot evaluate`, `needs an eye`, or `observed`
(a standing line's value).
With `--record` it appends a `fired` record for each newly fired watch
(never a `not-fired` record — those are a sitting's, when it wants one
on the record) and runs the filed-paper check before it commits (§5.4).
Re-arming, rewording and closing are a sitting's (§1.4). The
three-same-class-events calibration trigger from the seed's first pass
is one more catalog query over evidence occurrence counts, added the
first time a sitting wants it as a watch.

### 3.3 The blueprint verbs: open, ratify, close

- **`office blueprint open SLUG`** — makes
  `drafting-table/blueprints/YYYY-MM-DD-SLUG/blueprint.md` from the
  template, history line `drafted`. A sitting may equally write the
  directory itself; the script is for the occupant drafting alone.
- **`office blueprint ratify ID --words notepad/PAGE | --sid SID`** —
  writes the charter's `ratified:` line and a `ratified` history line;
  from then on `office status` checks the charter's bytes against the
  ratifying commit. Refuses a blueprint whose charter is empty. A
  sitting can write the same two lines itself; ratification given
  outside a sitting (an "as assumed" reply) is what the script is for.
- **`office blueprint close ID`** — prints the pack line for a sitting
  scoped to that blueprint: it ships the blueprint, its member folders
  and the close template, and lands `close.md` and the sitting's
  notepad page. Closing the member folders is `office close`, listed in
  the close report's Scope and applied as desk moves (§5.3). A close
  is judgment (the residual, the partition), so it is a session; it is
  not a new kind, because a sitting already writes the drafting-table.

### 3.4 The rider verbs

`office rider add TITLE --source SRC [--rides GLOB | --carrier folder
N]`, `office rider carry N --folder M`, `office rider consumed N SID`,
`office riders [--forecast PATH…] [--orphans]` — §1.5 gives the shapes.
Numbers are minted by the script as one more than the highest rider
number on the page and in every folder. Cleanup, a session, also adds
riders; the one-writer rule (§5.4) keeps the two from minting the same
number.

### 3.5 The rulings and evidence verbs

Read-only scripts: `office rulings [ID]` lists rulings, or renders one
with its amendments, supersessions (forward and derived back-pointers)
and the folders and sessions it landed at; `office rulings --check`
resolves every citation in the drafting-table and the desk against
§1.7's grammar and reports what does not resolve. `office evidence [N]`
does the same for the evidence ledger, with each entry's occurrence
count by attribution. Writing either ledger is a sitting's (§5); the
`amendment_target` of an exchange answer is a ruling id as first
minted (§1.2). `office agenda add TEXT --source SRC` appends an agenda
item, so a question can wait for a sitting without a session.

### 3.6 Changes to existing verbs

- **`office open`** gains the field flags (`--class`, `--size`,
  `--lane`, `--source`, `--blueprint`, `--after`, `--serializes-after`,
  `--consumer`, `--linked`), `--candidate`, and `--filed --sid SID` for
  a folder born done; it mints the number.
- **`office close`** gains `--into N`, `--split A,B`, `--retired WHY`,
  and writes the status and history lines; **`office reopen`** writes
  `reopened`.
- **`office sessions`** writes the folder's `opened` history line and
  `open` status with the first sid it records, and `--ratified [--except
  TEXT]` writes the ratified line. It never writes whether a session
  applied: that is bale's record, rendered (§4).
- **`office desk`** renders §2.3.
- **`office status`** adds three checks: filed pages are append-only
  against git (§5.4); a ratified charter is unchanged since
  ratification; every folder's status agrees with its History.

---

## 4. The read side

The office reads bale's records in its projects' repos and renders
them; it never copies them. The in-flight snapshot MASTER.md keeps by
hand was six weeks stale in a doc landed four days earlier ("In-flight
snapshot" *(queue)*) — that is the case for rendering.

**Where it reads.** The projects an office scopes are listed in
`floor-plan/manifest.toml` (*new* table `[projects]`: name and path per
project on this machine). Per project it reads bale's registry (open
sessions, sids, outcomes, admissions), telemetry records (claims,
verdicts, attempts, `work_class`, `provenance.bale_version`, feedback),
the changelog, and exchange records. It reads them through bale's JSON
surfaces (`--json`, no interactive prompt — seed §7's rule), never by
parsing `.bale/` internals, and it keeps what it reads in a consumption
manifest, `share/bale-consumption.toml` (*new*): each bale verb and
flag it calls, each JSON key it reads, and the bale version range it
was written against — twine's own pattern against bale (seed N6, D2–D4),
so a bale release that moves a key fails one office test instead of
one office walk-in. The session that builds it (§8, session 3) probes
the installed bale's surfaces first, stats included, and writes the
manifest from what it finds.
Where a datum the office needs is missing, the fix is a slip for
bale-src (OFFICE.md §10), never a scrape. A project on another machine
is the open Q-2 and is not read yet (§7).

**What it renders.**

- **In flight** — open sessions across projects, each mapped to the
  folder whose Sessions section names its sid (or listed as "no folder"
  when none does), and the open blueprints with their open folders.
  `office desk`'s first group, the walk-in screen and the digest use it.
- **A folder's sessions with outcomes** — `office sessions FOLDER`
  prints each sid with its outcome (applied, held, bailed, open,
  superseded), date, bale version, claims beside verdicts, and exchange
  rounds. The folder holds sids; everything else is rendered ("DONE
  record: a pointer to the sid, not a story" *(queue)*).
- **The trust ledger per work class** — per project and `work_class`:
  sessions applied, HOLD rate, first-attempt PASS rate, claim
  agreement, bailouts. It is the evidence a trust grant is made on (seed
  Q-6, still open); the office renders it and holds no grant here.
- **Last landed by** — for any path, the latest applied session whose
  change set held it ("In-place "Last landed by" line" *(ledger)*,
  `bale-already`). If telemetry records only the forecast, the answer is
  still derivable for ledger paths, because every session that writes
  one forecasts it.
- **The version trail** per project ("Version landmark" *(ledger)*).
- **Derived state on the drafting-table** — a ruling's amendments and
  who supersedes it; an evidence entry's occurrences; a finding's
  disposition state, followed through its pointer; a watch's state
  from its log.
- **Records beside reports** — wherever a close report or a worker's
  `notes.md` states a count the records can compute, the rendering
  prints both ("Records over reports" *(queue)*, judgment; doctrine
  line below).

**Doctrine lines for OFFICE.md** (seed Q-7, and the judgment rows the
read side serves):

- §10, after "A folder points at session ids; it never copies what bale
  records": *"The office reads bale's records and renders them.
  Reading is not copying: a rendering is derived, recomputed on every
  run, never edited, and never cited as a source — a citation names
  the sid, and the rendering is how a reader follows it. A rendering
  written to a page (the digest) is overwritten on every run, like the
  survey."*
- §10: *"Where a report and the records it summarizes part, the records
  stand, and the difference is written down, never smoothed."*
- §13: *"A number that can go stale is computed where it is shown —
  by a survey step or the digest — and never written down as a
  standing count."*

---

## 5. The sitting kind under Q-4

Q-4 is answered (seed §8, 2026-09-29): sittings write `drafting-table/`
and `notepad/` directly, and the sitting-close ceremony — nineteen
`sitting-close-deltas` sessions to date — retires ("The close is a
session" *(queue)*; "Close-recorded, not desk-recorded" and "Lift from
chat or board to §5" *(ledger)*: nothing is lifted, because the
sitting writes the ledger it rules in).

### 5.1 What a sitting is

An office session, packed from the office, forecasting
`drafting-table/` and `notepad/`. It collides with no project worker —
different repo — and with no other office session unless that session
forecasts the same paths, which bale refuses by its disjointness gate.
It is the planner's desk: it reads, decides, writes the office's
progression, and authors the bundles for the sessions it decides to
open (PLANNER.md's bundles, delivered beside their `bale open` lines).

**Ships:** the whole drafting-table (digest first, run just before the
pack line is printed), the desk (read), the hung items and the
doctrine. Never the filing cabinet wholesale; a sitting that needs a
closed folder names it.

**Lands**, always: a notepad page, `notepad/YYYY-MM-DD-slug.md`, with the
occupant's words verbatim (OFFICE.md §5; house rule 1). **Lands**, when
the sitting decides them: ruling records, evidence records, watches and
watch-log records, blueprints and close reports, agenda changes,
riders, and desk moves.

**Does not land:** the bundles it authors, and anything on the desk
directly (§5.3). The bundles are a departure from the seed's §5 table,
which lists them among a sitting's landings: a bundle is delivered
beside its `bale open` line and its brief travels in the request bale
records, so the office keeps its sid (through `office sessions` after
the pack), never a copy.

The header's "going-forward convention" ("Going-forward convention"
*(ledger)*) is the sitting verb's `writes` — `drafting-table`,
`notepad` — and a pack's forecast holds it mechanically.

### 5.2 How the sitting-close blocks become notepad pages plus cleanup

A MASTER.md sitting-close block (forty of them, 3,645 lines; "Sitting-close
block" *(queue)*, `content`) is split by what each part is, and no part
is written as a block:

| part of the block | where it goes |
|---|---|
| the sitting's words, the architect's messages | the sitting's notepad page, verbatim |
| what landed, claims counts, attempts, versions | rendered by the read side; never written |
| dispositions of the workers' Proposals | the cleanup kind, after each build lands: every Proposal filed as a rider (verbatim) or dispositioned on the folder, one line each |
| ratified judgment calls | the folder's Sessions `ratified` lines, by cleanup or `office sessions --ratified` |
| rulings made at the desk | ruling records, written by the sitting |
| evidence, occurrences | evidence records, written by the sitting |
| board and registry deltas | desk moves (§5.3) and riders |
| "Sequencing for the next desk" | gates on folders; the desk renders the order |
| light-block and probe tallies | telemetry, rendered |
| "close recorded by …" | nothing: the landing is the sitting's own sid, which bale records |

The rule each close block states, "this block carries only what has no
row home", becomes the doctrine line for the sitting and cleanup kinds
(*a fact lands once, on the folder or blueprint or ledger record it
belongs to; a sitting's page holds only the occupant's words*), with its
mechanical tell as a cleanup check: a sid cited on a notepad page and
also on a folder's History line is fine; the same fact restated in two
records is not ("One-home rule for facts of record" *(queue)*). The
note on sittings straddling midnight never needs writing: the read side
shows a sitting's span ("Expected-provenance note for sittings
straddling midnight" *(queue)*, `bale-already`).

**Goal commandeering** ("Goal commandeering on record" *(queue)*,
judgment): a sitting whose goal the occupant overrides mid-session
keeps the override words on its notepad page, and the re-ask becomes a
new folder or blueprint rather than a counted exception — AGENT.md §3's
"a fresh `bale pack`", in the office's terms. The count is a digest
line if anyone wants it, never a field.

### 5.3 Desk moves

A sitting decides things about folders — open this, gate that, retire
the other — but the desk is the office command's and cleanup's to
write, and folder numbers are minted by the office command alone. So
the sitting writes its desk decisions as data on `drafting-table/moves.md`,
one line each:

```markdown
- [ ] 2026-10-02 open "riders verbs" class=code size=small lane="office-src: bin/" blueprint=2026-09-29-drafting-table after="folder 141"
- [ ] 2026-10-02 gate folder 80 after="agenda 7"
- [ ] 2026-10-02 retire folder 57 why="premise corrected at evidence 212"
```

`office moves` applies every pending line in order through the same
code as `office open`, `office close` and the gate flags, ticks it
(`- [x] … → folder 142`), writes the minted number onto the blueprint's
decomposition line, and stops at the first line it cannot apply, naming
it. It is a script: twine runs it after a sitting's apply; offline it is
the one line the occupant runs after applying a sitting, and the walk-in
screen says "3 desk moves pending from `SID`" until it is run (house rule
4: a hand step that cannot be avoided is given as one line). This is
what replaces the nineteen close sessions: the same deltas, declared as
data by the sitting that decided them, applied by a script.

### 5.4 The close-by-reversal check, inherited

MASTER.md's closes prove their insertions by reversal: remove the
declared additions, restore any line edited in place, and hash the
result to the request's `provenance.base_files` sha256 ("Close proves
its insertions by reversal" *(ledger)*; seed Q-14). It is OFFICE.md §15
for sessions, and it becomes the office's check on every write to filed
paper, whichever verb does the writing:

- **In sessions** — a `validation.sh` fragment every session carries
  when its forecast holds a filed path (`drafting-table/rulings.md`,
  `evidence.md`, `watch-log.md`, a `close.md`, a notepad page). For a
  filed file that existed at pack time the check is the strict case of
  the reversal — additions only, all at the end: the first
  `base_size` bytes of the staged file hash to the `base_files` sha256
  the request stamped, where `base_size` is measured from the copy the
  request shipped (bale stamps the hash, not the size). A filed path the session creates needs no base.
  The fragment ships as `doctrine/checks/filed-append-only.sh` (*new*):
  the doctrine directory already rides with every office session as a
  context tarball (OFFICE.md §4), so every worker has it, and the worker
  fills in the paths, sizes and hashes from its own request, the way
  bale's crafter parameterizes its doc assertions. Live drafting-table
  pages (`watches.md`, `agenda.md`, `riders.md`, `moves.md`) may carry
  the full reversal (declared additions plus enumerated in-place edits)
  and are not required to.
- **In scripts** — `office note`, `office watches check --record` and
  any later script that appends to filed paper checks the same prefix
  in-process before it commits, and refuses on a mismatch.
- **After the fact** — `office status` walks git history for every
  filed page (the drafting-table's filed list and the notepad) and
  reports any commit whose diff does more than append at the end: the
  net for a hand edit that went through neither bale nor a script.
  Filed folders keep office-src's existing §15 check (§0 rule 1).

**The one-writer rule**, which keeps numbers unique without a counter
file: a script that mints a number or appends to a page refuses while
bale's registry shows an open session whose forecast holds that page,
and names the sid. Sessions are kept apart by bale's own disjointness
gate; scripts are kept off sessions' pages by this rule.

---

## 6. The verb-table columns

`share/verbs.toml` gains three keys per verb (seed §5, N7):

- **`lands`** — a list of paths or path patterns guaranteed to exist,
  created or changed, after the verb succeeds; each entry falls inside
  one of the verb's `writes`. `[]` means nothing is guaranteed.
- **`attended`** — `true` when a person must be present while it runs
  (answering, carrying, deciding); `false` when it can run with nobody
  there.
- **`trigger`** — a list from a closed vocabulary: `manual`,
  `before-sitting`, `after-sitting`, `after-build`, `on-hold`,
  `on-correctable-hold`, `schedule`. What a schedule is (its cadence
  and where it is declared) is left to twine-src with Q-6's trust
  grants; the office only says a verb may be scheduled.

**The rule: no declared landing, no unattended spawn.** A session-kind
verb (`office-session`, `project-session`) with `attended = false` must
have a non-empty `lands`. office-src's tests refuse a `verbs.toml` that
breaks it, `office status` reports it, and twine reads the same keys
before it spawns anything (seed N7). Scripts declare the keys too, for
parity and for the shell, but spawn nothing.

**The seed's section 5 kinds, declared** (keys shown only where new;
`sitting` and `cleanup` also appear in §3's table):

```toml
[verbs.sitting]
kind = "office-session"
built = false
ships = ["drafting-table", "desk"]
writes = ["drafting-table", "notepad"]
lands = ["notepad/{date}-{slug}.md"]
attended = true
trigger = ["manual"]

[verbs.chat]
kind = "office-session"
built = false
ships = ["desk/{folder}"]
writes = ["desk/{folder}"]
lands = ["desk/{folder}/transcript.md"]   # where it lands is Q-3, open
attended = true
trigger = ["manual"]

[verbs.cleanup]
kind = "office-session"
built = false
ships = ["desk", "notepad", "suggestion-box", "handbook", "drafting-table/riders.md"]
writes = ["desk", "filing-cabinet", "handbook", "rolodex", "calendar", "suggestion-box", "drafting-table/riders.md"]
lands = ["desk/{folder}/folder.md"]
attended = false
trigger = ["after-build", "after-sitting", "schedule"]

[verbs.blueprint-close]
kind = "office-session"   # a sitting scoped to one blueprint (§3.3)
built = false
ships = ["drafting-table/blueprints/{id}", "desk/{member folders}", "drafting-table/rulings.md", "drafting-table/evidence.md", "drafting-table/watches.md"]
writes = ["drafting-table", "notepad"]
lands = ["drafting-table/blueprints/{id}/close.md", "notepad/{date}-{slug}.md"]
attended = true
trigger = ["manual"]

[verbs.digest]
kind = "script"
built = false
writes = ["drafting-table/digest.md"]
lands = ["drafting-table/digest.md"]
attended = false
trigger = ["before-sitting", "manual"]

[verbs.review]
kind = "project-session"
built = false
ships = ["the held staging diff", "the HOLD's evidence"]
writes = ["{project}"]
lands = []        # seed: a triage record (correctable, escalate, fixture defect); twine-src places it
attended = true
trigger = ["on-hold"]

[verbs.check]
kind = "project-session"
built = false
ships = ["the landed change", "the brief"]   # never the oracle
writes = ["{project}"]
lands = []        # seed: an independent verdict as a claims block; twine-src places it
attended = true   # seed: false, once lands names a path (the rule below)
trigger = ["after-build"]                     # by policy (effort); Q-6

[verbs.retry]
kind = "project-session"
built = false
ships = ["the failure context", "the spec"]   # never oracle mechanics (PLANNER.md §5)
writes = ["{project}"]
lands = []        # seed: the corrected response, with corrects: lineage; twine-src places it
attended = true   # seed: false, once lands names a path
trigger = ["on-correctable-hold"]
```

`review`, `check` and `retry` are declared as the seed states them and
built with twine (seed §10 step 6), with one difference the rule forces:
until twine-src fixes where a triage record, a verdict and a corrected
response land, their `lands` are empty, so `check` and `retry` are
declared attended. The seed's `attended = false` for them returns the
day their `lands` name a path — the rule doing its job, not an
exception to it. The existing
verbs take the keys too: every script `attended = true`, `trigger =
["manual"]`, `lands` equal to its `writes` (`[]` for read-only ones),
except `sessions`, which twine also runs when it packs or applies
(`attended = false`, `trigger = ["manual", "after-build"]`);
`founding`, `work`, `prep`, `meeting` and `renovate` are attended, so
the rule holds for them with any `lands`; `build` is `attended = true`
until a build kind with a declared landing is proven by hand (PLANNER.md
§18's phasing, seed §9).

---

## 7. What is deferred, and to where

Every register row not homed in §1–§6, with its reason and what
re-opens it.

| row | kind | deferred to | why | re-trigger |
|---|---|---|---|---|
| "Claim-vs-verified marker" *(ledger)* | shape | a handbook renovation in the Nisaba office | a `verified: DATE by SID` note belongs on handbook and survey lines, not the drafting-table; nothing here reads it | the first handbook chapter that carries repo facts |
| "Version-and-date title line" *(ledger)* | shape | nowhere: home none | regeneration retires; a blueprint carries its own date and sid, git carries versions | none |
| "Condensation at regeneration" *(ledger)* | shape | nowhere: home none | OFFICE.md §15 is the stronger rule (§0 rule 1); the open part — recovering the provenance of §5's `Carried forward:` rulings and §6's entries 1–9 from v3 in git — goes to the content-filing session | seed §10 step 5, bale-src's filing session |
| "Verbatim carry from Proposals" *(queue)*, its dependency | shape | cleanup, once `notes.md` is readable | bale does not archive `notes.md` by default (AGENT.md §5); cleanup can file Proposals only if the project archives responses or bale keeps the notes with the session — a slip for bale-src if neither | building the cleanup kind |
| "Records over reports" *(queue)*, the automatic comparison | judgment | the `check` kind | the doctrine line lands now (§4) and the close report prints both counts; running the comparison on every upward report needs the check kind | twine-src's check kind |
| "Watch condition, machine-evaluable" *(queue)*, four of seven | shape | four slips for bale-src | a HOLD cause class; a real round's self-report; a deliberate-accept marker; the unused forecast entries per session (§3.2) | each datum landing in bale's telemetry |
| MASTER.md's 117 rulings, 210 evidence entries, 25 watches, 133 rows, 125 riders | content | the content-filing sessions | N3: content moves after the verbs exist, by office sessions | seed §10 step 5 |
| Minting ids for the carried-forward rulings | shape (part of "Ruling naming") | the content-filing session | they have no dates to mint from until v3 is read | the same |
| A second board's numbers (office-src's front sheet) meeting bale-src's 1–133 | shape (part of "Board row identity, not sequence") | the Nisaba office's founding | only one board exists today | founding the Nisaba office (N8) |
| "Ratified — do not re-litigate marker on the charter" *(ledger)*, the office's own charter | judgment | the Nisaba office's founding sitting | the profile's Purpose is where it lives, and that office has no profile yet | the same |
| Reading projects on another machine | read side | Q-2 | what "online" means for office is open | Q-2 answered |
| A chat's landing | kind | Q-3 | the `chat` declaration carries the recommended landing, not a ruled one | Q-3 answered |

[2026-10-02: "the Nisaba office" in the rows above is the home
office, `~/home-office`, founded 2026-09-30; see the annotation
beneath `nisaba-seed.md` N8.]

Judgment rows homed as doctrine lines or house rules, collected so the
office-src session that lands OFFICE.md text finds them in one place:

- §15: appending is not rewriting (§0 rule 1).
- §5 or a new drafting-table section: one home per fact, cited by id
  (§0 rule 3; "One-home pointers and "recorded once"" *(ledger)*,
  "One-home rule for facts of record" *(queue)*).
- The drafting-table: a ruling on the ledger is reopened only by a
  sitting that names it, and a reopening is a new ruling that
  supersedes ("Re-litigation protection" *(ledger)*). Each office's
  profile may add the house rule; OFFICE.md §9 need not.
- The evidence ledger admits only what live traffic earned ("Admission:
  earned from live traffic" *(ledger)*).
- §10 and §13: the three read-side lines (§4).
- The desk computes its order ("Board ordering and sequencing"
  *(queue)*).
- An eye-watch no sitting has looked at is reported, never silently
  aged ("Watch condition, judgment" *(queue)*).
- A commandeered sitting re-asks as a new folder ("Goal commandeering
  on record" *(queue)*).

Rows listed as such, with nothing built (`bale-already`, `content`):
"Expected-provenance note for sittings straddling midnight", "DONE
record: a pointer to the sid, not a story", "What / Why / Scope hints",
"Close-time delta summary", "Light-block and probe ledger at close",
"Sitting-close block" *(queue)*; "In-place "Last landed by" line",
"Regeneration ceremony and its record", "Version-position pointer",
"Version landmark", "Location, INDEX listing, project-doc
categorization", "Standing facts about the machine", "Desk-practice
rules accreting in §7" *(ledger)*. The read side renders the
`bale-already` ones (§4); the `content` ones are filed by the content
sessions (the survey takes the machine facts, bale-src's own docs and
ADRs take the desk-practice rules, the project's INDEX takes the
location), and the ledger register's "Project-facing rulings the
office should not take" stay bale-src's.

---

## 8. Landing order for office-src

Four sessions, packed from office-src, along four seams. Goals as the
planner would state them; the packs are the planner's to author.

1. **Space and templates.** Give the drafting-table its contents: the
   `filed` list form in `share/spaces.toml` and `office upgrade`'s
   reading of it; `templates/blueprint.md`, `templates/close-report.md`
   and the page skeletons for rulings, evidence, watches, the watch
   log, riders, the agenda and moves; `folder.md`'s field block, Riders
   and History; `doctrine/checks/filed-append-only.sh`; and the
   OFFICE.md lines of §0 and §7 that the space needs (§15's append
   rule, one home per fact, the ledger rules).
2. **The verb-table columns.** Add `lands`, `attended` and `trigger`
   to every verb in `share/verbs.toml`, declare the seed's §5 kinds as
   §6 writes them, and make office-src's tests and `office status`
   refuse an unattended session-kind verb with no landing. While its
   forecast stays disjoint from session 1's (1 in the catalogs,
   templates, doctrine and upgrade's reader; 2 in `verbs.toml`, its
   tests and the status check), the two run beside each other; if both
   need one source file, 2 serializes after 1.
3. **The read side.** After 1: the `[projects]` table in the floor
   plan; the consumption manifest, written from a probe of bale's JSON
   surfaces (stats included, so the watch queries of §3.2 can be named
   from what it finds); the reader over each project's registry and
   telemetry; the renderings of §4 that need no new verb — the
   in-flight list, a folder's sessions with outcomes, the trust ledger,
   last landed by, the version trail — inside `office sessions` and the
   walk-in screen; and OFFICE.md §10's and §13's lines. It can run
   beside 2.
4. **The verbs.** After 1, 2 and 3, because the desk's In-flight group,
   the one-writer rule and the watches check all read the registry
   through 3's reader: numbers, statuses, gates and history in `office
   open`, `close`, `reopen`, `sessions` and `desk`; `office moves`; the
   blueprint, rider, agenda, rulings and evidence verbs; `office
   watches` and `office watches check` with `share/watch-queries.toml`;
   the one-writer rule; `office status`'s three new checks; and `office
   digest` last, since it composes all of them. If the pre-flight says
   it will not fit one session, the seam inside it is desk verbs first,
   drafting-table verbs and the digest second.

The four bale-src slips of §3.2 are not office-src sessions; they go
to bale-src's own queue (its MASTER.md fold-in registry), each
confirmed by the probe in session 3 first. Once 1–4 have landed, the
Nisaba office can be founded (seed N8) and the content sessions of
seed §10 step 5 can file MASTER.md.

[2026-10-02: "the Nisaba office" here is the home office,
`~/home-office`, founded 2026-09-30; see the annotation beneath
`nisaba-seed.md` N8.]

---

## Appendix A — Register trace

Every row of both registers, by protocol name, with its kind and where
this blueprint disposes it.

| protocol | register | kind | disposed in |
|---|---|---|---|
| In-flight snapshot | queue | shape | §4 In flight; §2.3 |
| Watch entry shape | queue | shape | §1.4 |
| Watch condition, machine-evaluable | queue | shape | §3.2; four data deferred, §7 |
| Watch condition, judgment | queue | judgment | §1.4 (`evaluates: eye`); doctrine line, §7 |
| Watch firing history | queue | shape | §1.4, `watch-log.md` |
| Watch closure in place | queue | shape | §1.4, the `closed` record |
| Watch provenance | queue | shape | §1.4, `source` |
| Observation watch, no action attached | queue | judgment | §1.4; §3.1 standing lines |
| Ruling queue | queue | shape | §1.6, `agenda.md` |
| Fold-in registry, the list | queue | shape | §1.5, Q-11 |
| Registry entry shape | queue | shape | §1.5 |
| Verbatim carry from Proposals | queue | shape | §1.5, cleanup §3; dependency deferred, §7 |
| Rider lifecycle: rides → carrier → consumed | queue | shape | §1.5, status and orphans |
| Dispositions entry, "stands as shipped" | queue | shape | §1.1 close report, Proposals; §5.2 |
| Sitting-close block | queue | content | §5.2 (listed; split, nothing built for the block) |
| One-home rule for facts of record | queue | judgment | §0 rule 3; §5.2 doctrine line |
| Ratified judgment calls list | queue | shape | §2.1 Sessions, `ratified` lines |
| Goal commandeering on record | queue | judgment | §5.2 |
| Expected-provenance note for sittings straddling midnight | queue | bale-already | §5.2, §7 (listed) |
| Board row identity, not sequence | queue | shape | §2.1 `number`; second board deferred, §7 |
| Row title status vocabulary | queue | shape | §2.1 `status` |
| Row header line | queue | shape | §2.1 `class`, `size`, `lane`, `source` |
| Board ordering and sequencing | queue | judgment | §2.3; doctrine line |
| Dated bracket annotation | queue | shape | §2.1 History |
| Bracket verb vocabulary | queue | shape | §2.1 History verbs |
| DONE record: a pointer to the sid, not a story | queue | bale-already | §2.1, §4 (listed) |
| DONE at birth | queue | shape | §2.1, `office open --filed` |
| Arc row and its close report | queue | shape | §1.1 |
| What / Why / Scope hints | queue | bale-already | §1.5, §2.1 `source` (listed) |
| Row lineage and source | queue | shape | §2.1 `source` |
| Absorption, fusion, split, retirement | queue | shape | §2.1 statuses |
| Consumer and gate | queue | shape | §2.3 |
| Deferred / when-ready bucket | queue | shape | §1.5, no buckets |
| Cross-reference pointer grammar | queue | shape | §1.7 |
| The close is a session | queue | judgment | §5, retired under Q-4 |
| Close-time delta summary | queue | bale-already | §3.1 (listed) |
| Light-block and probe ledger at close | queue | bale-already | §3.1 (listed) |
| Records over reports | queue | judgment | §4 doctrine line; §1.1 Claims; automation deferred, §7 |
| Re-seed by stating progress against the doc | ledger | shape | §3.1 `office digest` |
| Version-and-date title line | ledger | shape | deferred: home none, §7 |
| In-place "Last landed by" line | ledger | bale-already | §4 (listed) |
| Going-forward convention | ledger | shape | §5.1, the sitting's `writes` |
| Location, INDEX listing, project-doc categorization | ledger | content | §7 (listed) |
| Ratified — do not re-litigate marker on the charter | ledger | judgment | §1.1 `ratified:`; office charter deferred, §7 |
| One-home pointers and "recorded once" | ledger | judgment | §0 rule 3; doctrine line, §7 |
| Per-arc residual summary | ledger | shape | §1.1 close report, Residual |
| Condensation at regeneration | ledger | shape | §0 rule 1; home none, §7 |
| Regeneration ceremony and its record | ledger | bale-already | §7 (listed) |
| Version-position pointer | ledger | bale-already | §3.1, §4 (listed) |
| Ruling block: date and source | ledger | shape | §1.2 |
| Ruling naming | ledger | shape | §1.2, the id |
| Verbatim capture of the operator's words | ledger | shape | §1.2 `words` |
| Landing pointer on a ruling | ledger | shape | §1.2 `landed` |
| In-place amendment of an earlier ruling | ledger | shape | §1.2 amendments |
| Scoped supersession | ledger | shape | §1.2 `supersedes` |
| Re-litigation protection | ledger | judgment | doctrine line and house rule, §7 |
| Lift from chat or board to §5 | ledger | shape | §5, retired under Q-4 |
| Grounding citations on a ruling | ledger | shape | §1.2 `grounds` |
| Rulings sourced from a light-block reply | ledger | shape | §1.2 `source` |
| Close-recorded, not desk-recorded | ledger | shape | §5, retired under Q-4 |
| Close proves its insertions by reversal | ledger | shape | §5.4 |
| Evidence entry identity and shape | ledger | shape | §1.3 |
| Batch provenance header | ledger | shape | §1.3 `filed` |
| In-place accretion on an entry | ledger | shape | §1.3 occurrences |
| Occurrence attribution | ledger | shape | §1.3 `attributed-to` |
| Citation of evidence by number | ledger | shape | §1.3, §1.7 |
| Admission: earned from live traffic | ledger | judgment | §1.3; doctrine line, §7 |
| Derivation into doctrine leaves the entry | ledger | shape | §1.2, §1.3 derived records |
| Standing facts about the machine | ledger | content | §7 (listed) |
| Version landmark | ledger | bale-already | §3.1, §4 (listed) |
| Dated measurements, never standing counts | ledger | judgment | §4 doctrine line; §3.1 |
| Claim-vs-verified marker | ledger | shape | deferred, §7 |
| MASTER.md's own include rule | ledger | shape | §1 (not hung), §5.1 ships |
| Desk-practice rules accreting in §7 | ledger | content | §7 (listed) |
| Findings register table | ledger | shape | §1.1 close report, Findings |
| Disposition vocabulary and split dispositions | ledger | shape | §1.1 close report, Findings |
| Dispositions updated in place | ledger | shape | §1.1; §4 derived state |
