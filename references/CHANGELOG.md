# Changelog

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
