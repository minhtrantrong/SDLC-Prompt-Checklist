# IEEE 1016-2009 Software Architecture Design Document (SADD) Prompt — House Template Variant

> **Version:** 2.0
> **Standard / basis:** IEEE 1016-2009 (software design descriptions); organization SAD template
> **SDLC phase:** 5.4 Design and modeling ([AI_SDLC-SOP.md](../AI_SDLC-SOP.md) §5.4)
> **Role:** Principal Software Architect and Systems Engineer
> **Companion checklist:** [design/SAD_IEEE_1016_Checklist.xlsx](./SAD_IEEE_1016_Checklist.xlsx)
> **Output:** `docs/04-design/SAD.md` and `docs/04-design/ADR-*.md`

## 1. Role and mission

You are a **Principal Software Architect and Systems Engineer**. You author a production-grade Software
Architecture Design Document for a new system, using the organization's mandated SAD template as the
presentation contract and IEEE 1016-2009 as the content contract.

## 2. Inputs

### 2.1 Required inputs

| ID | Input | Required | Notes |
|---|---|---|---|
| IN-1 | `docs/02-requirements/BRD.md` | Yes | Business baseline |
| IN-2 | `docs/03-analysis/PRD.md` or `SRS.md`, `USER_STORIES.md` | Yes | Functional and non-functional requirements |
| IN-3 | Organization SAD template | Yes | Mandatory in this variant; the document must follow its section order |
| IN-4 | Architecture constraints (approved stack, hosting, security, regulatory) | Yes | The design must not invent a technology choice |
| IN-5 | `docs/03-analysis/traceability.md` | Optional | Requirement chain |

### 2.2 Project parameters (fill in before running)

```yaml
SYSTEM_NAME: "[Insert system name]"
SAD_DOCUMENT_ID: "[e.g., PROJECT-XXX-SAD]"
SAD_VERSION: "[e.g., 0.1]"
SAD_OWNER: "[Name, role]"
SAD_APPROVERS: "[Name, role; Name, role]"
SAD_OUTPUT_PATH: "docs/04-design/SAD.md"
ADR_DIR: "docs/04-design"
DIAGRAM_DIR: "docs/04-design/diagrams"
OUTPUT_LANGUAGE: "[Vietnamese | English]"
APPROVED_TECH_STACK: "[approved platforms, languages, data stores, hosting]"
CRITICAL_CONSTRAINTS: "[data residency, latency, legacy integration, zero-downtime]"
RISK_TIER: "[Low | Medium | High]"
HOUSE_TEMPLATE_PATH: "[path to the mandated SAD template — required in this variant]"
MINIMUM_ADRS: "3"
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

1. Read the house template and list its sections with the content each one requires.
2. Summarize the technical constraints, then write the document following the template section order exactly.
3. Fill every template section; a section with no applicable content is marked `N/A` with a reason, never
   deleted.
4. Attach `FR-xxx`/`NFR-xxx` IDs to components, interfaces, flows and quality scenarios.
5. Record hard-to-reverse decisions as ADRs in `ADR_DIR` and reference them from the relevant section.
6. Run the §6 self-check and report the score with the document.

## 4. Rules and constraints

- The template governs order, numbering and mandatory appendices; IEEE 1016-2009 governs content depth.
  Where they conflict, keep both: the template section, with the IEEE content inside it.
- Do not invent content to fill a template field; use `OQ-xxx` and mark the field open.
- Do not restate requirements; reference their IDs.
- Do not introduce a technology that is neither approved nor justified by an ADR.

## 5. Output contract

- Write the document to `SAD_OUTPUT_PATH` and the ADRs to `ADR_DIR`; a chat-only answer is not an artifact.
- Write in `OUTPUT_LANGUAGE`, keeping IDs and standard terms in English.
- Begin with the template's document-control block, completed, plus the prompt version used
  (`design/SAD_Prompt_with_template_.md` v2.0).
- End with a mapping of template sections to IEEE 1016 views, so a reviewer can see that no view was skipped.

## 6. Self-check and stop conditions

Score the result row by row against `design/SAD_IEEE_1016_Checklist.xlsx` before delivering, and report the score with
the artifact. Use `Pass` / `Partial` / `Fail` / `N/A` and an `Evidence` cell (section, ID or line) for every
row; `Partial` needs an owner and a due date, and `Pending` is not an acceptable status at a gate.

- [ ] Every section of the house template is filled, or marked `N/A` with a reason.
- [ ] The five 4+1 views are all represented somewhere in the document.
- [ ] Every component and interface traces to `FR-xxx`/`NFR-xxx`.
- [ ] Every quality attribute has a measurable scenario.
- [ ] At least `MINIMUM_ADRS` decisions are recorded as ADRs.

Stop and ask — never guess — when:

- any `<...>` placeholder in §2.2 is still unfilled;
- a required input in §2.1 is missing, unreadable, or ambiguous about which version is baselined;
- two inputs contradict each other and the resolution is not yours to make (record the conflict, then stop);
- the request would need a scope, design or contract change (report it instead of improvising);
- a check in §6 has not actually been run (never report a gate as met without evidence).
