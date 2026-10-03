# notes — 2026-10-03-nisaba-seed-reconcile-001

## Receipt

Both files hashed as the brief's probe said on receipt: `nisaba-seed.md`
`646253b0…` (799 lines, 46,243 bytes) and `blueprints/drafting-table.md`
`f7bade8e…` (1416 lines, 77,164 bytes). Every "after" line in the brief's two
tables matched its shipped bytes exactly, and every end anchor was where the
brief put it. Nothing had to be placed by guesswork, so no probe went out.

I sliced the nine texts from the brief's ```` ```text ```` fences in code, never
retyping them. `validation.sh` carries them as fixtures, each pinned to the
sha256 of its fence bytes. If a fixture drifts from its fence, the script exits 2
rather than grading against the wrong bytes.

## Where each text landed (line numbers in the landed files)

`nisaba-seed.md`: 799 → 871 lines (+65 of text, +7 blank); 46,243 → 50,333 bytes.

| text | text lines | blank before (shipped) | blank after (inserted) | next line |
|---|---|---|---|---|
| S1 | 85–90 | 84 | 91 | 92, the `---` closing §1 |
| S2 | 151–157 | 150 | 158 | 159, `**N5 — …` |
| S3 | 204–222 | 203 | 223 | 224, `**N9 — …` |
| S4 | 241–245 | 240 | 246 | 247, the `---` closing §2 |
| S5 | 289–294 | 288 | 295 | 296, `What this seed adds (N3, section 6): …` |
| S6 | 755–767 | 754 | 768 | 769, S7 |
| S7 | 769–777 | 768 (inserted, after S6) | 778 | 779, the `---` closing §10 |

`blueprints/drafting-table.md`: 1416 → 1433 lines (+12 of text, +5 blank);
77,164 → 77,767 bytes.

| pointer | text lines | blank before | blank after | next line |
|---|---|---|---|---|
| P1, inside item 3 (indented 3 spaces) | 289–291 | 288 (inserted) | 292 (inserted) | 293, `4. It reads in prose. …` |
| P1, after the paragraph ending on shipped line 810 | 817–819 | 816 (inserted) | 820 (shipped 811) | 821, `**Behavior.** …` |
| P2, after the deferral table | 1255–1257 | 1254 (inserted) | 1258 (shipped 1245) | 1259, `Judgment rows homed as …` |
| P1, after the paragraph ending on shipped line 1329 | 1344–1346 | 1343 (inserted) | 1347 (shipped 1330) | 1348, `---` |

Delete exactly those 89 inserted lines (77 of text, 12 blank) and both files
hash to their shipped values again. That reversal is in `validation.sh`.

## The blank-line and indentation calls

**List item 3 (shipped lines 284–287).** I followed the brief exactly: one
blank line, P1 indented three spaces on every line, one blank line, then item
4. The list stays intact: it is still one `<ol>` of four items, P1 renders as a
second paragraph inside item 3, and item 4 keeps its number. The rendered effect
to know about: the list was tight and is now loose. All four items render
wrapped in `<p>`, so the list gets paragraph spacing between items. That can't
be avoided by changing the blank lines. Item 3 now holds two blocks separated by
a blank line, and that alone makes a CommonMark list loose. I checked that
dropping the trailing blank renders the same loose list. So I kept the brief's
form. The other choice is to put P1 after item 4, outside the list. That keeps
the list tight but loses "here", which then points at the whole list rather than
the item that holds the line.

**The table (header at shipped line 1231, last row 1244).** P2 sits after the
last row, behind one inserted blank line, and the shipped blank at 1245 follows
it. The blank before P2 is load-bearing: in GFM a line without a pipe directly
under a table row is absorbed into the table as a row. The table renders with
the same row count as before, and P2 is a separate paragraph after it.

**The two paragraph pointers** (after shipped lines 810 and 1329) and **every
seed text**: the shipped file already had exactly one blank line on one side, so
I inserted only the other blank. This adds nothing to the brief's form. I
rendered both files whole (markdown-it-py, CommonMark plus tables) before and
after. Headings, `<hr>`s, tables, lists and code blocks are identical in count.
The only differences are the new paragraphs: 7 in the seed, and 4 in the
blueprint plus the 4 list items now wrapped in `<p>`. In particular, no `---`
became a setext underline, because each text ahead of a `---` keeps a blank line
between them.

## Flags: the texts against the bytes I hold

These are flags, not edits. Every text is placed byte-verbatim.

1. **S5's "the 2026-10-02 annotation in §10" is now ambiguous.** When S5 was
   written, §10 had one 2026-10-02 annotation (A3). After this session it has
   three: A3, S6 and S7. S5 means A3, the one that says what steps 3 and 4
   landed. The context makes that recoverable, but the definite article no
   longer picks one out.
2. **S2 against A1's "N4 is unchanged."** S2 says N4's deletion test "gains one
   item" (transcripts-as-logs), where N4 itself answers "Spend history and
   nothing else." A1 (beneath §3.3, shipped) says "N4 is unchanged," meaning the
   holds-no-intent substance, and S2 agrees that the substance stands. But a
   reader who goes from S2 to A1 will see N4's test change while A1 says N4
   didn't. They don't contradict each other, but A1's wording now reads stronger
   than the two together support.
3. **P1 inside item 3 quotes "the Nisaba office" in lower case.** Line 284 opens
   its sentence with "The Nisaba office". It's trivial, but P1 presents the
   phrase as a quotation. P1's other two placements quote lower-case
   occurrences correctly.
4. **Not a text error, but stale text the pointers now sit beside.** Deferral
   rows 1241 and 1242 (landed 1250–1251) are deferred to "the Nisaba office's
   founding", with re-triggers "founding the Nisaba office (N8)" and "the same".
   P2 now says that office was founded on 2026-09-30, so both re-triggers have
   fired, and P2 doesn't say so. Row 1242's *why*, "that office has no profile
   yet", no longer holds: S3 quotes the home office's profile Purpose. Likewise
   the sentence at shipped 807–810 routes slips to bale-src's queue "until the
   Nisaba office exists". It now exists, though its suggestion box is
   presumably not the drafting-table's to use until the renovation. See
   Proposals.

I didn't re-verify the `twine-seed.md` citations (T1, T4, T5, D15, the Arc 1
correction) or the probe `home-office` facts, as the brief asked. Everything
those texts cite *inside* the seed checks out against the bytes: the component
line and diagram (S1), N4's heading (S2), N8's "a nisaba office" quotation
(S3), N10's last two sentences and A2 beneath Q-8 (S4), §3.2's "0.2.0" (S5), A1
listing the cost spine and kill-switch under the runtime (S7), and §10 step 6's
"online: the loop" (S7). The light block 6 default quoted in S6 matches the
brief's transported block byte for byte.

## Validation, as run here

I ran `validation.sh` the way bale does: copied into a tree built from the
shipped files with `files/` overlaid and a `.bale-manifest.json` in place, with
cwd at the root. The landed tree gives 15/15, with all 14 claims agreeing. On
the shipped tree, all eleven placements and both reversals fail. One check
passes on both trees: "no TODO added". It's there because the brief asked for
it, as a guard, so it isn't evidence of the change. The file-syntax check is
mechanical and unclaimed. Three mutation runs each failed exactly the check they
should:

- a one-byte change inside P2 failed P2's placement only;
- a changed shipped line in §1 (no text touched) failed the seed's reversal only;
- `TODO` appended inside S7 failed S7's placement and the TODO check.

Following the lesson of `2026-10-02-nisaba-twine-faces-001`'s HOLD, the script
makes no tree or `git status` assertion. Its only write is its own log, under
`.validation-logs/<UTC timestamp>/validation.log`, which it announces on its
first line.

## Proposals

- **What:** a short session over `blueprints/drafting-table.md` §7 rows 1241
  and 1242, and the slip-routing sentence at shipped 807–810, to record that
  their re-trigger (the founding) fired on 2026-09-30. It would also settle
  where each now goes: the charter marker into the home office's profile
  Purpose, the second-board numbering against the home office's board, and
  slips into the home office's suggestion box or still to bale-src's queue
  until the renovation.
  **Why:** P2 and P1 now tell a reader the office exists, while the rows beside
  them still read as waiting on it, and row 1242's reason ("no profile yet")
  is contradicted by S3. That's a ruling for the desk, not a pointer.
  **Scope hints:** `blueprints/drafting-table.md` only, as dated insertions
  under this repo's no-edit convention, unless the desk decides the
  drafting-table blueprint is superseded by the home office's renovation. It
  probably waits on office-src's `renovate` verb, which decides what the
  drafting-table in the home office actually holds.
