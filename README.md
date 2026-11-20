# Bug Bounty Methodology

Working notes on how I hunt for web and API vulnerabilities and turn them into
reports that survive triage. Everything here is general method — no specific
programs, targets, or findings.

## Core principles

1. **Hunt where others don't.** Surface-level findings (missing headers, basic
   CRUD access-control swaps, obvious enumeration) are found by everyone, fast.
   The durable value is in deep surfaces: business logic, state machines, and
   flows the product team itself rarely revisits.
2. **Falsify, don't just confirm.** Every hypothesis gets a test that could
   prove it *wrong*, designed before the first request is sent. A finding that
   survives a genuine falsification attempt is worth ten that were never
   challenged.
3. **No claim without a control.** Especially for cross-tenant and
   authorization claims: if the legitimate owner cannot perform the same
   action in the same run, the test proves nothing.
4. **Evidence or it didn't happen.** Sanitized request/response pairs, exact
   object identifiers, timestamps, and an explicit confidence label on every
   claim.
5. **Speed matters in crowded programs.** A proven finding that sits in a
   notebook loses to a duplicate. Verify, dedupe-check, and file — in that
   order, without a gap.

## Contents

- [01 — Deep surfaces](01-deep-surfaces.md): where the under-hunted bugs live.
- [02 — Testing discipline](02-testing-discipline.md): paired controls,
  cross-tenant method, stale authorization, API key scoping.
- [03 — Evidence and reporting](03-evidence-and-reporting.md): what a report
  must contain, confidence labels, and dedupe hygiene.

## The short version

Standard checks are a warm-up, not the hunt. Pick one deep surface, write down
what would prove the hypothesis wrong, run the paired test, and write up only
what survives.
