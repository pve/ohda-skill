# Changelog

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
