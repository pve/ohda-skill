---
name: ohda
description: Run non-trivial technical troubleshooting/diagnosis as an OHDA loop (Observe → Hypothesize → Decide → Act) with a replayable worklog. Use whenever you're about to debug or diagnose something where the cause isn't already obvious — an error, an unexpected state, a "why is X broken" — and more than one quick check will be needed. Not for trivial one-shot fixes (typo, single obvious command). Also handles closing out a worklog into a "lesson learned" (TL;DR + dead-ends kept, crossed out, not deleted).
version: 1.1.0
---

# OHDA method

Source: Peter van Eijk, "Professional IT troubleshooting, simplified" (Club Cloud Computing).
See `references/CHANGELOG.md` for what's changed between versions of this skill itself.

## Why

"A professional is somebody who uses an approach shared by other professionals — reliable,
consistent, scalable. Amateurs do it their own way; alone you go faster, together you go
further." The OHDA loop and its worklog are what make a diagnosis session **replayable by
somebody else** (a colleague, or you in two weeks) — every step must be understandable and
re-doable by a reader who wasn't there.

## The loop

Troubleshooting is a loop through four steps, repeated until the observation matches
expectation. **Enforce the order — don't skip ahead to acting before hypothesizing and
deciding are written down.**

1. **O — Observe.** What do you see that you don't expect, or expect that you don't see?
   Result: a description of the situation, concrete enough that someone else could reproduce
   or at least review it. Copy/paste actual output — don't paraphrase.
2. **H — Hypothesize.** Research possible causes. Sources: your own mental model of how the
   system *should* work (decompose it into parts — each part is a hypothesis that it's the
   broken one), search engines/error messages, earlier OHDA logs on a similar problem, asking
   someone. Document search terms. **Prefer 2-3 candidate hypotheses over one** — result must
   be a credible, understandable-by-others idea of the cause.
3. **D — Decide.** Before doing anything, write down the 2-3 best candidate actions. A good
   action is hypothesis-driven, easy to execute, quick-turnaround, informative, and plausibly
   successful — usually a trade-off between "easy" and "informative". Every candidate action
   should either solve the problem or produce more relevant information; if it does neither,
   it's not worth the slot.
4. **A — Act.** Execute your best shot, and make it traceable/replayable (e.g. record the
   exact command, a git commit id). Record the result *before* moving on.

**Every `A:` is immediately followed by an `O:` that closes the loop against the hypothesis
it tested** — not just "here's the output", but an explicit verdict: what you now see, what
you expected, and whether the hypothesis is accepted or rejected. E.g. `O: permissions are
000, not 644 as expected → H "wrong permissions" accepted`. This is what makes the log
replayable reasoning rather than a bare transcript — a reader can follow *why* the loop moved
on, not just *that* it did. That `O:` is also the seed observation for the next iteration.

Stop when the observation matches the expectation. Otherwise, loop again — most real
diagnoses take multiple passes.

## The worklog

One growing text file per topic, append-only in spirit (dead-ends get struck through later,
never deleted). Every line is prefixed `O:`, `H:`, `D:`, or `A:` so the loop-step is visible
at a glance; consider a distinct style/color for raw computer output vs. your own typed notes.

**Header, once, at the top:**
- Title of the problem
- Objective — what "done" looks like
- Author, start date
- A `TL;DR` section (empty until step "Closing out", below)

**Discipline while working:**
- Log every action and result *as it happens* — before it happens, if you can (write the
  planned `D:` before the `A:` that executes it).
- Copy/paste and link liberally: URLs, screenshots, full command lines. Type commands into
  the log first, then copy them into the terminal — not the other way around. That makes a
  wrong command trivial to fix and retry, keeping the log the source of truth for what was
  actually run.
- Include rabbit holes. They warn the next reader off the same dead end — or turn out not to
  be a dead end after all under a slightly different approach.
- A shared location (visible to a teammate) is a feature, not a nice-to-have — give someone
  else a chance to jump in.

**Filename convention:** `OHDA log, <date> <topic>` (or a filesystem-safe variant of that,
e.g. `ohda-<topic>--<date>.md`) — consistent naming is what makes old logs findable later,
including as a `H:` source for a future, similar problem.

**Where the file lives:** this skill is project-local by design — it does not hardcode a
path. Before starting a new log:
1. Check the project's CLAUDE.md (or equivalent contract doc) for an existing worklog
   convention — if one exists (e.g. "worklogs live in `~/tmp/<topic>/`, outside the repo"),
   follow it exactly.
2. If none exists, propose a sensible default (a location outside any git repo the project
   uses, so the log is a working artifact rather than committed history) and confirm with the
   user before creating it — don't silently invent a convention for a project that doesn't
   have one yet.

## Closing out

Not automatic — triggered explicitly (e.g. "sluit de OHDA-log af", "close this out", "maak
een lesson learned"). But **do suggest it** once a session reaches a natural stopping point:
the problem is solved, or you've concluded it's a dead end.

On close:
1. Write/update the `TL;DR` at the top: problem summary, current status, and — if solved —
   the gist of the fix. A reader should get the outcome from the TL;DR alone; the full log is
   for whoever wants the detail.
2. Turn it into a "lesson learned": cross out (strike through) dead ends — don't delete them,
   the fact that a path was tried and failed is itself valuable information for the next
   reader. Make the log more self-contained: fill in the "wait, what was that again" gaps you
   glossed over while moving fast.
3. **Promote the lesson learned into the project's CLAUDE.md by default**, under a
   `## Lessons learned` section (create it if absent) — one entry per closed-out log, dated,
   with a one/two-line summary and a link/path to the full worklog. CLAUDE.md is already read
   at the start of every session in this project, so this is what actually gets a lesson
   *seen* again, rather than filed and forgotten. Exception: if the host project has its own
   richer promotion path for conclusions (e.g. a `fact`/`journal`/`hyp` memory layer, as in
   Peters Infra), defer to that instead — don't create a competing CLAUDE.md section there.

## Worked example

```
O:  % more readme.txt
    more: cannot open readme.txt: Permission denied
H:  file has the wrong permissions
H:  we are not the user we think we are
D:  check permissions, `ls -l`
A:  % ls -l readme.txt
    ----------  1 peter  wheel  48 Jan 25 12:32 readme.txt
O:  permissions are 000, expected 644 → H "wrong permissions" accepted
```
(Verdict is explicit in the closing `O:` — no need to re-read the `A:` output to know the
loop resolved.)
