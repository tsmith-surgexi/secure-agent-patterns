<!-- Copyright © 2026 SurgeXi Business Intelligence, a Teamsmith Enterprises LLC company. All Rights Reserved. -->
# ADR 0002 — Structured validation before any side effect

- **Status:** Accepted
- **Context:** If free-form model output can drive a tool, a single
  injection-influenced generation can trigger a real, possibly irreversible
  action. The gap between "the model said something" and "a tool ran" is where
  the damage happens.
- **Decision:** The model proposes a *schema-constrained* action object
  (`{tool, args}`). A dispatcher validates it against the schema **and** against
  the task's tool grant **before** the action reaches any executor. Malformed or
  out-of-grant proposals are rejected outright.
- **Consequences:**
  - ➕ Free-form text can never directly cause a side effect.
  - ➕ Validation, least-privilege, and allowlist checks all hang off one choke
    point — easy to reason about and audit.
  - ➖ The agent must emit structured proposals (a small constraint on prompting
    / output handling). Worth it.
- **Alternatives considered:** parse natural-language intent into actions
  (fragile, injectable); trust the model and validate after execution (too
  late — the action already ran).
