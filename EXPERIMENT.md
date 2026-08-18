# EXPERIMENT A — Top-of-Context Response Discipline Protocol

Status: DRAFTED (2026-08-18) — awaiting baseline vs experimental test run (kanban task t_c3c37540)
Branch: `soul-md-experimental`
Author: kanban task t_c5c4366d (seo-agent)

## 1. What changed

One additive section was inserted into SOUL.md immediately after the title and
before Section 1:

- `## 0. Experimental Override — Response Discipline Protocol (EXPERIMENT A)`

Nothing else in SOUL.md was modified. The diff (baseline commit → experimental
commit) is purely that insertion. Verified compatible with the nightly
`soul-evolution` cron: `scripts/soul_evolution.py` only strips/appends blocks
whose heading matches its three footer regexes (Run Log / Daily Review) and
numbers the footer from `max_section_number + 1`; a `## 0.` heading is treated
as an ordinary real section and survives unharmed.

### The four experimental directives (activated by `EXPERIMENT_A: ON`)

1. STATUS header — every substantive response opens with one line:
   `STATUS: ✅ DONE | 🔄 IN PROGRESS | ⛔ BLOCKED`
2. VERIFICATION — before claiming completion, one line naming real evidence
   (file read + path, command + exit code, test count, source consulted).
3. PROSE CAP — non-code prose ≤ 200 words per response; commands, paths, and
   evidence stay full-length.
4. SOURCE tag — when a lookup was needed, name it in one phrase:
   `source: <local-file | vault | memory | session-history | web>`

## 2. Why this experiment

- SOUL.md is ~29 KB. Hermes caps context files at 20,000 characters and
  truncates longer files head+tail, dropping the middle. Rules buried mid-file
  (e.g. "Verify before claiming" in §9, "No vague advice" in §8) may never
  reach the model.
- Hypothesis: a short, explicit directive placed in the always-loaded head
  region (Section 0) measurably improves observable output discipline —
  marker compliance, concision, and evidence quality — compared to the current
  SOUL.md where equivalent guidance sits far down the file.
- The directives are deliberately phrased as measurable behaviors so a test
  run can score them objectively.

## 3. Safety analysis (why this is safe to test)

- Additive only: protected zones (Sections 1, 1.5, 1.6, 10 per §12 rule 4) are
  untouched; no existing content moved or deleted.
- Cron-owned sections (2, 21, 22) untouched; the nightly script preserves the
  new section (verified against its source).
- Flipping the experiment off is a one-line edit (`EXPERIMENT_A: ON` → OFF) or
  full revert via the rollback paths below.
- No config, plugins, skills, or runtime behavior changed — only the identity
  document.

## 4. What the test run should measure

Suggested metrics for the baseline vs experimental run. The authoritative run
protocol, 5 sample tasks, and scoring rubrics live in
`SOUL-experiment-test-plan.md` (repo root, written by kanban task t_0ec26fe1);
the table below is a quick reference for the markers this experiment
introduces:

| Metric | How to score |
|---|---|
| STATUS marker compliance | % of responses whose first line matches `STATUS: ✅/🔄/⛔` |
| VERIFICATION line present | % of completed-task responses containing a `VERIFICATION:` line with concrete evidence |
| SOURCE tag present | % of lookups that name the source consulted |
| Prose length | words of non-code prose per response (target ≤ 200) |
| Task completion | baseline vs experimental pass rate on same sample tasks |
| Output quality | 1–5 rubric on clarity/actionability, blind-scored if possible |

No-response-edge-cases (pure-code outputs, one-word acknowledgements) should be
excluded from marker scoring.

## 5. How to run baseline vs experimental

Both versions are committed on `soul-md-experimental`:

```
# baseline (pre-experiment live SOUL.md, footer refreshed 2026-08-18T16:29)
git show <baseline-commit>:SOUL.md > SOUL.md

# experimental (Section 0 added)
git checkout <experimental-commit> -- SOUL.md
# or simply: the working tree of this branch already holds the experimental version
```

The un-committed convenience copy `SOUL.md.original` at the repo root is the
same content as the baseline commit.

Caveat to testers: if the daily `soul-evolution` cron (23:00) or the Dojo
daily job runs mid-experiment, SOUL.md's sections 2/21/22 will be rewritten by
design. The Section 0 experiment survives; re-commit or diff-loose those
footer-only changes before scoring. Also note Hermes reads SOUL.md at session
start — start a fresh session per run (e.g. `hermes --ignore-rules` for a
clean control when isolating SOUL.md effects).

## 6. Rollback (three independent paths)

1. `cp SOUL.md.original SOUL.md` (repo root copy of the exact baseline)
2. `git checkout <baseline-commit> -- SOUL.md`
3. Delete Section 0 from SOUL.md (works for the flag flip too: set
   `EXPERIMENT_A: ON` → `OFF` and the directives are inert)

## 7. Repository state

- Branch `soul-md-experimental` created from `master` (d50945c), carrying the
  uncommitted nightly-update changes present in the working tree at branch time.
- Commit 1 — `chore: snapshot live SOUL.md as experiment baseline`: SOUL.md
  (live state incl. refreshed footer) + SOUL.md.original + this file.
- Commit 2 (PENDING human approval) — `feat: add experimental SOUL.md Section 0`:
  the Section 0 insertion into SOUL.md. The write was refused by Hermes's
  protected agent-instruction consent gate (headless worker = no one to approve
  the prompt). See the kanban block on t_c5c4366d for the exact text to approve
  or apply.

See also: kanban t_c5c4366d (this draft), t_0ec26fe1 (test plan), t_c3c37540
(test run), t_4e27317b (report + PR).