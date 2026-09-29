# Nisaba — Suite Seed Document

> The seed document for the Nisaba suite: what the tools are, where
> the seams between them fall, what was ruled at the sitting that
> defined them, and what is still open. First commit of the
> nisaba-src repository, on the precedent of tedder-src's
> `harness-seed.md`.
>
> Provenance: authored at bale-src session
> `2026-09-28-open-discussion-001` (read-only planner session, packed
> from bale-src at bale 0.4.45, goal: "before we design the harness,
> I'd like to define the overall product I'm creating here"). The
> architect's messages are transported verbatim in section 11; every
> ruling in section 2 cites the message it comes from. The agent's
> side of the sitting is distilled into sections 3–9; the chat
> transcript is its only verbatim record.
>
> Standing rule from the sitting (message 3, verbatim): "Don't worry
> about the previous harness or office ratifications, we're
> redesigning everything but the core of bale here." So tedder-src's
> `harness-seed.md` D1–D24 and office-src's 2026-09-23 construction
> sitting are **inputs** to this document, not contracts over it.
> Where this seed and either of them disagree, this seed is the
> later ruling. office-src's `doctrine/OFFICE.md` remains the
> doctrine of the office *as built*; section 2 says what this seed
> changes about it, and nothing else in it is touched.

---

## 1. Identity and premise

**Nisaba** is a suite of three tools and one shell that together let
one person run AI-assisted work on any project, situation or meeting
— from a code change to a house purchase — with the full context the
work needs, the records to trust it, and a path from hand-carried
sessions to unattended orchestration that never loses the hand path
as ground truth.

The architect's direction, verbatim (from tedder-src's
`harness-seed.md` Q-7, recorded 2026-09-24): "I expect tedder, office,
and bale to all work together to eventually create a suite of tools
that allows full agentic spawning and full meta-context of any
project/situation/meeting that needs to be AI-assisted, and allows
claude or any other llm the full toolset to do so."

The four components, one line each; section 3 gives each its
definition:

- **bale** — the session. The wire contract between a planner and a
  worker (request, response, probe, exchange) and the verbs that
  carry a session from pack to close inside one repo. **Unchanged by
  this seed.**
- **office** — the person and the job. A git repo organized like a
  physical office, holding what only its occupant and their sessions
  may read, across projects and time; and — new with this seed — the
  home of a project's progression (the queue, the watches, the
  rulings, the evidence) that MASTER.md carries by hand today.
- **twine** (formerly tedder) — the process. The courier that carries
  what a person carries by hand today, and the scheduler that spawns
  sessions from what the office declares. Headless. Holds no intent.
- **nisaba** (the shell) — the one UI over all three, in its own
  repo. Renders; never owns.

The layer cake, with dependencies pointing strictly downward:

```
              nisaba shell (UI)          one CLI per core
                   │                      bale / office / twine
                   ▼
      ┌──────── twine ────────┐   process: courier + scheduler
      │          │            │
      ▼          ▼            │
   office ─────► bale ────► git   office declares; bale carries; git lands
```

- bale depends on nothing.
- office depends on bale (packs ride bale; office reads bale's
  records, never copies them).
- twine depends on both (reads the office's declarations, drives
  bale's verbs, writes only its own mechanical streams).
- the shell depends on bale and office, and on twine **optionally**:
  an office on a machine with no API access still gets the shell,
  with the person as courier.

---

## 2. Rulings from the sitting

Each entry carries its status and its source. **Ratified** means the
architect said so in the sitting; **directed** means the architect
named the direction and the agent supplied the shape; **proposed**
means the agent's design, not yet ratified; **open** means asked and
unanswered — section 8 carries those with their recommended
defaults.

**N1 — bale's core is unchanged; everything else is redesigned.**
Ratified (message 3). bale ships the five global docs and the two
tools and nothing else (message 4: "MASTER.md is NOT currently a part
of the bale tool, only bale-src and meta development. the only docs
bale ships are the 5 globals."). Nothing in this seed adds to bale,
and nothing here is a bale-side obligation.

**N2 — The seam between office and project is ownership, and role
projections ride on it as verb declarations.** Directed. The line
(OFFICE.md §2, carried as built): a project holds what its audience
may read; the office holds what only the occupant and their sessions
may read. The agent's earlier picture — separation by *role*, what
the planner sees versus the worker versus the architect — is a finer
seam that fits inside the ownership seam and is implemented by what
each session kind's verb declares it *ships* (office's
`share/verbs.toml`), never by a second mechanism. The ownership line
is structurally enforced by bale: a project session's write forecast
names project paths, office context rides as a `--context` tarball,
and `bale apply` lands into the packing repo, so office material
cannot land in a project through apply.

**N3 — The office absorbs MASTER.md's intent: protocols first,
content last.** Ratified (message 4: "I do really like the idea of
merging the intent of MASTER.md with the intent of office, i think
the two are related and i didn't see that before." Message 5: "I
kind of disagree with just the idea of 'hanging MASTER.md'.
MASTER.md has a bunch of well tested protocols for stuff that office
is supposed to do mechanically and I'd like to extract all of that I
can before just hanging it as a non-core file"). The extraction
follows bale-src's own mechanize-shape pattern: where a MASTER.md
protocol is *shape* it becomes an office verb, template or check;
where it is *judgment* it becomes a doctrine line or a house rule;
where bale already does it mechanically it is dropped. Content moves
only after the verbs exist, and by office sessions, never by hand.
Section 6 carries the first-pass register and the extraction plan.

**N4 — Twine is the process layer: courier and scheduler, headless,
holding no intent.** Proposed shape under a ratified direction
(message 4 rejected "twine is web"; message 4 answer 3 assumed the
planning chat is a hosted office session, "open to more
discussion"). Twine's durable state is its mechanical streams only —
per-call usage and cost, the in-flight state of its transition
table, its consumption manifest of the surfaces it reads. Plans,
words, decisions and answers land in the office or the project. The
test: if twine's local state were deleted, what is lost? Spend
history and nothing else. Any design that would make the answer "a
plan" or "a conversation" is on the wrong side of the line.

**N5 — CLI and UI for office and for twine; offline and online for
both.** Ratified (message 4: "for 'the seat', I disagree that twine
is 'web'. I want both offline and online options for both, and I also
want CLI and UI interfaces for both"). Section 7 carries the
interface matrix and the one design rule that makes all four cheap:
each tool is a core with a command registry; every surface is a
client of the registry; every transport is a courier plugin. What
"offline" and "online" mean for office is open (Q-2).

**N6 — The UI is one shell in its own repo, nisaba-src.** Ratified
(message 6, answer 1). Hard dependency on bale and office, optional
on twine. The cores keep a CLI and a JSON surface and no rendering.
Reasons: dependency divergence (office is bash plus python stdlib,
bale is stdlib-only; a UI brings a framework); the shell must nest
what three tools produce (the office's walk-in screen, a folder's
sessions, twine's session pane, the inboxes); and the repo boundary
makes "renders, never owns" structural. The shell reuses twine's own
pattern against bale — a version pin per core and a consumption
manifest of the surfaces it reads — and a parity test walks each
core's command registry against the shell's actions, with any
CLI-only verb listed explicitly rather than absent.

**N7 — Every session kind declares its landing; no kind without a
declared landing may be spawned unattended.** Directed (message 4:
"I also like the idea of automatically keeping chats and possibly
even auto updating office/MASTER.md in the background. If this is the
case, we need more session-type definitions so we don't hit a
snag"). Section 5 is the table. The rule is D17's total-transition
idea (every outcome has a defined move) applied to session kinds,
and it is what makes background cleanup and kept chats safe under
OFFICE.md's house rule 1, "every session lands something."

**N8 — The first project of Nisaba is Nisaba, after office can
carry a project's progression; office-src dogfoods itself in-repo
until then.** Ratified with sequencing (message 4: "I want Nisaba's
first project to be Nisaba"; message 5: "I need to do much more work
on office before I start a nisaba office. The point of office-src
was to dogfood while I develop it, like bale-src."). The Nisaba
office — one office for bale-src, office-src, twine-src and
nisaba-src, since they share one set of house rules — is founded
only once the drafting-table and the read side (section 6) exist.
Until then bale-src keeps MASTER.md, office-src keeps its front
sheet and sittings under `claude/`, and this repo keeps this seed
and the registers.

**N9 — The extraction runs as two audit sessions split at MASTER.md's
§4/§5 seam, followed by a merge.** Ratified (message 6, answer 2).
The queue audit covers §3 (in flight, watches) and §4 (the board);
the ledger audit covers the header, §1, §2, §5 (contracts), §6
(evidence), §7 (environment facts) and §8 (findings). Each returns a
protocol register in the shape of section 6's table, landed in this
repo under `registers/`. A merge session turns the two registers
into office-src's blueprint for the drafting-table. Only then does
content move.

**N10 — The name tedder is retired in favor of twine.** Ratified
(message 2: "'tedder' is the name i had previously for twine, and I
haven't updated it anywhere yet"). The repo is still `~/tedder-src`
on chordsphere; `~/tedder-src-v0` is an earlier, unrelated attempt.
The rename of the repo and of `harness-seed.md`'s references is a
session of its own and is not scheduled by this seed.

---

## 3. The tools, defined

### 3.1 bale — the session

As built and as documented in its five global docs; restated here
only to fix its place in the suite. bale records everything from
pack to close inside one repo: the request (goal, includes, the
write forecast), the four turn-ending shapes a worker returns (a
response tarball, a probe block, a light question block, a
clarification response carried by `bale relay`), the apply pipeline
(pre-flight, staging, the worker's `validation.sh` beside the
planner's blind checkpoint, merge on PASS or hold on HOLD), the
per-sid registry and its disjointness gates, and the telemetry,
changelog and exchange records. The manual path — a person packs,
uploads, pastes the opener, carries each shape by hand, downloads
the response, applies — is the ground truth every other component
mirrors and never changes. bale is transport-agnostic and
project-agnostic, and it is not a master-changelog system (AGENT.md
§7): it records sessions and their lineage, never jobs or projects.

### 3.2 office — the person and the job

As built (office-src 0.2.0; `doctrine/OFFICE.md` is its doctrine):
an office is a git repo organized like a physical office — profile,
floor plan and survey, desk (open folders, one per job),
filing-cabinet (closed folders), notepad (the occupant's words,
verbatim, never edited), suggestion-box (friction slips), drawer
(the office's own tools), and by renovation a handbook (the private
layer of documentation), clipboards (recurring meetings), calendar,
rolodex, letterhead and drafting-table. It holds what only the
occupant and their sessions may read; projects hold what their
audience may read. It never runs, schedules or carries a session: it
declares what a session should carry and where it lands
(`share/verbs.toml`), and prints the pack line. Sessions that land
in the office are packed from it; sessions that land in a project
are packed from the project with the office's context riding beside
them as a context tarball. Hung items (the profile, the survey,
whatever a renovation hangs) ride with every office session through
bale's include group.

What this seed adds (N3, section 6): the office is also the home of
a project's **progression** — the queue of work with its ordering
and dependencies, the watches with their re-triggers, the rulings
ledger, the evidence ledger, the arc blueprints and their close
reports — and it has a **read side** that renders bale's records
from the project repos it scopes (a folder's sessions with their
outcomes; the trust ledger per work class) without ever copying
them. The line OFFICE.md §10 draws stands: "bale records everything
from pack to close inside one repo … The office records the person
and the job across repos and time"; "and when" is already on the
office's side of that line, and the board is "when."

### 3.3 twine — the process

The courier and the scheduler, and nothing else. As courier it
implements the four turn-ending shapes as a program: it executes a
probe block against the repo and feeds the paste back; it answers a
light question block from the office's declarations or parks it in
the escalations inbox; it relays a clarification round through `bale
relay`; it applies a response through `bale apply`. As scheduler it
reads a ratified decomposition from the office's drafting-table,
packs the children via bale (`bale open` on planner bundles),
dispatches them — to a model over an API, or, offline, by emitting
the same tarball and opener a person pastes — in parallel where
forecasts are disjoint and serialized where they are not, and
enforces a spend cap with bailout semantics (stop spawning, in-flight
workers hand off, validated work commits). It holds every bale verb
and executes the agent loop as operator; its workers hold tools that
reach only their per-sid sandbox and never a bale verb or an oracle.
Its core is headless; its CLI is `twine`; its rendering lives in the
shell.

Carried from `harness-seed.md` as still-good inputs, not contracts:
the cost spine and kill-switch as first foundations (D15); the total
transition function over bale's outcome and closure vocabularies
plus twine's own API-side stop set (D17); bale-native tools wrap
bale's shapes and never fork them (D13); bale-version pinning with a
consumption manifest (D2–D4); tool-access workers with lazy reading
(D10–D11); caching discipline as a design constraint (D12). Retired
by this seed: D9 ("a locally run web application … chat mode is the
default face") — the chat is a hosted office session (N4, Q-1) and
the face is the shell (N6); D22's "the harness chat is the planning
desk" is re-read as "a sitting is an office session twine hosts."

### 3.4 nisaba — the shell

One UI, in its own repo, for all three cores. Its home screen is
walking into the office (`office` with no verb: the desk, this week,
the last notes, the slips). A folder opens into its sessions; a
session opens into twine's pane (the conversation, thinking, tool
calls, the cost ticker); the four controls of PLANNER.md §10 —
ratify decompositions, answer escalations, review final merges,
grant trust expansions — are its inboxes. Everything else is a
read-only view. Offline, the shell shows the opener to paste and a
drop target for the response tarball, runs the probe the person
pastes back, and relays the exchange round — replacing the browser
tab groups the architect keeps by hand today (office-src sitting,
message 6) with the sessions' real state read from bale's registry.
TUI or local web is a rendering choice held loosely; the shell's
contents are the decision.

---

## 4. The flow, walked once

Today, on the manual path, from bale-src's own sittings: read
MASTER.md → author a bundle → `bale open` → upload the tarball to a
chat → paste the opener → the worker's turn ends in one of four
shapes → carry each shape by hand → `bale apply` → hand-edit
MASTER.md, sometimes through a dedicated "sitting-close-deltas"
session.

With the suite, offline (the person is the courier):

1. Walk into the office. The desk shows the folders and their next
   moves; the drafting-table shows the blueprints and what each one
   is waiting on.
2. Pick a folder. Office declares what the session carries (the
   folder, the hung items, the handbook chapters the verb names) and
   prints the pack line; a build session is packed from the project
   with the office's context riding beside it.
3. The shell shows the opener and waits for the response. Each shape
   the worker returns is carried by the person, but the shell
   renders it and records it: the probe output is pasted back, the
   light block answered, the exchange round relayed.
4. `bale apply` lands code in the project. The folder records the
   session id (`office sessions`), and a cleanup session, or the
   person, brings the folder's Next and the front sheets up to date.

With the suite, online (twine is the courier):

1–2 as above; a sitting can also be the thing that picks and packs,
    as a hosted office session.
3. Twine packs via bale and dispatches to a model session. It runs
   the probe and pastes back; answers a light block from the office's
   declarations or parks it in the escalations inbox; relays a
   clarification; applies the response.
4. On PASS twine spawns cleanup (an unattended session kind with a
   declared landing) to fold the outcome into the folder and the
   board; on HOLD the triage lands in the review inbox with the
   worker's evidence. The person sees only the four inboxes.

The records are identical on both paths — TARBALL.md §4.6's "same
contract, whoever carries it" — which is what lets the courier be
swapped for a person at any moment.

---

## 5. Session kinds

Office's `share/verbs.toml` declares each verb's `kind`, `ships` and
`writes`. This seed adds three columns — **lands** (what is
guaranteed to exist afterward), **attended** (whether a human must be
present) and **trigger** (manual, after a build lands, on a schedule,
on an event) — and the kinds below beside the seven office has
(founding, work, build, prep, meeting, cleanup, renovate). The rule:
**a kind with no declared landing cannot be spawned unattended.**

| kind | packed from | ships | lands | attended | trigger |
|---|---|---|---|---|---|
| sitting | office | drafting-table, desk, hung items | blueprint and board deltas, a notepad page, the bundles it authors | yes | manual |
| chat | office (a folder, or one auto-opened) | the folder, hung items | the transcript into the folder; nothing else guaranteed | yes | manual |
| cleanup (exists, by hand) | office | desk, notepad, suggestion-box, handbook, plus bale's records read from the projects | folders' Next, front sheets, board rows, filed slips | no | after a build lands, or a schedule |
| digest | office | drafting-table, desk, project telemetry (read) | the sitting-open page | no | before a sitting |
| review | project | the held staging diff, the HOLD's evidence | a triage record: correctable, escalate, or fixture defect | yes | on HOLD |
| check | project | the landed change and the brief, never the oracle | an independent verdict as a claims block | no | policy (effort) |
| retry | project | the failure context; spec, never oracle mechanics (PLANNER.md §5) | the corrected response with `corrects:` lineage | no | on a correctable HOLD |

Kept chats are the `chat` kind with the transcript as its declared
landing. Background updating is `cleanup` with `trigger =
after-build`. Neither touches filed paper (OFFICE.md §15 already
guards it). Where a chat's transcript lands, and whether a chat with
no folder auto-opens one, is open (Q-3).

---

## 6. MASTER.md — the protocol register, first pass

MASTER.md is bale-src's development record: 12,476 lines, eight
sections, maintained by hand at every sitting. It is not content to
file; it is a hand-run machine. This first pass inventories the
*kinds* of protocol it carries, from what was read at the sitting
(the header, §1–§3 in full, board row 10, parts of §5), so the audit
sessions (N9) start from a shape rather than a blank page. It is
not the register; the audits produce that.

| MASTER.md protocol | What it does today | Candidate office home | Kind |
|---|---|---|---|
| "Last landed by" line, edited in place, never appended | Marks which session last touched the record | Read from bale's registry per project; never hand-edited | bale already |
| Going-forward convention: sittings write records, rows, evidence, contracts; no narrative accretes | Declares what a sitting may land | The sitting verb's `writes` | shape |
| Board rows: number as identity, title, status, sids, dated `[bracket]` annotations, **What / Why / Scope hints**, "rides row N", "consumed at" | The work queue and its history | `folder.md` gains the fields; `office desk` orders by dependency; "rides" attaches a folder item to another folder's session | shape |
| Watches: source, re-trigger condition, `[date: FIRED / NOT fired / consumed]` history | Named re-triggers that never expire on their own | A drafting-table register; `office watches check` runs the mechanically checkable conditions against bale stats and reports the rest for judgment | shape + judgment |
| Fold-in registry: worker `notes.md` Proposals queued onto rows | Routes what workers noticed into the queue | The suggestion box: cleanup reads landed responses' Proposals and files slips | shape |
| §5 contracts: dated, sourced to a sitting, "do not re-litigate casually" | The rulings register | A decisions ledger on the drafting-table with date and sitting sid; the natural `amendment_target` for exchange answers | shape |
| §6 evidence pile: numbered, append-only, cited by number | Longitudinal proof behind rulings | A numbered ledger marked filed paper, cited by number | shape |
| §2 per-arc residual summaries; condense to git at milestones | Keeps the record readable | Never condense: an arc's folder goes to the filing cabinet whole; the blueprint keeps the summary | shape (office's rule is stronger) |
| Upward report: partition landed / ratified / escalated / on-watch, claims block, consumed vs deferred scope, proposals | Closes an arc | A blueprint's close template | shape |
| Sitting-open: provenance version check, stats digest, "digest over dump" | Grounds a sitting cheaply | `office digest` | shape |
| Calibration triggers: three same-class events in a rolling window | Decides when a calibration sitting is due | `office watches check` over bale stats, thresholds as data | shape |
| "Ultimate goal, ratified — do not re-litigate" | Pins the charter | Profile Purpose plus a ratified flag on a blueprint's charter | judgment |
| §7 standing environment facts and landmarks | Facts about the machine and the repo | The survey (exists) plus a landmarks section per project | mostly exists |
| End at milestones; one master per sitting; predicted refusals are control flow | Practice | Already PLANNER.md §6 and §13 | drop (bale's docs) |
| Cadence rulings (doc-only sessions bump-exempt) | A project rule | The project's ADRs or the office's house rules | judgment |
| §8 findings register: finding → disposition table | Traceability from an audit to the work it queued | A filed ledger page cross-linked to folders | shape |

*Note, 2026-09-29 (`2026-09-29-suite-merge-001`).* Both audits applied
on 2026-09-28 (`2026-09-28-master-audit-queue-001`,
`2026-09-28-master-audit-ledger-002`); their registers under
`registers/` are the register of record and supersede this first
pass, and `blueprints/drafting-table.md` is the merge. The table above
and the extraction plan below stand as written; the sitting accepted
the audits' errata as found:

- §4 has 133 rows, not 343. The queue audit: "The seed's 343 is the
  whole-file count of `^[0-9]+\. \*\*` — 133 board rows plus 210
  numbered evidence entries in §6."
- §6 has 210 numbered entries, 10–219, contiguous, with entries 1–9
  carried as one paragraph; the plan's 219 is the last number, not the
  count.
- §3 is mostly sitting-close narrative: forty `Landed <date>, …` blocks
  make 3,645 of its 5,489 lines. The queue audit: "the per-sitting
  narrative the header's going-forward convention says no longer
  accretes in §2. It accretes in §3 instead."
- §6 is not append-only at the body level. The ledger audit: "Nineteen
  dated `[YYYY-MM-DD: …]` appendices and eleven running occurrence
  counts are written into entries at later sittings. Numbers are
  append-only."
- Condensation reached §5 and §6, not only §2. The ledger audit: "§5
  opens with a `Carried forward:` paragraph of pre-v4 rulings with no
  dates and no sources; §6's entries 1–9 are one paragraph."
- §7 is a third environment facts. The ledger audit: "The rest is
  version landmarks (bale-already) and desk-practice rules that
  accreted there — include rules, forecast rules, dispatch checks,
  "one-apply-behind held for" instances." The "mostly exists" row is
  three kinds, not one.
- §5's 117 rulings have no ids. The ledger audit: "117 bold leads,
  cited by name in prose. The seed's `amendment_target` for exchange
  answers has nothing stable to point at until they do." (Q-12.)
- The board row's real field set is, in the queue audit's words,
  "number, title, status, date, a class parenthetical, a source, sids,
  and dated brackets." What / Why / Scope hints, "rides row N" and
  "consumed at" belong to the fold-in registry: "On the board they are
  rare (21 labels on 9 rows; one "rides row"; two "consumed at"). In
  the fold-in registry they are the norm (75 labels; 83 "rides"; 59
  "consumed")."
- The table's compound kinds ("shape + judgment", "mostly exists",
  "drop (bale's docs)") are not register kinds; the registers use four
  (Q-10). The fold-in registry's home is not the suggestion box
  (Q-11).

**The extraction plan** (N9). Two audit sessions, packed from this
repo, each landing one register file under `registers/`:

- **master-audit-queue** — §3 (lines 133–5621: in flight, watches)
  and §4 (lines 5622–8713: the board, 343 numbered rows). Reads by
  structure — headings, `^[0-9]+\. \*\*` row headers, `^\s*\[20`
  dated bracket annotations, `\*\*What:\*\*` / `\*\*Why:\*\*` /
  `\*\*Scope hints:\*\*` field labels, "rides", "consumed at",
  "Re-trigger:" — reading a row whole only when its shape is new.
  Lands `registers/queue-protocols.md`.
- **master-audit-ledger** — the header (lines 1–21), §1, §2, §5
  (lines 8714–9728: 36 "New, ratified" blocks), §6 (lines
  9729–12037: 219 numbered evidence entries), §7 (lines
  12038–12460) and §8 (lines 12461–12476). Same structural reading.
  Lands `registers/ledger-protocols.md`.
- **merge** — authored after both land, derived from the two
  registers: office-src's blueprint for the drafting-table space,
  its verbs and its read side. Not authored by this seed.

Each register row carries: the protocol's name; a MASTER.md anchor
(heading or line range); what it does; the kind — `shape`,
`judgment`, `bale-already`, or `content`; the candidate office home
(a space, a verb, a template field, a check, or a doctrine line);
what is mechanically checkable about it; and open questions. The
audits move nothing.

---

## 7. The interface matrix

Four cells per tool, one rule: **each tool is a core with a command
registry; every surface is a client of the registry; every transport
is a courier plugin.**

| | CLI | UI |
|---|---|---|
| **bale** | `bale` (exists) | none of its own; the shell renders its records |
| **office** | `office` (exists) | the shell's home screen and folder views |
| **twine** | `twine` | the shell's session pane and inboxes |

| | offline | online |
|---|---|---|
| **twine** | the person is the courier: the shell emits the opener and takes the response | twine drives a model over an API (Anthropic first; adapters later) |
| **office** | open — Q-2 | open — Q-2 |

Registries: office's `share/verbs.toml` already is one; bale's
subcommand table is nearly one; twine's is designed as one from the
start. The parity test walks each registry against the shell's
actions; a verb marked CLI-only is listed, never silently absent.
Twine drives bale only through bale's non-interactive paths (`--json`,
`--no-interact`, bundles, pre-answered intents, the admission
flags): the moment a harness drives an interactive prompt, parity is
gone. The same rule binds office and twine: no prompt without its
flag twin.

---

## 8. Open questions register

Each entry carries the recommended default from the sitting. An
answer accretes here, dated, and ships verbatim into the request it
affects.

- **Q-1 — The planning chat is a hosted office session.** Asked
  2026-09-28; the architect: "I would assume so but I'm open to more
  discussion." Recommended: yes — a sitting is an office session
  that twine hosts; its words land in the notepad, its plans on the
  drafting-table; twine keeps nothing of it but the mechanical
  streams. Consequence if yes: `harness-seed.md` Q-4 (chat
  persistence) is answered.
- **Q-2 — What "offline" and "online" mean for office.** Asked
  2026-09-28, unanswered. Recommended reading: local-repo-only
  versus reachable from another machine (the work office on
  docker.medgen driven from chordsphere's shell). The other reading
  — local model versus cloud API — is a twine adapter question, not
  an office one.
- **Q-3 — Where a chat lands.** Asked 2026-09-28, unanswered.
  Recommended: a chat with no folder auto-opens one on the desk; the
  transcript lands in the folder (the folder already holds "the
  conversation that started the job"); the notepad stays the
  occupant's words only; cleanup files it.
- **Q-4 — Sittings write to the office directly.** Asked 2026-09-28,
  unanswered. Recommended: yes — a sitting packed from the office
  forecasts `drafting-table/` and `notepad/`, which collides with no
  project worker (different repo), and lands its own plan; bale-src's
  "sitting-close-deltas" ceremony (nineteen sessions to date)
  retires with it. The read-only rule for sittings predates
  ADR-0015; since then only writes lock.

  [2026-09-29: answered "as assumed" to the sitting's light block [1],
  carried in the brief of `2026-09-29-suite-merge-001`: "yes; the
  close blocks become notepad pages plus cleanup". Sittings write
  `drafting-table/` and `notepad/` directly, and the sitting-close
  ceremony retires with them. The sitting kind is
  `blueprints/drafting-table.md` §5.]
- **Q-5 — Where spend lands.** Carried from `harness-seed.md` Q-8:
  bale's telemetry has carried an all-null `attempts[].cost` block
  since 0.4.6 with no verb to fill it. Either bale grows an input
  (a linked pair, bale-side) or spend lives twine-side only.
  Recommended: both — twine's stream is the owner, bale's block a
  mirror, so the "twine holds no intent" test (N4) reads spend as
  the one thing twine owns.
- **Q-6 — Trust grants as house rules.** Proposed at the sitting:
  a grant ("code work in project X runs at rung 3") is a house rule
  in the office's profile; office holds the policy, twine reads it,
  bale's telemetry is the evidence it is granted on. Not yet
  discussed.
- **Q-7 — The read side's contract with OFFICE.md §10.** §10 says the
  office "never copies what bale records." Reading and rendering is
  not copying, but the doctrine line should say so once the read
  side exists: the office renders bale's records, and its renderings
  are derived, never authoritative.
- **Q-8 — The rename.** `~/tedder-src` → twine; `harness-seed.md`'s
  references; whether that file is superseded by this seed or kept
  as twine's own seed under it. Recommended: kept, as twine's, with
  a header pointing here and D9/D22 marked retired by N4.
- **Q-9 — Metaphor.** bale and twine are hay; the office is a
  building. The architect declined the agent's earlier metaphor
  proposals (office-src sitting, messages 7–8); nothing here depends
  on resolving it.
- **Q-10 — The register's kind vocabulary.** Asked 2026-09-28 (the
  sitting's light block [2]).

  [2026-09-29: answered "as assumed" — "four; the queue audit's split
  of one seed row into five is the right shape". The kind column stays
  `shape`, `judgment`, `bale-already`, `content`, with no compound
  kinds; a row whose shape the office's stronger rule makes
  unnecessary stays `shape` with "home: none". Pinned in
  `registers/README.md`.]
- **Q-11 — The fold-in registry's office home.** Asked 2026-09-28 (the
  sitting's light block [3]).

  [2026-09-29: answered "as assumed" — "yes; slips stay friction
  reports as OFFICE.md 5 defines them". Small carried work lives on a
  riders page on the drafting-table plus a `Riders` section in
  `folder.md`, not in the suggestion box. `blueprints/drafting-table.md`
  §1 and §2.]
- **Q-12 — Stable ruling ids.** Accepted 2026-09-28 from
  `2026-09-28-master-audit-ledger-002`'s Proposals; open, recorded
  2026-09-29. Recommended: every ruling on the drafting-table's
  rulings ledger carries an id of the form `YYYY-MM-DD-slug`, minted
  when the ruling is written and never changed; an exchange answer's
  `amendment_target` names the id of the ruling as first minted.
  MASTER.md §5's 117 rulings get ids when their content is filed, not
  before (N3). `blueprints/drafting-table.md` §1 says why that shape
  and not a number.
- **Q-13 — `office watches check`.** Accepted 2026-09-28 from
  `2026-09-28-master-audit-queue-001`'s Proposals; open, recorded
  2026-09-29. Recommended: the check starts from the seven
  machine-evaluable watches the queue register names, each with its
  `bale stats` query and threshold as data; the four conditions that
  need a datum bale does not stamp today are slips for bale-src and
  are never guessed office-side (OFFICE.md §10).
  `blueprints/drafting-table.md` §3.
- **Q-14 — The close-by-reversal check on every ledger write.**
  Accepted 2026-09-28 from `2026-09-28-master-audit-ledger-002`'s
  Proposals; open, recorded 2026-09-29. Recommended: inherit it as the
  office's check on every write to filed paper, whichever verb does
  the writing — a `validation.sh` fragment in every session that
  forecasts filed drafting-table or notepad paper, the same check
  in-process in the scripts that append to it, and `office status`
  re-checking git after the fact. It depended on Q-4, now answered.
  `blueprints/drafting-table.md` §5.

---

## 9. What this is not

Not a change to bale: the five global docs, the wire format and the
verbs are untouched, and no obligation here lands bale-side.

Not a replacement for `doctrine/OFFICE.md`: that doc governs the
office as built; this seed changes what the office *also* holds
(section 3.2) and the session-kind table (section 5), and nothing
else in it.

Not a harness design: twine's mechanism — the loop, the sandbox, the
adapters, the transition table — is twine-src's, and `harness-seed.md`
stays its input material under the standing rule.

Not a shell design: the shell's contents are section 3.4; its
rendering is a later decision in nisaba-src.

Not autonomous, yet: PLANNER.md §18's trust phasing stands, and every
rung is proven by hand before twine inherits it.

---

## 10. The road from here

In order. Each session is authored as a bundle beside its `bale open`
line; the two audits are authored with this seed.

1. **master-audit-queue** and **master-audit-ledger** — packed from
   this repo, side by side (disjoint forecasts), MASTER.md and
   office's doctrine riding beside each as context tarballs.
2. **merge** — derived from the two registers: office-src's blueprint
   for the drafting-table, its verbs (blueprint, board ordering,
   watches, `digest`, `watches check`) and the verb-table columns of
   section 5.
3. **office-src: the drafting-table** — the space and its verbs.
4. **office-src: the read side** — `office desk` and `office digest`
   rendering bale's records across the office's projects.
5. **The Nisaba office** — founded; then cleanup sessions file
   MASTER.md's content, one per repo's `claude/`.
6. **twine-src: the core and its registry** — the courier first
   (offline: emit and take; online: the loop), the cost spine and
   kill-switch with it; then the scheduler over the drafting-table.
7. **nisaba-src: the shell** — walking in, folders, the session
   pane, the four inboxes; parity test against the three
   registries.

[2026-09-29: steps 1 and 2 are done. The two audits applied on
2026-09-28 (`2026-09-28-master-audit-queue-001`,
`2026-09-28-master-audit-ledger-002`); the merge is
`2026-09-29-suite-merge-001`, which pinned the register anchor grammar
and landed `blueprints/drafting-table.md`, the input to step 3. That
blueprint's §8 cuts steps 3 and 4 into four office-src sessions.]

---

## 11. The sitting's words, verbatim

Session `2026-09-28-open-discussion-001`, packed read-only from
bale-src on chordsphere. Every message the architect typed, in order.
Probe outputs were attached as files and are elided; the two probes
read `~/office-src`, `~/tedder-src` and `~/tedder-src-v0`, and
office's doctrine, catalogs and construction sitting.

Message 1 (the session opener; the goal is the manifest's, verbatim):

> I'm using "bale", a CLI that packaged the attached request tarball.
> This message opens read-only bale session 2026-09-28-open-discussion-001
> (empty write forecast: an orchestration/discussion session — no changes land from it).
> Goal, verbatim from the request manifest: before we design the harness, I'd like to define the overall product I'm creating here. My current vision, which is what I want to discuss and criticize, is a suite of tools under the name 'Nisaba'. The three tools I have in mind are bale, twine (the harness and UX), and office (underdeveloped, probe ~/office-src for more info). It's a little fuzzy exactly how it will work in practice, but the seams are clear to me. Office contains all the meta information and controls the separation between what shows to what audience. Ideally, bale and twine would be operated from office (not sure how this works with twine being the UX as well). So office hits twine, twine packs bales, everything gets returned to office for distribution. The seams make sense to me (but push back if it doesn't to you), I'm just struggling to envision the final tool and how everything will work. Ideally i'd like a UX AND a CLI to both be capable of the same thing, buy I still don't see the flow.
> The docs and tools in the tarball are mine, written for this workflow;
> AGENT.md and the four docs beside it are my instructions for this
> session. Read manifest.json first, then AGENT.md; AGENT.md says when
> the other four docs are needed. tools/craft_response.py and
> tools/response_lint.py are stdlib-only formatters with no network
> access — conveniences over the docs, which are the contract; read them
> before you run them, and a response assembled by hand is just as
> valid.
> Packed at 2026-09-28T12:23:57+00:00 (UTC).
> bale's dates are UTC and can run a day ahead of this chat's date (a timezone gap, not an error); date what you write from the session id.
> If you need something from me, a fact from my machine or a decision,
> end that turn with the matching block from TARBALL.md (a probe, a
> light question block, or a clarification response) rather than a
> question in prose, which tends to get lost. This is a planner session:
> nothing lands from it, so don't build a response tarball, even an
> empty one. What I need back is your answer in chat and, for each
> session I ask you to author, a crafter bundle with its bale open line,
> as PLANNER.md describes.

Message 2 (with the first probe's output attached):

> one note, 'tedder' is the name i had previously for twine, and I haven't updated it anywhere yet. So ~/tedder-src still contains some harness docs as well

Message 3 (with the second probe's output attached):

> Do you think "MASTER.md, mechanized" is necessary to have? Am I missing a component or should that live somewhere else?
>
> Don't worry about the previous harness or office ratifications, we're redesigning everything but the core of bale here.
>
> It's interesting you had a different picture, can you describe where the two deviate, where the strengths in both are, and how/if we could merge them?

Message 4 (answering the light block: [1] one engineering office with MASTER.md's board on its drafting-table; [2] twine's core headless with a CLI twin; [3] the planning chat as a hosted sitting):

> I want to note that MASTER.md is NOT currently a part of the bale tool, only bale-src and meta development. the only docs bale ships are the 5 globals.
>
> I do really like the idea of merging the intent of MASTER.md with the intent of office, i think the two are related and i didn't see that before.
>
> I also like the idea of automatically keeping chats and possibly even auto updating office/MASTER.md in the background. If this is the case, we need more session-type definitions so we don't hit a snag
>
> for "the seat", I disagree that twine is "web". I want both offline and online options for both, and I also want CLI and UI interfaces for both
>
> answers:
>
> 1. i'm not sure and I want to discuss more, in simpler terms. I want Nisaba's first project to be Nisaba
> 2. answered above i believe
> 3. I would assume so but I'm open to more discussion

Message 5 (the light block it followed — [1] sittings write to the office directly; [2] the meaning of offline/online for office; [3] a folderless chat auto-opens a folder — was not answered and stands open as Q-4, Q-2 and Q-3):

> First, I need to do much more work on office before I start a nisaba office. The point of office-src was to dogfood while I develop it, like bale-src.
>
> second, I kind of disagree with just the idea of "hanging MASTER.md". MASTER.md has a bunch of well tested protocols for stuff that office is supposed to do mechanically and I'd like to extract all of that I can before just hanging it as a non-core file
>
> Is the UI a separate repo? does UI live in the respective src directories?

Message 6 (answering the light block: [1] the UI as one shell in nisaba-src; [2] two audit sessions split at §4/§5; [3] author the audit bundles now):

> 1. yes
> 2. yes
> 3. yes, you currently hold the most comprehensive, and really only, documentation for how i want the three tools to work. If you don't immortalize what we've gone through in this session then it will be lost and have to be rederived

### How the sitting ended

The suite has four components, dependencies pointing down: bale
(unchanged) carries sessions; office declares what a session carries
and, newly, holds a project's progression; twine carries and
schedules without holding intent; one shell in its own repo renders
all three. The seam is ownership, and role projections ride it as
verb declarations. MASTER.md is a hand-run machine to be extracted
into office verbs before its content is filed; two audit sessions
were authored to inventory it. Both tools get CLI and UI, offline and
online. Nisaba's first project is Nisaba, once office can carry it.
Probes emitted: two, both answered. Light blocks emitted: three;
dispositions — block 1 (engineering office; headless twine; hosted
chat) answered inline; block 2 (sittings write directly;
offline/online; chat landing) unanswered, carried as Q-4, Q-2, Q-3;
block 3 (shell repo; two audits; author now) answered inline.
