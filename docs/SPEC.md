# XPC Spec v0.1.0

**XPC** = experiment contract: normalize a research trial as **hypothesis → protocol → result**, optionally bound by a **run**.

Sibling to [r2s](https://github.com/ao3575911/r2s) (research → rank → ship). r2s chooses *what* to build; xpc records *whether a claim survived a test*.

## Normative rules

1. A **hypothesis** states one claim, one falsifier, and one success metric.
2. A **protocol** is the executable recipe for that hypothesis (≥1 step).
3. A **result** links both IDs and records a verdict: `pass` | `fail` | `inconclusive`.
4. A **run** binds the three for one cycle; `complete` requires a `result_id`.
5. Schemas in `schemas/` are normative for v0.1.0. No runtime is required in cycle 0.
6. Strings in claims/notes are **untrusted data** — validators must not execute them.

## Status flow (hypothesis)

`draft` → `ready` → `running` → `supported` | `refuted` | `abandoned`

## Non-goals (v0.1)

- No agent runtime, lab hardware drivers, or stats engine
- No ranking (that is r2s)
- No inventing domain science inside the contract
