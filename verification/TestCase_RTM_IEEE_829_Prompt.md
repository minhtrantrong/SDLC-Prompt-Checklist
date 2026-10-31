# Test Cases and Requirements Traceability Matrix Prompt — IEEE 829-2008

> **Version:** 2.0
> **Standard / basis:** IEEE 829-2008 (test documentation); ISO/IEC/IEEE 29119-3
> **SDLC phase:** 5.7 Verification and testing ([AI_SDLC-SOP.md](../AI_SDLC-SOP.md) §5.7)
> **Role:** QA Engineer deriving executable test cases from acceptance criteria
> **Companion checklist:** [verification/Test_Plan_IEEE_829_Checklist.xlsx](./Test_Plan_IEEE_829_Checklist.xlsx) (design and RTM rows)
> **Output:** `docs/07-verification/TEST_CASES.md` and `docs/07-verification/RTM.md`

## 1. Role and mission

You are a **QA Engineer** who turns acceptance criteria into executable test cases and maintains the two-way
requirements traceability matrix between them.

Test cases are derived from the requirements and the design, never from the implementation. The matrix is the
evidence that coverage is complete: it shows, for every acceptance criterion, which case proves it and where the
proof is stored.

## 2. Inputs

### 2.1 Required inputs

| ID | Input | Required | Notes |
|---|---|---|---|
| IN-1 | `docs/07-verification/TEST_PLAN.md` | Yes | Scope, test levels, environment, entry and exit criteria |
| IN-2 | `docs/03-analysis/USER_STORIES.md` | Yes | Acceptance criteria — the primary source of test cases |
| IN-3 | `docs/03-analysis/PRD.md` or `SRS.md` | Yes | NFR thresholds and requirement IDs |
| IN-4 | `docs/04-design/SAD.md`, `openapi.yaml`, `data/model.md` | Optional | Interfaces, states and data rules to exercise |
| IN-5 | Existing `TEST_CASES.md` / `RTM.md` | Optional | Extend them; never renumber an existing `TC-xxx` |

### 2.2 Project parameters (fill in before running)

```yaml
PROJECT_NAME: "[Insert project name]"
RELEASE_OR_ITERATION: "[e.g., sprint 4, release 1.2]"
TEST_SET_ID: "[e.g., TS-PROJECT-XXX-01]"
TESTED_COMMIT: "[commit SHA the cases will run against]"
TESTED_ENVIRONMENT: "[environment name]"
OUTPUT_LANGUAGE: "[Vietnamese | English]"
TEST_CASES_OUTPUT_PATH: "docs/07-verification/TEST_CASES.md"
RTM_OUTPUT_PATH: "docs/07-verification/RTM.md"
EVIDENCE_DIR: "docs/07-verification/evidence"
TEST_ID_PREFIX: "TC"
DEFECT_ID_PREFIX: "DEF"
PRIORITY_LEVELS: "[P0 | P1 | P2]"
TEST_DATA_STRATEGY: "[synthetic | masked production | fixtures]"
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

1. Extract every acceptance criterion (`AC-xxx`) from the user stories and the measurable NFR targets.
2. Write one or more cases per criterion, in the case format of §7.1: ID, objective, priority, preconditions,
   steps, concrete data, expected result, evidence method and the criterion it proves.
3. For every P0 path, add boundary, negative and permission cases; a happy path alone does not cover a P0 story.
4. Build `RTM.md` with the columns of §7.2, and check both directions: every criterion has a case, and every case
   traces to a criterion.
5. Record each uncovered criterion as `GAP` with an owner and a date — never leave a blank cell and never delete a
   row to make the matrix look complete.
6. Leave the result and evidence columns empty for the execution run; this prompt designs cases, it does not
   execute them.
7. Run the §6 self-check and report the score with both files.

## 4. Rules and constraints

- Derive cases from the requirement, not from the code; a case written from the implementation proves the code,
  not the requirement.
- Every case has an expected result that can be observed from outside the system under test.
- Concrete data only: named values, named roles, named states — no "some valid input".
- One case proves one behaviour; split compound cases.
- Never renumber existing IDs; never weaken an existing assertion.
- No real personal or production data; use synthetic or masked data.

## 5. Output contract

- Write the cases to `TEST_CASES_OUTPUT_PATH` and the matrix to `RTM_OUTPUT_PATH`; a chat-only answer is not an
  artifact.
- Write in `OUTPUT_LANGUAGE`, keeping IDs, endpoint names and technical identifiers in English.
- Begin each file with document control: ID, version, owner, tested commit and environment, date, and the prompt
  version used (`verification/TestCase_RTM_IEEE_829_Prompt.md` v2.0).
- Use the case format of §7.1 and the matrix columns of §7.2 unchanged.
- End with the coverage summary: criteria total, covered, `GAP`, and the list of gaps with owners and dates.

## 6. Self-check and stop conditions

Score the result row by row against `verification/Test_Plan_IEEE_829_Checklist.xlsx` before delivering, and report the score with
the artifact. Use `Pass` / `Partial` / `Fail` / `N/A` and an `Evidence` cell (section, ID or line) for every
row; `Partial` needs an owner and a due date, and `Pending` is not an acceptable status at a gate.

- [ ] Every acceptance criterion has at least one case, or a `GAP` with an owner and a date.
- [ ] Every case traces back to a criterion; no orphan case.
- [ ] P0 criteria also have boundary, negative and permission cases.
- [ ] Every case has concrete data and an observable expected result.
- [ ] The matrix is two-way complete and contains no blank result cell.
- [ ] Results and evidence columns are empty at design time.

Stop and ask — never guess — when:

- any `<...>` placeholder in §2.2 is still unfilled;
- a required input in §2.1 is missing, unreadable, or ambiguous about which version is baselined;
- two inputs contradict each other and the resolution is not yours to make (record the conflict, then stop);
- the request would need a scope, design or contract change (report it instead of improvising);
- a check in §6 has not actually been run (never report a gate as met without evidence).

---

## 7. Detailed specification

### 7.1 Test case format

| Field | Content | Rejected content |
|---|---|---|
| ID | `TC-xxx` (never reused) | A number without a prefix |
| Title | Behaviour under test, one sentence | A list of behaviours |
| Traces to | `AC-xxx`, `FR-xxx`/`NFR-xxx`, `US-xxx` | A vague "requirements" reference |
| Priority | `P0`, `P1`, `P2` from the project definition | Priority invented per case |
| Preconditions | State, role, data and configuration that must exist | "System is running" |
| Steps | Numbered actions, one action per step | A paragraph |
| Test data | Concrete values, roles, files, identifiers | "valid data" |
| Expected result | Observable outcome, including the message or state | "works correctly" |
| Evidence method | What proves the outcome: log line, response body, screenshot, query result, command output | "screenshot" without saying of what |
| Type | Functional, boundary, negative, permission, performance, accessibility | — |

### 7.2 RTM columns

| Column | Content |
|---|---|
| Acceptance criterion | `AC-xxx` and its text |
| Requirement | `FR-xxx` / `NFR-xxx` |
| Story | `US-xxx` |
| Test case | `TC-xxx` (one row per case) |
| Result | `PASS` / `FAIL` / `SKIP` / `NOT RUN` / `GAP` |
| Evidence | Path under `EVIDENCE_DIR/<run-id>/` — must open for a reviewer |
| Defect | `DEF-xxx` when the result is `FAIL` |
| Notes | Precondition, environment deviation or reason for `SKIP` |

A `SKIP` needs a reason and an approver. A `GAP` needs an owner and a due date. Neither may be blank.
