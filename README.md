# Engineering with AI agents — field notes

> Programming got cheap. Knowing what must not break did not.

I build complex software every day — enterprise, regulatory, legal and data-heavy systems — with AI coding agents (Codex, Claude). Most of my work is no longer writing code. It is teaching the agent what it must not get wrong, and turning every correction into a written rule that the next session already knows.

This repository collects those principles.

## Principles

1. **The agent executes. The architect is accountable.** No output ships because "the model wrote it".
2. **Expertise didn't die. It became context.** What you know is only useful to the agent once it lives in the repository: rules, decisions, acceptance tests.
3. **A correction that repeats is a system failure, not an agent failure.** Fix the context, not just the output.
4. **Every rule carries its reason.** A rule without a "why" gets broken the first time it seems inconvenient.
5. **Agents drift toward excess.** Full test suites by habit, gates with no real risk behind them, layers nobody asked for. Many of the best rules tell the agent to do *less*.
6. **Verification is proportional to risk.** Focused tests for a scoped fix; the full suite only when the change is structural, risky or cross-cutting.
7. **Operational blockers are not code blockers.** A missing certificate or authorization is not an unfinished feature, and the two must never be confused.
8. **Acceptance tests are never loosened to turn green.**
9. **Decisions are written down, including the ones you reverse.** Knowing why something was stopped saves the next session from restarting it.
10. **Humans keep the irreversible steps.** Anything with real-world fiscal, legal or financial effect requires human approval.

## Examples of rules agents don't know on their own

- Empty a table with `TRUNCATE`, never an unqualified `DELETE` (dead tuples, WAL bloat, indexes that never shrink).
- The application's runtime role never owns database objects; capability is granted by name, never by ownership.
- A table read by the UI is never rebuilt in place: build and validate an inactive version, then switch a pointer.
- Raw API responses are persisted (with hash) before any parsing.

---

Luciano Manetta · Belo Horizonte, Brazil · [lm.tec.br](https://lm.tec.br)
