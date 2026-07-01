<!-- Copyright © 2026 SurgeXi Business Intelligence, a Teamsmith Enterprises LLC company. All Rights Reserved. -->
# ADR 0001 — Allowlist, never blocklist

- **Status:** Accepted
- **Context:** Agent actions touch an open-ended space — any URL, any command,
  any file path. Enumerating everything *forbidden* is an infinite, losing game;
  one missed entry is a breach.
- **Decision:** Every action class is governed by an *allowlist* of what is
  permitted (egress domains, runnable commands, reachable paths). Anything not
  explicitly allowed is denied by default.
- **Consequences:**
  - ➕ The system fails *closed*: an unforeseen action is blocked, not allowed.
  - ➕ The permitted surface is small, reviewable, and auditable.
  - ➖ Legitimate new needs require an allowlist update (a deliberate, reviewed
    change). Accepted as the cost of safety.
- **Alternatives considered:** blocklist of known-bad (always incomplete);
  anomaly detection only (probabilistic; an injected action that looks normal
  slips through).
