---
layout: default
title: Aurora Healthcare POC
---


# Aurora Healthcare POC

```text
========================================================================
AURORA HEALTHCARE POC — BEFORE / AFTER COMPARISON
========================================================================

Demonstration purpose:
Show the difference between an unguided medical AI system that proceeds
despite contradictions or missing evidence, and a governed system that
admits facts, blocks inadmissible actions, and produces an auditable trail.

This is not a model comparison.
It is a decision-admissibility comparison.
========================================================================


========================================================================
SIMULATED BLACK-BOX NOTE (UNGOVERNED)
========================================================================

SCENARIO 1 — VALID EXTRACTION

Chief complaint: chest pain
Assessment: Myocardial infarction
Plan: ECG, troponin, aspirin (standard chest pain pathway)

------------------------------------------------------------------------

SCENARIO 2 — DENIAL CONFLICT (black-box failure)

Chief complaint: chest pain (triage)
History: Patient denies current chest pain
Assessment: Myocardial infarction
Plan: ECG, troponin, aspirin

NOTE: Ungoverned system still outputs a diagnosis
despite explicit patient denial.

------------------------------------------------------------------------

SCENARIO 3 — INSUFFICIENT EVIDENCE (black-box confabulation)

Chief complaint: chest pain (not actually established)
Assessment: Myocardial infarction
Plan: ECG, troponin, aspirin

NOTE: Ungoverned system produces a diagnosis
without recorded supporting evidence.

========================================================================
OBSERVATION
========================================================================

The black-box system proceeds in all cases.
It has no mechanism to determine whether an action itself is permissible.

It always acts.
========================================================================



========================================================================
AURORA-GOVERNED RUN (WITH FORENSIC LEDGER)
========================================================================

AURORA HEALTHCARE POC: GOVERNED CLINICAL EXTRACTION

------------------------------------------------------------------------
SCENARIO 1 — VALID EXTRACTION
------------------------------------------------------------------------

TRANSCRIPT LINE: "Patient reports chest pains"
  [ADMITTED] Fact added to ledger.

TRANSCRIPT LINE: "Provider diagnoses Myocardial Infarction"
  [ADMITTED] Fact added to ledger.

------------------------------------------------------------------------
SCENARIO 2 — REFUSE (DENIAL CONFLICT)
------------------------------------------------------------------------

TRANSCRIPT LINE: "Patient denies chest pain"
  [ADMITTED] Fact added to ledger.

TRANSCRIPT LINE: "Provider diagnoses Myocardial Infarction"
  [REFUSE] Diagnosis forbidden.
           Reason: Patient explicitly denied chest pain.

------------------------------------------------------------------------
SCENARIO 3 — STOP (INSUFFICIENT EVIDENCE)
------------------------------------------------------------------------

TRANSCRIPT LINE: "Provider diagnoses Myocardial Infarction"
  [STOP] Cannot admit diagnosis.
         Reason: No reported symptoms or supporting evidence.

========================================================================
FINAL FORENSIC LEDGER ENTRIES (ABRIDGED)
========================================================================

[ADMIT]   CID: cid:rns65:0x000000002C2F580FA
          Payload: subject, relation, head, admissibility, policy, module

[ADMIT]   CID: cid:rns65:0x000000002584F8543
          Payload: subject, relation, head, admissibility, policy, module

[ATTEMPT] CID: cid:rns65:0x000000001F4B2BD3F
          Payload: attempted_action, origin, state_hash

[REFUSE]  CID: cid:rns65:0x0000000026C62F3F9
          Reason: safety_conflict

[STOP]    CID: cid:rns65:0x000000001CA4C5C79
          Reason: insufficient_evidence

========================================================================
CLINICAL SUMMARY VIEW (HUMAN-READABLE + AUDITABLE)
========================================================================

ADMITTED (patient-reported & observed facts)
- Patient reports chest pain
- Patient denies chest pain

ATTEMPTED (captured diagnostic actions)
- Provider attempts diagnosis: myocardial infarction

BLOCKED (inadmissible clinical actions)
- REFUSE: diagnosis myocardial infarction (safety_conflict)
- STOP: diagnosis myocardial infarction (insufficient_evidence)

------------------------------------------------------------------------
INTERPRETATION
------------------------------------------------------------------------

The system records attempted clinical actions for auditability,
but prohibits commitment when evidentiary or safety constraints are not met.

Refusal and stop outcomes are deterministic, logged,
and represent correct system behavior.

========================================================================
AUDIT & VERIFICATION
========================================================================

Ledger file:
medical_audit.jsonl

Verify integrity:
python libs/audit/verifier.py medical_audit.jsonl --mode semantic

========================================================================
END OF DEMONSTRATION
========================================================================
```
