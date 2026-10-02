# notes — 2026-10-02-nisaba-twine-faces-001

## Re-attempt after HOLD (corrects the held response)

The first attempt held on one check: "only nisaba-seed.md differs from git HEAD".
Every check on the work itself passed. The failure was in my script. Bale's
staging tree is its own git worktree, and bale places `validation.sh` in it before
running it, so `git status` listed `?? validation.sh` beside ` M nisaba-seed.md`.
My filter exempted `.bale-manifest.json` and the logs but not the script. My local
test missed this because I ran the script from outside the test tree.

The fix: the tree check now also ignores the script's own path, worked out from
`$0` relative to the working directory, not assumed by name. Nothing else is
newly exempted. `nisaba-seed.md` under `files/` is byte-identical to the held
response (sha256 `646253b0…`); only `validation.sh` changed. I retested with the
script copied into each test tree and run from there, the way bale runs it: the
staged tree gives 8/8 with every claim agreeing; the unmodified tree fails the
placement checks, the reversal and the tree check; a tree with an extra
untracked file still fails the tree check; and a copy nested inside the repo
without its own `.git` skips with the reason.

## Receipt

`nisaba-seed.md` hashed to `16dd24473aadf69d9e0b12ce3ef5ca3d0eea73c59f092007cc29f55fb4c63d0e`
(44,488 bytes) on receipt, matching the brief. All three anchors were where the
brief said, so nothing had to be placed by phrase alone.

## Where each annotation landed (line numbers in the shipped file)

| | Lines | Neighbors |
|---|---|---|
| A1 | 292–304 | after §3.3's last paragraph and its blank (290–291); one inserted blank at 305; `### 3.4` at 306 |
| A2 | 589–594 | inserted blank at 588 after the Q-8 bullet text (584–587); `- **Q-9` at 595 |
| A3 | 698–705 | after §10's `[2026-09-29: …]` paragraph and its blank (691–697); one inserted blank at 706; `---` at 707 |

30 lines inserted (27 of annotation text, 3 blank); 44,488 → 46,243 bytes. Delete
exactly those 30 lines and the file hashes to `16dd2447…` again; that reversal is
`validation.sh`'s insertions-only check. I took the three texts mechanically from
the brief's `text` fences, not by retyping, and the fixtures in `validation.sh`
are pinned to the sha256 of those fence bytes.

## One placement call to ratify: A2's trailing blank line

The brief says A2 goes in "with a blank line on each side (the form beneath
Q-4)". Those two halves disagree. Beneath Q-4 (and Q-10 and Q-11) the seed puts a
blank line *before* the annotation and none after it: the next bullet follows
directly. No bullet in §8 has a blank line in front of it. I followed the seed's
actual form, since matching it is what the brief was after. CommonMark renders
both the same, because §8's list is already loose. If you meant a literal blank on
both sides, it's a one-line insertion before line 595, and the reversal check's
`b"\n" + a2` piece would become `b"\n" + a2 + b"\n"`.

## Flags: where the new texts sit against the seed as it stands

These are flags, not edits. Each one is unannotated text elsewhere in the seed
that a reader will now find out of step with one of the three paragraphs.

1. **Twine still has two faces outside §3.3.** A1 makes the runtime the third
   face and says "N4 is unchanged." That holds for N4's substance (holds no
   intent; the deletion test). But N4's own heading (line 132) reads "courier and
   scheduler, headless, holding no intent". §1's component bullet (lines 58–60)
   gives twine as "The courier … and the scheduler". The layer-cake diagram (line
   70) says "process: courier + scheduler". Only §3.3 carries the pointer, so a
   reader entering at §1 or §2 meets two faces.
2. **The cost spine moved faces, and §10 step 6 doesn't say so.** Step 6 (lines
   684–686) has "the courier first …, the cost spine and kill-switch with it; then
   the scheduler". A1 puts the cost spine and kill-switch in the runtime, and A3
   makes the runtime its own arc after the courier. So step 6's "with it" now
   points at the wrong arc. A3 records the changed arc order but not where the
   cost spine went.
3. **A2 versus N10 (ratified).** N10 ends: "The repo is still `~/tedder-src` …
   The rename of the repo and of `harness-seed.md`'s references is a session of
   its own and is not scheduled by this seed." A2 says "there is no rename" and
   that `~/tedder-src` stands as archive. N10's actual ruling (the name tedder
   retired for twine) survives. Its closing sentences are superseded with nothing
   beneath N10 to say so. Separately, A2 answers Q-8 differently from Q-8's
   recommendation: a fresh `twine-seed.md` derived from `harness-seed.md`, not
   `harness-seed.md` kept as twine's with a header. That's an answer, not a
   contradiction, and it agrees with §3.3 and §9 treating `harness-seed.md` as
   input material.
4. **A3 and §10's "In order".** §10 opens with "In order", and step 5 (found the
   Nisaba office; then the cleanup sessions) sits between step 4 and step 6. A3
   records steps 3 and 4 done and step 6 begun, and says nothing of step 5. Either
   step 5 is under way and A3 is silent about it, or step 6 started ahead of it.
   The second would reorder the road itself, beyond the within-twine arc order A3
   says was ratified. N8's precondition for founding the office (the
   drafting-table and the read side exist) is met by A3's own account.
5. **Minor.** A3 lists step 4 as "the read side and the desk verbs". Step 4 names
   `office desk` *and* `office digest`, and I can't tell from here whether digest
   landed. §3.2's "As built (office-src 0.2.0 …)" now describes a build three
   minors behind the 0.5.0 that A3 cites. That's dated text, not wrong text, but
   readers will notice.

I can't verify what the texts cite in twine-src (`twine-seed.md` T1, T4–T7 and
T11, and the quoted "a scheduler before a runtime would only have a person to
dispatch to"), because none of it ships in this request. I placed those words as
given.

## Validation, as run here

I ran `validation.sh` on a simulated staging tree (the request's `context/` as a
git repo, `files/` overlaid, `.bale-manifest.json` in place): 8/8 pass and every
claim agrees. On the unmodified tree, the three placement checks, the reversal
and the tree check fail, as they should. Two checks pass on both trees: UTF-8 and
no TODO. They're there because the brief asked for them, as guards, and are not
evidence of the change. The UTF-8 check is unclaimed as file syntax; the no-TODO
check is claimed. I also checked that a one-byte change inside A2 fails both A2's
check and the reversal.

The tree check runs only when the staging directory is itself the top of a git
worktree. A plain copy under `<repo>/.bale/staging/` would otherwise read the
*real* repo's `git status`, so in that case it prints `[SKIP]` with the reason. I
tested both cases, and bale's own reconciliation covers the tree either way. The
HOLD settled which layout bale uses: staging is its own git worktree, so the check
runs and its claim should reconcile `[agree]`.

## Proposals

- **What:** a follow-up annotation session for flags 1–3: dated paragraphs
  beneath N4, beneath §1's component list (or the diagram) and beneath N10, plus
  a word on step 6's cost spine, each pointing at A1/A2 rather than restating
  them.
  **Why:** the seed is the later ruling over the suite. Right now its two most
  likely entry points (§1 and the N-rulings) still describe twine with two faces
  and a pending rename, and only a reader who reaches §3.3 or Q-8 finds the
  update. Insertions beneath N-rulings keep their bytes, so this session's
  constraint holds there too.
  **Scope hints:** `nisaba-seed.md` only. The wording is the planner's to author,
  since this session places text and doesn't write it. Flag 4 needs a fact first:
  whether step 5 has begun.
