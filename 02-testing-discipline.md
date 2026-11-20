# 02 — Testing Discipline

## Pre-register the falsification test

Before sending a single test request, write down:

- The hypothesis in one sentence.
- The observation that would **falsify** it.
- The observation that would **support** it.

If you cannot state the falsifying observation, you do not have a hypothesis
yet — you have a hunch. Hunches are for recon, not for reports.

## Paired positive controls

For any access-control test, run the legitimate action in the same session:

- The owner reads their own object → must succeed (positive control).
- The other account reads the same object → the actual test.

A failure of the positive control invalidates the run: the endpoint may be
broken, the object may not exist, or the session may be wrong. A "blocked"
result without a working positive control is noise, not evidence of safety —
and a "success" without one is not evidence of a bug.

## Cross-tenant method

1. Create equivalent objects in two accounts you control, with unique marker
   content in each.
2. Confirm each owner can access their own object (positive controls).
3. Attempt the cross-access in both directions — asymmetries are common.
4. Vary one thing at a time: identifier, header, key scope, surface.
5. Record the exact status, body shape, and error string for every attempt;
   error-string differences are themselves a signal.

## Stale authorization checklist

After any privilege change — role downgrade, group removal, disable, delete —
re-test everything that was issued *before* the change:

- API keys and personal access tokens
- Active sessions and refresh tokens
- Signed or shared URLs
- Webhook subscriptions and automation rules
- Invitations sent but not yet accepted

Access that survives its own revocation is a finding; access that is cleanly
cut is a data point. Record both.

## Rate and safety discipline

- Stay inside the program's stated rate limits and scope, always.
- Test only on accounts and objects you own.
- Prefer the smallest demonstration that proves the claim; never pull real
  user data to make a point a marker file would make.
- Stop escalating the moment the claim is proven. Proof is the goal, not
  maximum impact.
