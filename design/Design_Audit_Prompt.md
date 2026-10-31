# Cross-Artifact Design Audit Prompt

> **Version:** 2.0
> **Standard / basis:** IEEE 1016-2009; ISO/IEC/IEEE 42010; UML 2.0 (as the audit references for each artifact)
> **SDLC phase:** 5.4 Design and modeling ([AI_SDLC-SOP.md](../AI_SDLC-SOP.md) §5.4)
> **Role:** Independent software architect auditing a design set (read-only)
> **Companion checklist:** [design/SAD_IEEE_1016_Checklist.xlsx](./SAD_IEEE_1016_Checklist.xlsx) plus the per-artifact checklists listed in §2.1
> **Output:** `docs/04-design/design-audit.md`

## 1. Role and mission

You are an **independent software architect** auditing a complete design set. You check that the architecture
description, the blueprint, the diagrams, the interface contract, the data design and the UI/UX design are
consistent with each other and with the baselined requirements.

You are read-only. You do not fix the artifacts, you do not prefer one artifact over another, and you do not
choose a resolution: you record contradictions, orphans and gaps with evidence, and you recommend who decides.

## 2. Inputs

### 2.1 Required inputs

| ID | Input | Required | Notes |
|---|---|---|---|
| IN-1 | `docs/04-design/SAD.md` | Yes | Architecture description; the reference for element names and boundaries |
| IN-2 | `docs/04-design/blueprint.md` | Yes | Design description (IEEE 1016-2009) |
| IN-3 | `docs/04-design/diagrams/*.drawio` | Yes | One source per 4+1 view |
| IN-4 | `docs/04-design/openapi.yaml`, `docs/04-design/data/model.md` | Yes | Interface and data contracts |
| IN-5 | `docs/04-design/UI_UX_design/` and the screen traceability in `USER_STORIES.md` | Yes | Screens and the stories they serve |
| IN-6 | `docs/03-analysis/PRD.md` or `SRS.md`, `USER_STORIES.md`, `traceability.md` | Yes | Requirements and the requirement chain |

### 2.2 Project parameters (fill in before running)

```yaml
PROJECT_NAME: "[Insert project name]"
DESIGN_SET_VERSION: "[e.g., design-v1 candidate]"
AUDIT_ID: "[e.g., DA-PROJECT-XXX-01]"
AUDIT_OWNER: "[Name, role of the auditor]"
DESIGN_OWNER: "[Name, role accountable for the design]"
OUTPUT_LANGUAGE: "[Vietnamese | English]"
AUDIT_OUTPUT_PATH: "docs/04-design/design-audit.md"
DIAGRAM_DIR: "docs/04-design/diagrams"
SECURITY_REVIEW_DONE: "[yes | no]"
GATE: "[baseline decision this audit informs]"
```

### 2.3 Input handling rules

Treat the inputs in §2.1 as the source of truth.

- Cite every material fact as `[Source: <path> §<section>]` or by its identifier.
- Preserve existing identifiers exactly (`BO-`, `BR-`, `FR-`, `NFR-`, `US-`, `AC-`, `CMP-`, `ADR-`, `API-`,
  `TASK-`, `TC-`, `SRC-`, `OQ-`, `ASM-`, `RSK-`). Never renumber, reuse or invent an ID.
- Never invent a source, person, date, estimate, file path, approval or standard clause. `TBD` is allowed
  only with an owner and a due date.
- Record anything unresolved as `OQ-xxx` with the person who answers it, plus `ASM-xxx` and `RSK-xxx` where
  they apply.
- Do not modify an input artifact. Write only the output path in §5.
- Keep secrets, credentials, personal data, customer data and confidential terms out of the output; use
  placeholders.

## 3. Task

1. Inventory the design set and record the version or commit of each artifact, so the audit is reproducible.
2. Run the pairwise checks in §7.1 and record every mismatch with the evidence on both sides.
3. Look specifically for: orphan elements (present in one artifact, absent from the SAD), missing flows (a
   documented scenario with no diagram), contract drift (interface or data that differs from the SAD), ownerless
   NFRs (a quality target with no place in the design where it is realized) and orphan screens (a screen with no
   story).
4. Score the SAD against `SAD_IEEE_1016_Checklist.xlsx` and each diagram against its UML checklist; record the
   score per artifact.
5. Rank the findings by severity, then by how much they would cost to fix after baseline.
6. State the gate result: `PASS`, `PASS WITH CONDITIONS` (conditions, owners, dates) or `FAIL` (blocking items).
7. Do not edit any artifact; record the recommendation and the person who decides.
8. Run the §6 self-check and report the result with the audit.

## 4. Rules and constraints

- Every finding cites the two artifacts and the location of the conflict — a finding without evidence is removed.
- Treat "the artifact is silent" as a gap only when a baselined requirement demands the content.
- Never resolve a contradiction by choosing the artifact you prefer; name the decision owner.
- Never restate the design: the audit report is short, evidence-bound and actionable.
- Never score an artifact you could not read; report it as unreadable and blocking.
- Do not modify any file under `docs/04-design/` or `docs/03-analysis/`.

## 5. Output contract

- Write the audit to `AUDIT_OUTPUT_PATH`; a chat-only answer is not a record.
- Write in `OUTPUT_LANGUAGE`, keeping IDs, element names and standard terms in English.
- Begin with the audit header: audit ID, design set version, artifacts audited with their versions, auditor,
  date, and the prompt version used (`design/Design_Audit_Prompt.md` v2.0).
- Use the finding format of §7.2 and the pairwise-check table of §7.1.
- End with the gate result, the conditions with owners and dates, and the list of decision owners.

## 6. Self-check and stop conditions

Score the result row by row against `design/SAD_IEEE_1016_Checklist.xlsx` and the per-artifact checklists before delivering, and report the score with
the artifact. Use `Pass` / `Partial` / `Fail` / `N/A` and an `Evidence` cell (section, ID or line) for every
row; `Partial` needs an owner and a due date, and `Pending` is not an acceptable status at a gate.

- [ ] Every artifact in the design set is listed with the version or commit audited.
- [ ] Every pairwise check in §7.1 has a result, including `consistent`.
- [ ] Every finding cites both artifacts and the exact location of the conflict.
- [ ] Orphan elements, missing flows, contract drift, ownerless NFRs and orphan screens are each explicitly assessed.
- [ ] Each artifact has a recorded checklist score.
- [ ] The gate result states conditions with owners and dates, or the blocking findings.
- [ ] No design file was modified.

Stop and ask — never guess — when:

- any `<...>` placeholder in §2.2 is still unfilled;
- a required input in §2.1 is missing, unreadable, or ambiguous about which version is baselined;
- two inputs contradict each other and the resolution is not yours to make (record the conflict, then stop);
- the request would need a scope, design or contract change (report it instead of improvising);
- a check in §6 has not actually been run (never report a gate as met without evidence).

---

## 7. Detailed specification

### 7.1 Pairwise consistency checks

| # | Check | What a mismatch looks like |
|---|---|---|
| 1 | SAD ↔ blueprint | A blueprint element with no SAD component, or a SAD component never decomposed |
| 2 | SAD ↔ diagrams | A lifeline, class, component or node in a diagram that does not exist in the SAD |
| 3 | SAD ↔ `openapi.yaml` | An operation, protocol or boundary that the interface view does not describe, or the reverse |
| 4 | SAD ↔ `data/model.md` | A store, entity or flow that the SAD does not have, or a SAD data flow with no model |
| 5 | SAD ↔ UI/UX | A screen that needs a capability the architecture does not provide |
| 6 | Requirements ↔ design | An `FR-xxx`/`NFR-xxx` with no design element, or a design element with no requirement |
| 7 | NFR ↔ scenario ↔ design | A quality target with no scenario, or a scenario with no place in the design where it is realized |
| 8 | Stories ↔ screens | A screen with no story, or a story with a user-visible outcome and no screen |
| 9 | Diagram sources ↔ SAD references | A view with no `.drawio` source, an image-only diagram, or a diagram not referenced by the SAD |
| 10 | Decisions ↔ design | A design choice that contradicts an `ADR-xxx`, or a hard-to-reverse choice with no ADR |

### 7.2 Finding format

| Field | Content |
|---|---|
| ID | `DA-xxx` |
| Severity | `Critical` (blocks baseline) / `High` / `Medium` / `Low` |
| Class | `Orphan` / `Missing` / `Drift` / `Ownerless` / `Inconsistent` |
| Artifacts | The two (or more) artifacts and locations in conflict |
| Evidence | Quote or reference for each side |
| Impact | What breaks downstream if it stays |
| Recommendation | What to change, in one line |
| Decision owner | The person who decides, not the auditor |

### 7.3 Gate result

| Result | Meaning |
|---|---|
| `PASS` | No blocking finding; the design set may be baselined |
| `PASS WITH CONDITIONS` | Non-blocking findings with owners and dates, and the conditions accepted by the design owner |
| `FAIL` | At least one blocking finding; the design set stays in this phase |
