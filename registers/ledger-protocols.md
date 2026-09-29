# Ledger protocols — MASTER.md header, §1, §2, §5, §6, §7, §8

Landed by session `2026-09-28-master-audit-ledger-002` against the copy
of `bale-src/claude/MASTER.md` that traveled with the request: 12,476
lines, last landed by `2026-09-24-sitting-close-deltas-19-001`. Line
ranges below are of that copy. Columns are `registers/README.md`'s; the
`kind` vocabulary is `shape`, `judgment`, `bale-already`, `content`.
Anchors are a section heading (`header`, `§1` … `§8`) with the line
range the protocol was read at, `§5 L8738–8764`; several anchors are
separated by `;`.

Two anchors (the in-place amendment row and the evidence-citation
row) normalized 2026-09-29 by `2026-09-29-suite-merge-001` to the
grammar `registers/README.md` pins, which is this register's own made
strict; no other cell changed.

The section counts the rows rest on, re-derived from the copy: header
lines 1–21; §1 from line 22; §2 from line 44; §5 lines 8714–9728, 36
blocks opening `New, ratified`, 117 rulings, every one a bullet with a
bold lead; §6 lines 9729–12037, entries 10–219 numbered (contiguous, no
gaps), 1–9 carried as one paragraph, 26 `New from …` batch headers, 19
dated `[YYYY-MM-DD: …]` appendices inside entries; §7 lines 12038–12460,
78 top-level bullets, 12 of them version landmarks; §8 lines
12461–12476, a nine-finding table.

## The register

| protocol | anchor | what it does | kind | office home | checkable | open |
|---|---|---|---|---|---|---|
| Re-seed by stating progress against the doc | header L3–7 | The doc's stated use: a fresh master chat states its current progress against this file and continues; regenerate at major milestones | shape | `office digest` (the sitting-open page the seed's §5 table names; ships the drafting-table and the desk) — the ledger side is that the blueprint and ledgers are what a sitting opens against, never a narrative | The sitting verb's `ships` in `share/verbs.toml` names the drafting-table | Whether "state progress against" becomes a digest section (what changed since the last sitting) computed from bale's records rather than read from a doc |
| Version-and-date title line | header L1 | `# … — v5 — 2026-08-16`: the regeneration number and its date identify which condensation the reader holds | shape | None once regeneration retires (see the condensation row); a blueprint carries its own date and session id, and git carries versions | Title matches `^# .* — v[0-9]+ — [0-9]{4}-[0-9]{2}-[0-9]{2}$` | Drop with regeneration, or keep as the blueprint's `revised` date |
| In-place "Last landed by" line | header L14–15 | Names the session that last landed a change to the record; edited in place at each landing, never appended | bale-already | The read side: bale's registry and telemetry know which session last applied a change whose forecast held the ledger's path; the office renders it, never hand-edits it | The line names exactly one sid; the sid is the latest applied session whose `resolved_scope` covers `claude/MASTER.md` | Confirm bale's telemetry record carries the applied `changes[]` paths and not only the forecast; if only the forecast, "last landed by" is still derivable because every close forecasts the ledger |
| Going-forward convention | header L17–20 | Recorded once, effective v4: sittings write `claude/telemetry/` records, board rows, evidence entries and §5 contracts; no per-sitting narrative accretes; the header line is edited in place | shape | The sitting verb's `writes` in `share/verbs.toml` (the seed's sitting row: blueprint and board deltas, a notepad page, bundles); telemetry records are bale's and drop from the list | `verbs.toml` declares `writes` for `sitting`; a close's `changes[]` stay inside the declared paths | Whether sittings write the ledgers directly (seed Q-4) or a close session does (today: nineteen `sitting-close-deltas` sessions) |
| Location, INDEX listing, project-doc categorization | header L9–12; §5 L8748–8755 | The record lives in the repo at `claude/MASTER.md`, listed in `INDEX.md`, categorized as a project doc not a global one; regenerate = edit in place | content | Project-facing: the project's `INDEX.md` and DOCS.md inventory; the office's equivalent is `floor-plan/manifest.toml` listing the drafting-table | Project side: DOCS.md §9's INDEX coherence (the crafter's `--doc-assertions --index`) | Nothing for the office: a ledger on the drafting-table is listed by the floor plan, not by a doc |
| Ratified — do not re-litigate marker on the charter | §1 L22–43 | The ultimate goal and its ratified floor (four "what"-shaped controls) and two axes are pinned; the heading says ratified and forbids re-litigation | judgment | Profile `Purpose` (`share/profile-shape.toml`) for the office's own charter; a `ratified` flag with date and sitting sid on a blueprint's charter for a project's | The heading carries the marker; the charter's bytes unchanged since the ratifying sitting (hash against git) | The floor's four controls are PLANNER.md §10's (a DOCS.md §9 sanctioned pair); an office copy would be a third home — point, do not copy |
| One-home pointers and "recorded once" | §2 L118–121; §2 L110–116; §5 L9016–9020; header L17 | A fact or rule has one home; other sections point ("one home — §7's landmark", "wording unchanged there", "recorded once", "the one home for their contract force") | judgment | Doctrine line: OFFICE.md §5 Handbook already has it for public docs ("a chapter points at it rather than restating it"); extend to ledgers: a blueprint cites a ruling or an evidence entry by id, never restates it | A restated ruling is a duplicate bold lead across sections (grep) — weak | Whether the read side resolves pointers into rendered text so restating never tempts |
| Per-arc residual summary | §2 L54–116 | One paragraph per closed arc: `**The <name> arc — CLOSED <date>** (board N; sids …)`, the version range, the residual, and where the upward report lives (`claude/context/board-N-arc/`) | shape | A blueprint's close section on the drafting-table (the seed's "blueprint's close template"); the arc's folder goes to the filing cabinet whole and the blueprint keeps only this | Each residual names a board row and at least one sid; every sid resolves in bale's registry; the version range matches §7's landmarks | Derive the residual from the close's upward report (read side) instead of writing it twice |
| Condensation at regeneration | header L5–7; §2 L46–52; §5 L8716–8736; §6 L9735–9745 | At a milestone the doc is regenerated in place: the per-sitting log condenses out, board queue entries condense to pointers, the old version lives in git and in telemetry; contracts (§5), evidence (§6) and findings (§8) are said to stay | shape | None — OFFICE.md §15 is the stronger rule: filed paper is never rewritten. The arc's folder files whole, the blueprint holds the summary, git holds history; nothing condenses | With §15: `office upgrade` already rolls back if filed paper changed; the same diff check guards a filed ledger. For MASTER.md today: nothing | The cost is already visible: §5 opens with a `Carried forward:` paragraph of pre-v4 rulings with no dates and no sources, and §6's entries 1–9 are one paragraph — condensation reached the ledgers, not only §2. The merge decides whether to recover the provenance from v3 in git |
| Regeneration ceremony and its record | §2 L123–131 | A regeneration is three sessions — a read-only orchestrator authors the ratified brief, a worker lands the regeneration, a microdeltas session ratifies — and §2 records the sids | bale-already | Retires with condensation; the sids that landed anything are bale's registry and telemetry, rendered by the read side | Every sid named resolves | Nothing once regeneration is gone |
| Version-position pointer | §2 L118–121; §7 L12187–12420 | "Current version: one home — §7's bin/bale landmark"; the sitting-open version check is satisfied by the request's `provenance.bale_version` stamp (paste-form rule retired, evidence 80) | bale-already | The read side: every request stamps `bale_version`; `bin/VERSION` is in the repo; `office digest` shows the tool version per project from bale's records | §7's latest landmark equals `bin/VERSION` at the copy's commit | Whether `bale stats` answers "version at each session" or the office reads the request manifests |
| Ruling block: date and source | §5 L8738–9728 (36 blocks) | A block opens `New, ratified <date> (<source>):` — the source is a sitting sid, a desk, "in chat", a brief, or an operator's light-block reply; blocks are chronological and appended at the end | shape | Drafting-table rulings ledger: one record per ruling with `date` and `source` (a sid, or a notepad page for words said in chat) | Every block has a date; block dates non-decreasing; every sid in an opener resolves | The source vocabulary (sid, notepad page, light block `[n]`, brief) needs fixing before `amendment_target` can point at it |
| Ruling naming | §5 L8738–9728 (117 rulings) | A ruling is a bullet whose bold lead is its name; rulings are cited by name in prose, never by number | shape | Ledger record `name`; give each an id (rulings are the seed's `amendment_target` for exchange answers, and a name is not a stable target) | Every §5 bullet opens `- **`; names unique within the section | Number rulings like evidence entries, or key them `<date>/<slug>` |
| Verbatim capture of the operator's words | §5 L9355–9359; L9636–9645 (17 `verbatim` markers) | A ruling of record quotes the operator byte-verbatim ("Operator's ruling, VERBATIM from the desk: …", "Byte-verbatim:") and marks it so | shape | The notepad (`notepad/DATE-SLUG.md`, filed, verbatim and dated, never edited) holds the words; the ledger record points at the page. OFFICE.md §5 Notepad is the stronger rule: every sitting's words are filed, not only the ones a ruling quotes | A quoted ruling's text appears in a notepad page (grep) | Whether a light-block reply ("as assumed") is a notepad line or only bale's `notes.md` trail |
| Landing pointer on a ruling | §5 (18 `landed at row / lands at row / landed via` pointers) | A ruling names where it took effect: a board row, a wave, a doc section, or a session | shape | Ledger record `landed` pointing at a folder (the board row's future) or a sid; the queue side owns the row | Every pointer resolves to a board row or a sid | Ledger side only; the row's back-pointer to the ruling is the queue audit's |
| In-place amendment of an earlier ruling | §5 L8801–8816; L8936; L9318; L9564 (6 dated markers: `(amended 2026-08-05 …)`, `(trued up 2026-08-16 …)`, `[2026-07-25: …]`, `[2026-08-06: …]`, `[2026-09-20: …]`, `[2026-09-21: …]`) | A later sitting amends an earlier ruling inside its bullet with a dated parenthetical or bracket; the original wording stays readable | shape | Ledger record `amendments[]`: date, sid, text — appended to the record; the seed's `amendment_target` for exchange answers is this field | Every amendment carries a date; the date is on or after the block's date; no ruling bullet was rewritten between two copies (diff) | OFFICE.md §15 forbids rewriting filed paper; an amendment as a new record that points back keeps the ledger filed. The merge chooses between an `amendments[]` field on a live record and a filed append |
| Scoped supersession | §5 L9355–9361; L9342; L9413; L9485 | A ruling names what it supersedes and how far ("Supersedes board 51's multi-open refusal only"; "superseded for the sandbox escape only"); the superseded ruling stays in place | shape | Ledger record `supersedes` (target id plus scope text); the read side shows a superseded record as such | Every named target exists; a superseded record is never deleted (diff) | Today only forward pointers exist: the superseded ruling does not say it was superseded. Back-pointer derived by the read side, or written? |
| Re-litigation protection | §5 L8714; L9385–9387; §1 L22 | The heading says "do not re-litigate casually"; rulings add "Not re-litigated by …" clauses; lifting a chat ruling to §5 is "for re-litigation protection" | judgment | Doctrine line for the drafting-table plus a house rule in the profile: a ledger ruling is reopened only by a sitting that names it | Nothing | How a reopening is recorded (a new ruling that supersedes, presumably) |
| Lift from chat or board to §5 | §5 L9014–9020; §4 L5857 (`[2026-08-16: lifted to §5.]`) | A ruling resolved in chat or on a board row is lifted into §5 as its one home; the board side gets a dated `[lifted to §5]` note and its queue entry condenses to a pointer | shape | Sitting verb `writes` the rulings ledger directly (seed Q-4), so nothing is lifted; a board row that resolved into a ruling points at the record | Every `[lifted to §5]` annotation on the board has a §5 ruling dated the same day (queue side) | Q-4. Ledger side registered; the board's annotation is the queue audit's |
| Grounding citations on a ruling | §5 (15 `evidence NN` / `§6 entry NN`; 6 `ADR-NNNN`; 23 `board N`) | A ruling's rationale points at evidence entries by number, ADRs by number, and board rows | shape | Ledger record `evidence[]` (entry ids) and `adrs[]`; the read side resolves them | Every cited evidence number exists (≤ the last entry); every ADR path exists in the project | Nothing |
| Rulings sourced from a light-block reply | §5 L9692–9728 ("Block one, [2]"; "as assumed") | The operator's inline or "as assumed" answer to a worker's light question block is a ruling of record, cited by block and question index | shape | The ledger record's `source` admits a light-block answer; the trail is the response's `notes.md` (TARBALL.md §5.10), which bale archives and the office reads | The cited response's `notes.md` names the question and the answer | Whether the office's cleanup files "as assumed" defaults as rulings automatically |
| Close-recorded, not desk-recorded | §5 L9631–9634; L9692–9694 ("recorded at close 18/19") | Rulings made at a desk are written into §5 by a later close session, which cites the desk and the close | shape | Retires under Q-4: the sitting writes; otherwise the `cleanup` verb (`writes` includes the drafting-table) is the close | The close's `changes[]` are additions and enumerated in-place edits only (see the reversal row) | Q-4 |
| Close proves its insertions by reversal | §5 L9702–9707 | From close 19 a close's `validation.sh` removes its declared additions, restores any line it edited in place, and hashes the result to the request's `provenance.base_files` sha256 for the ledger: one exact check that nothing else moved | shape | An office check on every ledger write: append-only plus enumerated in-place edits, mechanized. OFFICE.md §15's `office upgrade` rollback is the same idea for migrations; extend it to sessions | Exactly this: reverse the additions and compare to `base_files` (bale stamps the hash already) | Whether ledger writes go through bale so the check rides every close's `validation.sh`, or the office runs it as a hook at `office sessions` |
| Evidence entry identity and shape | §6 L9747–12037 (entries 10–219) | `NN. **Title.** body`; the number is the identity, monotonic, never reused or renumbered; entries are never deleted | shape | Drafting-table evidence ledger: numbered records, marked filed (`filed = true` in `share/spaces.toml`'s sense) | Numbers contiguous from the first to the last; count equals last minus first plus one; every title bold | Entries 1–9 lost their shape at regeneration (one paragraph, L9735–9745) — the filed rule would have kept them |
| Batch provenance header | §6 L9800–10704 (26 `New from the <date> sitting (<slug>):` headers) | Entries land in batches per sitting; the batch header carries the date and sitting; a closing parenthetical on the entry is optional (106 of 210 close with one, naming a sid, a decision or a section) | shape | Ledger record `sitting` (sid) and `date`, filled per record from the batch at write time | Every entry sits under a batch header; every batch header has a date | Make provenance per record: a batch header is lost the moment an entry is cited alone |
| In-place accretion on an entry | §6 L9761–9769; L9770–9788 (19 dated `[YYYY-MM-DD: …]` appendices; 11 entries with occurrence counts) | An entry gains dated bracket appendices and running occurrence counts ("Second occurrence, packer-attributed … Third occurrence, this sitting … [Next occurrence, 2026-08-03 …]"); numbering is append-only, bodies accrete | shape | Ledger `occurrences[]`: one record per occurrence (date, sid, attribution) pointing at the entry — a new record each time, never an edit to the entry (OFFICE.md §15) | Every appendix carries a date; the date is on or after the batch's; entry text before the first appendix unchanged between copies (diff) | The seed's "append-only" is true of numbers, not bodies. The queue side's calibration trigger (three same-class events) counts these occurrences |
| Occurrence attribution | §6 L9770–9788 ("packer-attributed", "sub-master-attributed", "worker as packer") | Each occurrence names which role caused it; a class spans the roles it has been seen in; "two occurrences upgrade this from incident toward class" | shape | Occurrence record `attributed_to` from bale's role vocabulary (planner, worker, operator, courier); the class threshold is the queue side's `office watches check` | Attribution values in a closed vocabulary | Ledger side stops at the attribution field; the threshold and the trigger are the queue audit's |
| Citation of evidence by number | §6 L9729–12037 (cited from every section: 180 `§6 entry NN`, 37 `evidence NN`, 15 `evidence entries NN–MM`; from §3: 112, §4: 56, §5: 15, §7: 12, §2: 3, §8: 1) | Evidence is cited by number from every other section and from other entries ("See evidence 49"); never restated | shape | One citation form (`evidence NN`) the read side resolves into the record; blueprints, folders and rulings cite it | Every cited number exists; no dangling citation | Two spellings exist today; pick one |
| Admission: earned from live traffic | §6 L9729–9730 | The section's own rule: each entry is a rule earned from live traffic — an observed event with a session behind it, not a design opinion | judgment | Doctrine line for the evidence ledger | Weak: an entry names a sid or a session (63 lines in §6 cite a sid) | Whether a record without a sid is refused at write |
| Derivation into doctrine leaves the entry | §6 L9732–9734 | Planner-facing doctrine derived from named entries now lives in `docs/PLANNER.md`; the ledger entries stay unchanged; the section says which entries fed which doc | shape | Ledger record `derived_into` (doc and section); the derived doctrine itself is project-facing and stays in the project's docs | The named doc and section exist | Nothing |
| Standing facts about the machine | §7 L12040–12052; L12206–12209 | Bullets of facts with no judgment: WSL, the Downloads path, hooks, archive config, the pack machine's clock (UTC, verified) | content | `floor-plan/survey.md` (exists, OFFICE.md §13: facts only, overwritten every run) for machine facts; a handbook chapter's "For sessions" layer for repo facts that are private | The survey is regenerated, never edited (exists) | Repo facts with an audience (module list, tests layout, load-time imports) belong in the project's own docs, not the office |
| Version landmark | §7 L12187–12420 (12 `Version landmark` bullets) | Each bump appends `Version landmark: 0.4.NN (sid)`; bumpless landings get "unchanged at" / "still" landmarks naming their sids; §2 points here as the one home | bale-already | The read side: every request's `provenance.bale_version` and each session's telemetry carry the version; `office digest` renders the per-project version trail | Latest landmark equals `bin/VERSION` at the copy's commit; each landmark's sid resolves | Whether `bale stats` exposes version-per-session or the office reads request manifests |
| Dated measurements, never standing counts | §7 L12053–12071 ("a dated figure, not a standing count"; "enumerate from the tree, never from this doc"; "counts stated in briefs are claims to verify") | A number that can go stale carries its date and a rule not to trust it; counts and per-file lists are excluded from the record | judgment | Doctrine line; the survey's rule is stronger (recompute on every run, record nothing by hand) — a drawer survey step (`drawer/survey/`) recomputes what §7 dates | A number in the page without a date beside it flags (regex) | Which §7 figures become survey steps |
| Claim-vs-verified marker | §7 L12092–12094; L12181–12186 ("a claim; landed at … per the arc's upward report"; "verified 2026-09-15"); §2 L93–96 ("a claim to verify") | A fact the record did not observe is labeled a claim until a session verifies it; the verification is dated and names how (a grep, a probe) | shape | A check-note field on a survey or handbook line: `verified <date> by <sid>`; or the fact is recomputed by a survey step and needs no note | `verified YYYY-MM-DD` parses; the date is not older than the fact's last change | Whether bale's probe (a dated, sid-bound read) is the verifier of record |
| MASTER.md's own include rule | §7 L12115–12118 | Include the record in any session that needs the gameplan; keep it out of sessions that do not (master context, not worker context, by default) | shape | `share/verbs.toml` `ships`: the sitting ships the drafting-table; `build` ships the folder and named handbook chapters only (the seed's §5 table) | `verbs.toml` declares it; a build pack's includes do not touch the drafting-table | Nothing |
| Desk-practice rules accreting in §7 | §7 L12119–12146 (working style, desk emission rules); L12159–12165 (include-authoring rules, "now four"); L12190, L12210, L12226, L12254, L12280 (forecast and include rules, "accreted <date>"); L12198, L12284 (dispatch check, "grown"); L12271, L12276 ("One-apply-behind held for") | §7 has become the home of standing desk rules and dated instances of known mechanisms, not environment facts | content | Project-facing: the include-authoring, forecast and dispatch rules are bale-src's (PLANNER.md or ADRs); the working style is a profile house rule; the "held for" instances are evidence occurrences | Nothing today | The merge decides per bullet; none of these is the survey's |
| Findings register table | §8 L12461–12476 | `# \| Finding \| Disposition`; stable finding ids (1a, 1b, 2–9); the heading names the audit session and date; "the board carries the work" | shape | A filed audit sheet on the drafting-table (nearest template: `clipboard-sheet.md`'s "Decided … who owns each follow-up"), cross-linked to folders | The table has three columns; ids unique; every disposition names at least one of `Board N`, `ADR-NNNN`, a session, `§5`, `evidence NN` | Nothing |
| Disposition vocabulary and split dispositions | §8 L12467–12476 | A disposition is a pointer: a board row (queued), an ADR with status and date (doctrine), "Fixed in <session>" (done), a §5 contract, an evidence entry; a finding may split ("Doctrine: … Implementation: …") | shape | Disposition field with a closed pointer vocabulary: folder, ADR, sid, ruling id, evidence id | Every pointer resolves | Nothing |
| Dispositions updated in place | §8 L12468 ("ADR-0016 (Accepted 2026-08-07)" in a 2026-07-13 register) | A disposition's state is edited as it resolves; the register is not filed at audit close | shape | The read side derives the state from the folder or ADR the disposition points at; the sheet itself is filed at audit close (OFFICE.md §15) | Nothing today; with §15, the filed-paper diff | Whether an audit sheet is filed at close or lives on the drafting-table until every disposition resolves |

## Where the seed's first pass (nisaba-seed.md §6) was wrong or incomplete

- **§6 "numbered, append-only, cited by number."** Append-only holds
  for the numbers (10–219, contiguous, never reused) and not for the
  bodies: nineteen entries carry dated `[YYYY-MM-DD: …]` appendices and
  eleven carry running occurrence counts written into the entry at later
  sittings (entry 13 spans three sittings and four occurrences). The
  register splits this into the identity row, the accretion row and the
  attribution row. Under OFFICE.md §15 an occurrence is a new record
  pointing at the entry, never an edit.
- **§5 "dated, sourced to a sitting."** Confirmed, and richer than the
  seed had it: rulings are named not numbered (117 bold leads, no ids),
  carry landing pointers, are amended in place with dated markers,
  supersede with explicit scope, quote the operator verbatim, and can be
  sourced from a light-block reply. The `amendment_target` the seed
  wants for exchange answers has nothing stable to point at until
  rulings get ids.
- **"§2 per-arc residual summaries; condense to git at milestones."**
  The condensation reached the ledgers, not only §2: §5 opens with a
  `Carried forward:` paragraph (L8716–8736) of pre-v4 rulings stripped
  of their dates and sources, and §6's entries 1–9 are one paragraph.
  That is the concrete case for the seed's own note that OFFICE.md §15
  is the stronger rule.
- **"§7 standing environment facts and landmarks — mostly exists."**
  Roughly a third of §7's 78 bullets are environment facts the survey
  covers. The rest are version landmarks (bale already stamps the
  version on every request) and desk-practice rules that accreted here
  because the doc had no better section — include-authoring rules,
  forecast rules, dispatch checks, dated "one-apply-behind held for"
  instances. Those are project-facing or evidence, not survey.
- **"Last landed by — bale already."** Agreed, with one thing to
  confirm at the merge: whether bale's telemetry records the applied
  `changes[]` paths per session or only the forecast. Either way the
  line is derivable, because every close forecasts the ledger's path.
- **§8 "filed ledger page cross-linked to folders — shape."**
  Confirmed, with one wrinkle the seed did not see: dispositions are
  edited in place as they resolve (finding 1b's disposition carries an
  ADR status dated three weeks after the register's date), which a
  filed page cannot do. The read side has to derive that state.
- **Not in the seed's table at all:** the close-by-reversal check
  (§5 L9702–9707), which is the one ledger protocol MASTER.md already
  runs mechanically and the office should inherit as a check on every
  ledger write; the claim-vs-verified marker; the dated-measurement
  rule; the derivation-leaves-the-entry rule; and the batch-header
  provenance that per-record provenance should replace.

## Where OFFICE.md already has the stronger rule

- **§15, filed paper is never rewritten** — against regeneration's
  condensation, in-place amendment of rulings, in-place accretion on
  evidence entries, and in-place disposition updates. Four MASTER.md
  protocols edit filed text; under §15 each becomes a new record that
  points back, and the read side renders the current state.
- **§5 Notepad, the occupant's words verbatim and dated, never
  edited** — against §5's selective `VERBATIM` quoting. The office files
  every sitting's words; a ruling points at the page.
- **§13 The survey, facts only, overwritten every run, never edited by
  hand** — against §7's dated figures and "enumerate from the tree"
  warnings. What §7 dates, a survey step recomputes.
- **§5 Handbook, a chapter points at public documentation rather than
  restating it** — the one-home rule MASTER.md applies by hand, already
  doctrine for the office.
- **§14, only `office upgrade` writes the version stamp** — the
  precedent for the "last landed by" line: a stamp means the tool
  checked, never that someone said so.

## Project-facing rulings the office should not take

Rulings in the audited sections that bind any reader of bale-src rather
than the occupant, and so belong in bale-src's ADRs, changelog or global
docs, not the office: the cadence rulings (doc-only and tests-only
sessions bump-exempt, §2 L107–110 and §7's landmarks); the four
include-authoring rules and the forecast rules (§7 L12159–12165, L12190,
L12226); the one-clock ruling (§5 L9380–9387, already landed verbatim in
TARBALL.md §1); the terminal-shapes ruling (§5 L9388–9402, landed in
TARBALL.md §5.10); and the mechanize-shape contract itself (§5
L8825–8836), which is the pattern this register follows.
