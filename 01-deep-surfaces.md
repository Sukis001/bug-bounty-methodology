# 01 — Deep Surfaces

The surfaces below are under-hunted because they take longer to understand
than a scanner run or a header swap. That is exactly why they pay.

## Business logic and limit enforcement

- Configured limits (transaction caps, quotas, seat counts, plan tiers) that
  are displayed in the UI but never enforced by the API.
- Enforcement that exists on the primary path but is missing on bulk, import,
  mobile, or legacy versions of the same operation.
- Race windows: parallel requests that each pass a check which only holds
  when operations are serialized.
- Negative, zero, and boundary values in quantities, amounts, and discounts —
  especially where the front end validates but the API trusts.

## State machines and neglected flows

- Multi-step flows where a later step assumes an earlier check ran:
  checkout, onboarding, verification, approval chains.
- Account recovery and password reset: token lifetime, reuse, and whether
  completing one flow invalidates sessions created by another.
- Email change: whether the old address, existing sessions, and API keys keep
  working afterwards — and whether they should.
- Invitations: cross-tenant invites, role granted on acceptance, invites that
  survive revocation or expiry.
- Export and sharing: links and exports that outlive the permission that
  created them; exports that include more than the UI shows.

## Authorization depth

- Stale authorization: access that survives a role downgrade, removal from a
  group, or account disablement — including already-issued API keys, tokens,
  and signed URLs.
- Object references reachable through a *different* surface than the one that
  enforces the check (REST vs. GraphQL vs. file protocols vs. webhooks).
- API key scoping: keys documented as restricted (by path, workspace, or
  operation) that quietly accept broader requests; scope enforced on reads
  but not writes, or the reverse.

## Legacy and parallel surfaces

- Older API versions that remain live after a fix ships on the current one.
- Alternate clients (mobile API, partner API, embedded widgets) that
  re-implement the same feature with weaker checks.
- Async paths — imports, webhooks, scheduled jobs, automations — that act with
  broader permissions than the user who configured them.

## Picking a surface

Prefer surfaces that are:

1. Testable with one or two accounts you control.
2. Reachable without destructive actions.
3. Specific enough that a falsification test can be written in one sentence.
