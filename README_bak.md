# aurora_governor_docs
Provable governance substrate for AI reasoning with audit-grade STOP, CLARIFY, and REFUSE outcomes.

# Aurora Governor

A provable governance substrate for AI reasoning.

## What it does

Aurora Governor produces cryptographically auditable governance decisions—STOP, CLARIFY, and REFUSE—as first-class outcomes, not error states.

Every governed non-answer is logged as a forensic envelope with deterministic hash-chaining and canonicalization, making AI behavior replayable and verifiable.

## Why it matters

AI systems that make consequential decisions must be able to:
- Refuse inadmissible actions
- Request clarification when entities are ambiguous
- Stop when context is insufficient

These aren't failures. They're governed outcomes that deserve the same forensic rigor as accepted responses.

## Governance halts

Aurora implements three governed non-answer types:

- **STOP** — insufficient context to proceed safely
- **CLARIFY** — entity ambiguity requires disambiguation
- **REFUSE** — action is inadmissible under current policy

Each halt produces a `kind: aurora.event` envelope suitable for compliance audit and deterministic replay.

## Forensic guarantees

- Hash-chained event sequences
- Canonical serialization (no whitespace drift)
- Deterministic replay from JSONL logs
- Cryptographic verification of governance decisions

## Use cases

- Legal-tech systems requiring auditable refusals
- Compliance infrastructure for regulated AI
- Governance substrates for agentic systems
- Policy-aware reasoning kernels

---

**Source code available for evaluation under controlled access.**

For inquiries: meg.stokes.ai@gmail.com
