# Changelog

## 1.3.0 — 2026-09-11
- Lessons from a real incident log (promptfoo/BIG_O timeout diagnosis) that
  needed rework after the fact:
- TL;DR: made explicit there is exactly **one**, updated in place — a second
  TL;DR appended further down was the actual mistake seen.
- Observe: the replayability test now also covers *what you cite* — point at
  reproducible identifiers (job/run/request IDs, timestamps), never a line
  number into a local/temp file only you can open.
- Observe: when the objective includes handing findings to an outside party,
  check early whether your own logging/capture is detailed enough for that —
  don't discover a capture gap (e.g. a truncated error message) only while
  writing the final report.
- Hypothesize: a hypothesis the loop moves past without testing must be
  marked explicitly ("not tested — still open"), not left to drop silently.
- Header/Objective: if the original objective becomes unreachable as stated,
  update it in place and redefine what "done" now means, instead of leaving
  it stale against a log that moved on.
- Worklog discipline: evidence discovered late (e.g. while drafting a report)
  that logically belongs earlier gets inserted in its logical place, with an
  explicit note that it was moved and why — not appended at the end out of
  chronological order.

## 1.2.0 — 2026-09-10
- Source pinned to the actual video: "Introducing the OHDA method for
  professional IT troubleshooting" (Club Cloud Computing, 2024-01-25),
  <https://www.youtube.com/watch?v=rQ5MpGWCiUw>; flattened transcript added
  as `references/source-transcript-2024-01-25.srt`; link added to README.
- Observe: added the concrete replayability test — hand the write-up to
  someone who wasn't there; if they can't proceed without asking you, it's
  not observed yet.
- Hypothesize: hypothesizing may itself need small non-solving experiments
  that feed observations back into the loop.
- Decide: explicitly-written candidate actions can be parcelled out to
  multiple people/teams at large scale.
- Worklog: TL;DR is updated at every pause/break, not only at closing out.
- Why: added the "big idea" framing (explicit desired result / options /
  chosen action → reliable performance + teachable) and "professional is a
  process, not a state of mind".
- Act: every `A:` must name the `D:` it executes and the objective it
  serves; and before acting, judge whether the action needs a human in the
  loop (destructive / outward-facing / irreversible / outside mandate) and
  stop for confirmation if so.
- Worklog is Markdown: each O/H/D/A step is its own blank-line-separated
  paragraph, raw output in fenced code blocks — so it actually renders.
  Worked example rewritten to match.
- Hypotheses are numbered `H1`, `H2`, … so `D:`/`O:` lines can reference
  one unambiguously; worked example updated.
- A human-in-the-loop pause is also a trigger for updating the `TL;DR`.

## 1.1.0 — 2026-08-26
- Every `A:` must be immediately followed by an `O:` that explicitly closes
  the loop against the hypothesis it tested (what you now see, what you
  expected, accepted/rejected verdict) — not just a bare output dump.
- Lessons-learned promotion path decided: default to a `## Lessons learned`
  section in the host project's CLAUDE.md (created if absent), unless the
  project has its own richer promotion path (fact/journal/hyp layer), in
  which case defer to that instead.

## 1.0.0 — 2026-08-26
- Initial version, formalized from Peter van Eijk's "Professional IT
  troubleshooting, simplified" (Club Cloud Computing) OHDA method
  (video transcript + slide deck).
- Active-loop enforcement: O/H/D/A order is enforced, not just a logging
  convention.
- Log location is project-local-by-design: detect an existing convention
  from the host project's CLAUDE.md, else propose and confirm.
- Closing-out step (TL;DR + dead-ends struck-through, not deleted) is
  explicitly triggerable, and the skill should proactively suggest it at a
  natural stopping point.
