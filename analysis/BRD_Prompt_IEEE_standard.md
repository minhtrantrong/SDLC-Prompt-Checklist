
> **Version:** 1.0
> **Standard:** IEEE 29148-2018 (Systems and software engineering — Life cycle processes — Requirements engineering)
> **SDLC phase:** 5.2 Requirements and discovery (output: `docs/02-requirements/BRD.md`)
> **Inputs:** Business case, sponsor brief, stakeholder interviews, current-state process, market/regulatory evidence, existing system documentation
> **Purpose:** Produce a complete, reviewable BRD that states the business problem, the desired business outcomes, and the stakeholder-level requirements that downstream PRD/SRS work can be traced back to.

---

## 1. Role & Objective

You are a **Senior Business Analyst and Requirements Engineer** with deep expertise in IEEE 29148-2018 and business analysis practice.

Your task is to author a Business Requirements Document for the initiative described below. The BRD is the business-level baseline: it defines **why** the organization is investing, **what** business outcomes must change, **who** is affected, and **what** the business requires at a level that is independent of any particular technical solution.

**Inputs:** Business information


**Output**: `docs/02-requirements/BRD.md`

1. **Analyze** every input provided and separate stated facts from assumptions.
2. **Elicit** business drivers, objectives, stakeholder needs, business rules, and constraints.
3. **Express** requirements so each one is necessary, unambiguous, singular, feasible, verifiable, and traceable.
4. **Bound** the scope explicitly, including what is out of scope.
5. **Trace** every requirement upward to a business objective or stakeholder need, and downward to an acceptance criterion and verification method.
6. **Expose** gaps, conflicts, and unresolved decisions as open questions or risks — never silently invent them.

### Key principles

- **Business, not solution:** describe required business outcomes and capabilities, not UI design, architecture, or vendor choices. Technology may appear only as a constraint.
- **Evidence over opinion:** every objective, metric, and requirement cites its source (interview, document, regulation, data).
- **One requirement, one idea:** split compound statements until each is independently verifiable.
- **No orphan requirements:** a requirement without a business objective or stakeholder need is either unnecessary or misclassified.
- **No silent assumptions:** unresolved items are recorded as `OQ-xxx`, `ASM-xxx`, or `RSK-xxx`.

---

## 2. Inputs

### 2.1 Business foundation (fill in)

- **Organization / Business unit:** [Insert]
- **Initiative name:** [Insert]
- **Executive sponsor / business owner:** [Insert]
- **Problem owner:** [Insert]
- **Target customers / affected users:** [Describe]
- **Trigger for the initiative:** [e.g., regulation, revenue loss, cost pressure, competitive threat, operational incident]
- **Target timeline / key dates:** [Insert]
- **Budget or funding envelope (if known):** [Insert]
- **Known constraints:** [Regulatory, contractual, budget, headcount, data residency, legacy systems, deadlines]
- **Success definition in the sponsor's words:** [Quote or paraphrase]

### 2.2 Source evidence (attach or list)

| Source ID | Source | Type | Owner | Date / Version | What it evidences |
|---|---|---|---|---|---|
| SRC-001 | [Insert] | [Interview / report / policy / data extract / workshop] | [Insert] | [Insert] | [Business problem, metric baseline, rule] |
| SRC-002 | [Insert] | [Insert] | [Insert] | [Insert] | [Insert] |
| SRC-003 | [Insert] | [Insert] | [Insert] | [Insert] | [Insert] |

> If a claim cannot be sourced, mark it `[Unverified]` and raise an `OQ-xxx`.

### 2.3 House template (optional)

If a corporate BRD template is mandated, follow it and map its sections to the structure in Section 4. The repository template at `requirements/BRD-Template.md` may be used as the presentation layer; this prompt governs the content quality.

---

## 3. Requirement Quality Rules (IEEE 29148-2018)

### 3.1 Characteristics of each individual requirement

Every `BR-xxx` must satisfy all of the following. Reject and rewrite any requirement that fails one.

| Characteristic | Test to apply |
|---|---|
| **Necessary** | If removed, a business objective or stakeholder need is no longer met. |
| **Implementation-free** | States the required outcome or capability, not the mechanism, product, or design. |
| **Unambiguous** | Only one interpretation is possible to a informed reader; terms are in the glossary. |
| **Consistent** | Does not contradict another requirement, business rule, or constraint. |
| **Complete** | Contains everything needed to judge satisfaction: actor, trigger, outcome, and any condition or limit. |
| **Singular** | Expresses exactly one requirement; no "and/or" chains of unrelated obligations. |
| **Feasible** | Achievable within known business, legal, budget, and time constraints. |
| **Traceable** | Has a unique ID and a named source (`BO-xxx` or `SN-xxx`). |
| **Verifiable** | An objective acceptance criterion and verification method can be defined. |

### 3.2 Characteristics of the requirement set

The finished BRD must be:

- **Complete** — every objective has requirements; every requirement has a source.
- **Consistent** — no duplicate, overlapping, or contradictory requirements.
- **Feasible** — the set can be delivered within the stated constraints.
- **Bounded** — scope boundaries and exclusions are explicit.
- **Comprehensible** — readable by business stakeholders without technical translation.
- **Able to be validated** — each requirement can be confirmed by the business owner.

### 3.3 Requirement syntax

Use this form for business requirements:

> **[BR-xxx]** [Condition or trigger, if any], the [business actor or organization] **shall** [required capability or outcome] [object and qualifying constraint].

Rules:

- Use **shall** for mandatory requirements, **should** only for genuinely optional/desirable outcomes, and **may** for permitted options. Never use "will", "must", "can", or "needs to" as the normative verb.
- State one capability per requirement. Move compound detail into separate requirements or a business rule.
- Quantify wherever a quantity matters: volume, frequency, time, accuracy, cost, percentage.
- Avoid unverifiable words: *fast, user-friendly, robust, seamless, efficient, world-class, as needed, etc.* Replace them with a measurable criterion.
- Do not embed solution design. "The business shall approve a claim within 2 business days" is a requirement; "the system shall use a React workflow" is a design decision.

### 3.4 Identifier scheme

| Prefix | Meaning | Example |
|---|---|---|
| `BO-xxx` | Business objective | BO-001 |
| `MET-xxx` | Success metric / KPI | MET-001 |
| `STK-xxx` | Stakeholder | STK-001 |
| `SN-xxx` | Stakeholder need | SN-001 |
| `BR-xxx` | Business requirement | BR-001 |
| `BRU-xxx` | Business rule | BRU-001 |
| `CON-xxx` | Constraint | CON-001 |
| `ASM-xxx` | Assumption | ASM-001 |
| `DEP-xxx` | Dependency | DEP-001 |
| `RSK-xxx` | Risk | RSK-001 |
| `OQ-xxx` | Open question | OQ-001 |
| `AC-xxx` | Acceptance criterion | AC-001 |

IDs are permanent. Never renumber after review; mark withdrawn items `Withdrawn` and keep the row.

---

## 4. Required Document Structure

Produce the BRD in the following order. Do not omit a section; if a section is not applicable, state why in one sentence.

### 4.1 Document control

- Title, document number, version, status (`Draft` / `In review` / `Approved` / `Baselined`).
- Author, contributors, reviewers, approver.
- Version history table (version, date, author, change summary).
- Distribution list and confidentiality classification.

### 4.2 Executive summary

One page maximum, written for an executive audience:

- The business problem and its quantified impact.
- The proposed business change in one paragraph.
- Expected benefits and the metrics that prove them.
- Investment, timeline, and major risks at headline level.
- The decision being requested from the approver.

### 4.3 Business context and problem statement

- Current-state process, with a diagram where it aids understanding (Mermaid preferred).
- Who is affected and how, with evidence.
- Cost of inaction: revenue, cost, risk, compliance, customer impact.
- Root causes, distinguished from symptoms.
- Why now (trigger and urgency).

### 4.4 Business drivers and objectives

| ID | Business driver | Objective (outcome, not activity) | Metric ID | Baseline | Target | Timeframe | Source |
|---|---|---|---|---|---|---|---|
| BO-001 | [Driver] | [Outcome] | MET-001 | [Current value] | [Target value] | [Date] | [SRC-xxx] |

For each metric, define: definition, formula, data source, owner, frequency, and baseline date. A target without a baseline and a measurement method is not a valid objective.

### 4.5 Scope

- **In scope:** business capabilities, processes, organizational units, channels, data domains, and geographies covered.
- **Out of scope:** explicitly excluded items, with the reason.
- **Deferred:** items intentionally postponed to a later phase.
- **Boundaries:** where this initiative starts and stops relative to adjacent programs.

### 4.6 Stakeholders and needs

| ID | Stakeholder / group | Role in the business | Interest | Influence | Needs (`SN-xxx`) | Source |
|---|---|---|---|---|---|---|
| STK-001 | [Group] | [Role] | [What they care about] | [High/Med/Low] | [SN-001] | [SRC-xxx] |

Then list stakeholder needs individually:

| ID | Stakeholder | Need statement | Current pain | Evidence | Priority |
|---|---|---|---|---|---|
| SN-001 | STK-001 | [Need, in the stakeholder's terms] | [Pain] | [SRC-xxx] | [Must/Should/Could] |

Include negative stakeholders and those who can block adoption.

### 4.7 Business requirements

Group requirements by business capability or process area. Use one table per group.

| ID | Requirement (`shall` statement) | Rationale | Source | Priority | Acceptance criteria | Verification method | Status |
|---|---|---|---|---|---|---|---|
| BR-001 | [Statement] | [Why it is needed] | BO-001 / SN-001 | Must | AC-001 | [Review / Test / Inspection / Demonstration / Analysis] | Draft |

Priority scheme: **Must** (without it the initiative fails), **Should** (significant value, workaround exists), **Could** (desirable), **Won't** (explicitly excluded this release). If the organization uses the 1–5 value scale from `requirements/BRD-Template.md`, include the mapping.

Every requirement must have at least one acceptance criterion. Acceptance criteria must be objectively decidable and must not restate the requirement verbatim.

### 4.8 Business rules

| ID | Rule | Type | Scope | Enforcement owner | Source |
|---|---|---|---|---|---|
| BRU-001 | [Rule, e.g., "A refund above 500 EUR requires manager approval"] | [Policy / Legal / Calculation / Decision] | [Process or domain] | [Role] | [SRC-xxx] |

### 4.9 Constraints

| ID | Constraint | Type | Imposed by | Impact | Source |
|---|---|---|---|---|---|
| CON-001 | [Constraint] | [Regulatory / Legal / Budget / Time / Contractual / Technical / Organizational] | [Party] | [Effect on the solution space] | [SRC-xxx] |

Constraints are non-negotiable boundaries. Preferences belong in assumptions or design inputs, not here.

### 4.10 Assumptions, dependencies, and risks

| ID | Item | Type | Description | Impact if false | Owner | Validation / mitigation | Due |
|---|---|---|---|---|---|---|---|
| ASM-001 | [Assumption] | Assumption | [What is assumed true] | [Consequence] | [Owner] | [How and when it will be validated] | [Date] |
| DEP-001 | [Dependency] | Dependency | [External deliverable or decision] | [Consequence] | [Owner] | [Tracking action] | [Date] |
| RSK-001 | [Risk] | Risk | [Cause → event → effect] | [Severity] | [Owner] | [Mitigation / contingency] | [Date] |

### 4.11 Traceability

Provide a forward and backward traceability matrix:

| Business objective | Stakeholder need | Business requirement | Acceptance criteria | Downstream PRD/SRS ID |
|---|---|---|---|---|
| BO-001 | SN-001 | BR-001 | AC-001 | [TBD] |

Report coverage explicitly:

- Objectives with no requirements.
- Requirements with no objective or need (orphans).
- Needs with no requirement.
- Requirements with no acceptance criterion or verification method.

### 4.12 Open questions and decisions

| ID | Question / decision needed | Why it matters | Owner | Needed by | Status | Resolution |
|---|---|---|---|---|---|---|
| OQ-001 | [Question] | [Blocked requirement or scope] | [Name] | [Date] | Open | — |

Do not resolve an open question by assumption. If a decision was taken during elicitation, record it with date, decision maker, and rationale.

### 4.13 Glossary and references

- Glossary of business terms, abbreviations, and acronyms, including any term whose meaning is disputed.
- References with name, version, location, and access date.

### 4.14 Approval

| Role | Name | Decision | Signature / date |
|---|---|---|---|
| Executive sponsor | [Name] | [Approve / Approve with conditions / Reject] | [Date] |
| Business owner | [Name] | [Approve / Reject] | [Date] |
| Product manager / product owner | [Name] | [Approve / Reject] | [Date] |
| Compliance / legal (if applicable) | [Name] | [Approve / Reject] | [Date] |

State the conditions of approval and the baseline version being approved.

### 4.15 Appendix

Supporting analysis, process maps, interview notes, data extracts, and any material referenced above.

---

## 5. Verification and Review Checklist

Before delivering, verify the document against each item and report the result.

### 5.1 Requirement quality

- [ ] Every requirement uses the `shall` syntax and contains one obligation.
- [ ] Every requirement is free of solution/design language.
- [ ] Every requirement is quantified where quantity affects acceptance.
- [ ] No vague qualifiers remain (*fast, easy, robust, efficient, etc.*).
- [ ] Every term with a disputed or specialized meaning is in the glossary.
- [ ] No requirement duplicates or contradicts another.
- [ ] Every requirement has a unique, permanent ID.

### 5.2 Completeness and traceability

- [ ] Every business objective has at least one requirement.
- [ ] Every requirement traces to an objective or stakeholder need.
- [ ] Every requirement has at least one acceptance criterion.
- [ ] Every requirement has a verification method.
- [ ] Every stakeholder group has at least one need recorded.
- [ ] Scope, exclusions, assumptions, dependencies, and risks are all populated.
- [ ] Every open question has an owner and a needed-by date.

### 5.3 Business validation

- [ ] The problem statement is evidenced, not asserted.
- [ ] Baseline and target values are sourced and measurable.
- [ ] Benefits and costs are stated in business terms.
- [ ] The sponsor confirms the problem and desired outcome are represented accurately.
- [ ] The document can be understood by a business reader without technical translation.

Report any failed check as an open question or a defect against the affected requirement ID. Do not mark the document ready for approval while a Must requirement fails a check.

---

## 6. Output Instructions

1. **Start with a short validation summary:** list the inputs received, what is missing, and the top three risks to requirement quality.
2. **Then output the full BRD** using the structure in Section 4, in Markdown.
3. **Use tables** for objectives, stakeholders, requirements, rules, constraints, assumptions, risks, traceability, and open questions.
4. **Use Mermaid** for current-state and proposed-state process flows where a diagram clarifies the business change.
5. **Cite sources inline** using `SRC-xxx`; mark unsourced statements `[Unverified]`.
6. **Do not invent** metrics, baselines, stakeholders, or decisions. Where information is absent, write `[TBD: OQ-xxx]` and add the question to Section 4.12.
7. **Do not drift into solution design.** If a design idea is relevant, record it as an assumption, constraint, or note for the downstream PRD/SAD.
8. **Close with a readiness statement:** `Ready for review`, `Ready with conditions`, or `Not ready`, with the blocking items listed by ID.

---

## 7. Anti-Patterns to Avoid

| Anti-pattern | Why it fails IEEE 29148 quality | Correct approach |
|---|---|---|
| "The system shall be user-friendly" | Not verifiable or unambiguous | Define the measurable outcome and its acceptance criterion |
| "The system shall use Kubernetes" | Solution prescription, not a business requirement | Record as a constraint or leave to the SAD |
| "Users can view and edit and export reports" | Compound, not singular | Split into three requirements |
| "Improve efficiency by 20%" with no baseline | Not verifiable | State baseline, metric definition, and measurement method |
| Requirements with no source | Not traceable | Link to `BO-xxx` / `SN-xxx` or remove |
| Assumptions presented as facts | Not correct or validatable | Record as `ASM-xxx` with a validation action |
| Scope defined only by what is included | Not bounded | State exclusions and deferrals explicitly |
| Open questions resolved silently in the text | Hides unresolved conflict | Keep `OQ-xxx` open until the owner decides |

---

## 8. Fill-In Block

Replace the placeholders below before running the prompt, or attach the equivalent documents.

```text
ORGANIZATION:
INITIATIVE:
EXECUTIVE SPONSOR:
BUSINESS OWNER:
PROBLEM STATEMENT (sponsor's words):
TRIGGER / WHY NOW:
TARGET OUTCOMES AND METRICS:
KNOWN CONSTRAINTS:
KNOWN STAKEHOLDERS:
TARGET TIMELINE:
SOURCE DOCUMENTS:
HOUSE TEMPLATE (optional):
```

**Attach or paste:** [business case, sponsor brief, stakeholder interview notes, current-state process, regulatory requirements, baseline metrics, existing system documentation]
