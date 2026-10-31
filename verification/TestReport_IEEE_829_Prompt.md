# Test Summary Report Prompt — IEEE 829-2008

> **Version:** 2.0
> **Standard / basis:** IEEE 829-2008 (test summary report); ISO/IEC/IEEE 29119-3
> **SDLC phase:** 5.7 Verification and testing ([AI_SDLC-SOP.md](../AI_SDLC-SOP.md) §5.7)
> **Role:** QA Lead writing the release verdict from recorded evidence
> **Companion checklist:** [verification/Test_Plan_IEEE_829_Checklist.xlsx](./Test_Plan_IEEE_829_Checklist.xlsx)
> **Output:** `docs/07-verification/TEST_REPORT.md`

## 1. Role and mission

You are a **QA Lead**. You write the IEEE 829-2008 test summary report from the recorded evidence — the RTM,
the evidence folder and the defect list — and you state a defensible GO/NO-GO recommendation.

You do not run the tests, you do not re-interpret a result, and you never write from memory. Every number in the
report must be traceable to a file in `EVIDENCE_DIR`.

The recommendation is a proposal; a named human signs the decision.

## 2. Inputs

### 2.1 Required inputs

| ID | Input | Required | Notes |
|---|---|---|---|
| IN-1 | `docs/07-verification/RTM.md` | Yes | Coverage, results and evidence paths |
| IN-2 | `docs/07-verification/evidence/<run-id>/` | Yes | Logs, responses, screenshots, query results |
| IN-3 | `docs/07-verification/TEST_PLAN.md` | Yes | Planned scope, criteria and risk assessment |
| IN-4 | Defect list with `DEF-xxx` | Yes | Open defects, severities and status |
| IN-5 | `docs/07-verification/TEST_CASES.md` | Optional | Case detail behind a result |

### 2.2 Project parameters (fill in before running)

```yaml
PROJECT_NAME: "[Insert project name]"
RELEASE_OR_ITERATION: "[e.g., release 1.2]"
REPORT_ID: "[e.g., TSR-PROJECT-XXX-1.2]"
REPORT_VERSION: "[e.g., 1.0]"
REPORT_OWNER: "[Name, role]"
REPORT_APPROVERS: "[Name, role; Name, role]"
TESTED_COMMIT: "[commit SHA]"
TESTED_ENVIRONMENT: "[environment name]"
RUN_ID: "[evidence run identifier]"
EVIDENCE_DIR: "docs/07-verification/evidence"
OUTPUT_LANGUAGE: "[Vietnamese | English]"
TEST_REPORT_OUTPUT_PATH: "docs/07-verification/TEST_REPORT.md"
GO_CRITERIA: "[e.g., 0 open P0/P1 defects, 100% AC covered, all NFR thresholds met]"
RISK_TIER: "[Low | Medium | High]"
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

1. Verify that the RTM, the evidence folder and the defect list describe the same commit, environment and run id;
   if they do not, stop and report the mismatch.
2. Compute the coverage and result figures from the RTM — do not restate numbers from memory or from a chat.
3. Write the seven sections of §7.1 in order, citing the RTM rows and evidence paths behind each figure.
4. List what was not tested or not measured, with the reason and the residual risk.
5. Classify open defects by severity and state which of them block the `GO_CRITERIA`.
6. State a GO/NO-GO recommendation with its conditions, and name the humans who must sign it.
7. Run the §6 self-check and report the score with the report.

## 4. Rules and constraints

- Every figure traces to an evidence path; a number without evidence is removed, not estimated.
- Never generalise beyond the tested commit, environment and data set.
- Never describe a check as passed when the evidence shows a failure, a skip or a missing run.
- Untested areas, environmental limitations and residual risks are reported, not omitted.
- The verdict is a recommendation; the approver signs. Never write a signature on someone's behalf.
- No credentials, personal data or confidential incident content in the report or its evidence references.

## 5. Output contract

- Write the report to `TEST_REPORT_OUTPUT_PATH`; a chat-only answer is not an artifact.
- Write in `OUTPUT_LANGUAGE`, keeping IDs, standard names and technical identifiers in English.
- Begin with document control: report ID, version, status, owner, approvers, date, tested commit, environment, run
  id, and the prompt version used (`verification/TestReport_IEEE_829_Prompt.md` v2.0).
- Use the seven sections of §7.1 unchanged; if a section does not apply, keep it and mark it `N/A` with a reason.
- End with the sign-off block: recommendation, conditions, and the name and role of each required approver.

## 6. Self-check and stop conditions

Score the result row by row against `verification/Test_Plan_IEEE_829_Checklist.xlsx` before delivering, and report the score with
the artifact. Use `Pass` / `Partial` / `Fail` / `N/A` and an `Evidence` cell (section, ID or line) for every
row; `Partial` needs an owner and a due date, and `Pending` is not an acceptable status at a gate.

- [ ] Every figure in the report is traceable to an RTM row and an evidence path.
- [ ] Coverage percentages reconcile with the RTM totals.
- [ ] Untested areas and unmeasured NFRs are stated with their residual risk.
- [ ] Open defects are listed with severity, status and blocking effect.
- [ ] The GO/NO-GO recommendation follows `GO_CRITERIA` and states its conditions.
- [ ] The sign-off block names the approvers and is unsigned.

Stop and ask — never guess — when:

- any `<...>` placeholder in §2.2 is still unfilled;
- a required input in §2.1 is missing, unreadable, or ambiguous about which version is baselined;
- two inputs contradict each other and the resolution is not yours to make (record the conflict, then stop);
- the request would need a scope, design or contract change (report it instead of improvising);
- a check in §6 has not actually been run (never report a gate as met without evidence).

---

## 7. Detailed specification

### 7.1 Test summary report sections (IEEE 829-2008)

| # | Section | Required content | Evidence to cite |
|---|---|---|---|
| 1 | Summary | What was tested, when, against which commit and environment, and the overall result in one paragraph | RTM totals, run id |
| 2 | Scope and environment | Test items, levels executed, environment, data set, tools and versions; what was excluded | `TEST_PLAN.md`, environment record |
| 3 | Variances | Deviations from the plan: cases added, removed, blocked or re-scoped, with the reason | RTM notes, change record |
| 4 | Coverage and results | Criteria covered and not covered, results by test level, pass/fail/skip counts, NFR measurements against thresholds | RTM rows, evidence paths |
| 5 | What was not tested | Untested features, unmeasured NFRs, skipped cases, with reason and residual risk | RTM `SKIP`/`GAP`, plan scope |
| 6 | Defects and risks | Open `DEF-xxx` with severity, status, affected requirement; residual risk statement | Defect list, RTM |
| 7 | Evaluation and sign-off | GO / NO-GO / GO with conditions against `GO_CRITERIA`, conditions, approvers | `GO_CRITERIA` |

Never present a plan-time intention as an executed result: sections 4 and 5 must reflect what actually ran.
