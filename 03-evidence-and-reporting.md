# 03 — Evidence and Reporting

## What a report must contain

- **Target and scope reference** — the exact surface tested, and why it is in
  scope.
- **Preconditions** — accounts, roles, and objects used, all owned by the
  researcher.
- **Steps** — numbered, reproducible by a triager who has never seen the
  product.
- **Sanitized request/response pairs** — full enough to prove the claim, with
  credentials, tokens, and unrelated personal data removed.
- **Paired control results** — the legitimate action succeeding in the same
  run (see [02 — Testing discipline](02-testing-discipline.md)).
- **Impact statement** — what an attacker gains, stated conservatively and
  tied to what was actually demonstrated, not what might be possible.
- **Confidence label** — see below.

## Confidence labels

- **Confirmed** — reproduced end-to-end with controls, more than once.
- **Probable** — reproduced once, or reproduced without one control; the
  missing piece is named explicitly.
- **Suspected** — behavior observed but not isolated; reported internally
  only, never filed as-is.

Filing a *Suspected* item as *Confirmed* is how researchers burn credibility
and, on some platforms, their one available submission slot.

## Dedupe hygiene

- Search the program's disclosed reports and known-issue notes before
  building a full PoC.
- In crowded programs, a proven finding loses value by the hour. Once the
  evidence standard above is met, file immediately — deepening can continue
  as a supplement while the original is in triage.
- Keep a personal ledger of what you have already found and filed, per
  program, so you never re-test (or worse, re-file) your own work.

## Writing for the triager

- Lead with the demonstrated impact in two sentences; put methodology after.
- One claim per report. Chained impact belongs in the impact statement, not
  in a second bundled bug.
- State what you did *not* test. A report that names its own limits reads as
  more credible, not less.
