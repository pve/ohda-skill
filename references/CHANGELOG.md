# Changelog

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
