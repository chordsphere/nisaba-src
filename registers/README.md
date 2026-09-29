# registers/

Protocol registers extracted from bale-src's `claude/MASTER.md` by the
audit sessions the seed names (nisaba-seed.md §6, §10). Each register
is one Markdown file with one table, one row per protocol, and the
columns the seed fixes:

| column | holds |
|---|---|
| protocol | a short name |
| anchor | where in MASTER.md, in the anchor grammar below: a heading token (`header` or `§N`) plus `L<start>–<end>` line ranges of the named copy, `;`-separated when the protocol shows in several places |
| what it does | one line, in the record's own terms |
| kind | `shape`, `judgment`, `bale-already`, or `content` |
| office home | a space, a verb, a template field, a check, or a doctrine line — the candidate, not a decision |
| checkable | what about it a script could verify, or "nothing" |
| open | questions the merge session must settle |

Rows may be followed by prose; the table is the contract. A register
moves nothing: it names protocols and candidate homes.

- `queue-protocols.md` — MASTER.md §3 (in flight, watches) and §4 (the board).
- `ledger-protocols.md` — the header, §1, §2, §5 (contracts), §6 (evidence), §7 (environment facts), §8 (findings).
- `../blueprints/drafting-table.md` — not a register: the merge of these two into office-src's design for the drafting-table.

## The kind column

Exactly four values: `shape`, `judgment`, `bale-already`, `content`.
No compound kinds (ratified 2026-09-29, answering the sitting's light
block [2]): a protocol that is both shape and judgment is two
protocols and two rows, the way the queue register split the seed's
one watch row into five. A shape the office's stronger rule makes
unnecessary (condensation, say) stays `shape` and says "home: none"
in its office-home cell rather than taking a fifth value.

## The anchor grammar

Ratified at the `2026-09-28-open-discussion-001` sitting (the ledger
audit's grammar); pinned here by `2026-09-29-suite-merge-001`.

**The named copy.** Every line number in an anchor is a line of one
copy of MASTER.md, named once, here:

- `bale-src/claude/MASTER.md` as it traveled beside the audit requests
  on 2026-09-28: 12,476 lines, last landed by
  `2026-09-24-sitting-close-deltas-19-001`.

Its heading tokens and the lines each covers:

| token | heading line | covers |
|---|---|---|
| `header` | 1 | L1–21 |
| `§1` | 22 | L22–43 |
| `§2` | 44 | L44–132 |
| `§3` | 133 | L133–5621 |
| `§4` | 5622 | L5622–8713 |
| `§5` | 8714 | L8714–9728 |
| `§6` | 9729 | L9729–12037 |
| `§7` | 12038 | L12038–12460 |
| `§8` | 12461 | L12461–12476 |

A register re-anchored to a later copy names that copy in its own
preamble and carries its own token table; until one does, this copy is
the one every anchor means. Line numbers go stale the moment MASTER.md
lands again; re-derive from the headings before trusting one.

**The form.** An anchor is one or more *places*, separated by `; `:

```
anchor  = place *( "; " place )
place   = locator [ " " note ]
locator = token [ " " ranges ]  /  ranges
token   = "header" / "§" DIGIT
ranges  = range *( ", " range )
range   = "L" start [ "–" end ]        ; en dash, U+2013
note    = "(" text ")"                 ; balanced parentheses
```

- The first place opens with a token. A later place may drop its
  token and inherits the one before it: `§5 L9355–9361; L9342`.
- A range is a single line (`L5857`) or an inclusive span
  (`L135–150`); `start ≤ end`, and both lie inside the lines its token
  covers in the table above.
- A token with no range (`§5 (18 landing pointers)`) names a whole
  section; use it only when the protocol is spread through the section
  and no example range would help.
- The note is free text inside one pair of balanced parentheses at the
  end of a place: which watch, which row, a count, an example marker.
  A `;` or `,` inside a note separates nothing. Nothing else follows a
  locator — prose that is not a note belongs in the row's other
  cells.

Examples, one per shape: `header L14–15`; `§4 L8699–8712 (row 133)`;
`§3 L154–158 (watch 1); L212–242 (watch 13)`; `§7 L12190, L12210,
L12226 (forecast rules)`; `§5 (15 evidence citations)`.

What a script checks, and every register's `validation.sh` may
reuse: each anchor cell parses under the form; every token is in the
table; every range is in bounds for its token and not reversed.
