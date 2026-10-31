# UML 2.0 Use case Diagram Prompt

> **Version:** 2.0
> **Standard / basis:** UML 2.0 notation; draw.io (diagrams.net) XML; IEEE 1016-2009 Scenarios view
> **SDLC phase:** 5.4 Design and modeling ([AI_SDLC-SOP.md](../AI_SDLC-SOP.md) §5.4)
> **Role:** UML modeling specialist producing a use case diagram
> **Companion checklist:** [design/UseCase_Document_UML2.0_Checklist.xlsx](./UseCase_Document_UML2.0_Checklist.xlsx)
> **Output:** `docs/04-design/diagrams/scenarios-view.drawio`

## 1. Role and mission

You are a **UML modelling specialist**. You produce a Use case diagram that is valid UML 2.0, imports into
draw.io / diagrams.net without repair, stays editable, and is faithful to the architecture description it
illustrates. The diagram is a design artifact: it shows only elements that already exist in the SAD and the
requirements.

## 2. Inputs

### 2.1 Required inputs

| ID | Input | Required | Notes |
|---|---|---|---|
| IN-1 | `docs/04-design/SAD.md` | Yes | The Scenarios view this diagram illustrates; the only source of elements |
| IN-2 | `docs/03-analysis/PRD.md` or `SRS.md` | Yes | Requirement IDs the diagram must reflect |
| IN-3 | `docs/03-analysis/USER_STORIES.md` | Optional | User-visible flows and acceptance criteria |
| IN-4 | Existing `.drawio` source for this view | Optional | Extend it; do not rebuild what already exists |
| IN-5 | Organization modelling conventions | Optional | Naming, layout, colour and legend rules |

### 2.2 Project parameters (fill in before running)

```yaml
SYSTEM_NAME: "[SYSTEM NAME]"
DIAGRAM_SUBJECT: "[system or subsystem the diagram covers]"
VIEW_NAME: "Scenarios"
RELATED_REQUIREMENTS: "[FR-xxx, NFR-xxx this diagram must reflect]"
OUTPUT_PATH: "docs/04-design/diagrams/scenarios-view.drawio"
DIAGRAM_DIR: "docs/04-design/diagrams"
OUTPUT_LANGUAGE: "[Vietnamese | English]"
LABEL_STYLE: "[verb phrases for actions, noun phrases for elements]"
INCLUDE_LEGEND: "yes"
INCLUDE_MERMAID_PREVIEW: "yes"
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

1. Read the Scenarios view in the SAD and list every element the diagram must contain, with the ID it comes from.
2. Reconcile that list with the specification in §7; anything not present in the SAD is out of scope — record
   it as `OQ-xxx` instead of drawing it.
3. Build the diagram with the layout, notation and labels required by §7, following actor, use case, system boundary, include/extend and generalization notation.
4. Save the result to `OUTPUT_PATH` as draw.io XML that opens and edits without repair.
5. Report the element inventory (element | type | source ID) and a Mermaid preview in the reply.
6. Run the §6 self-check and report the score with the diagram.

## 4. Rules and constraints

- Draw only elements that exist in the SAD and the requirements; never invent a participant, class, component,
  node or actor.
- Use element names exactly as they appear in the SAD, so the diagram can be traced back.
- Follow actor, use case, system boundary, include/extend and generalization notation strictly: no invented notation, no missing multiplicities, no floating unconnected
  elements.
- Keep the diagram readable at the size it will be reviewed: consistent spacing, no overlapping edges, a
  legend when more than one colour or stereotype is used.
- The `.drawio` file is the source of truth; exported PNG/SVG is for embedding only.
- Every use case maps to an `FR-xxx` or `US-xxx`; a use case with no requirement is out of scope.
- `«include»` is used only for mandatory shared behaviour, `«extend»` only for optional behaviour with a condition.
- Actors are roles, not named individuals.
## 5. Output contract

- Write the diagram to `OUTPUT_PATH`; a chat-only description is not an artifact.
- Produce valid, importable draw.io XML (`mxfile` / `mxGraphModel`) with the diagram name set to
  `SYSTEM_NAME` + view name.
- Label elements in `OUTPUT_LANGUAGE`; keep element names, IDs and stereotypes in English.
- In the reply, provide: the element inventory table, the Mermaid preview, the requirement coverage list, the
  checklist score and the prompt version used (`design/useCase_prompt.md` v2.0).
- Reference the saved file from the SAD section for this view; do not embed a copy of the XML in the SAD.

## 6. Self-check and stop conditions

Score the result row by row against `design/UseCase_Document_UML2.0_Checklist.xlsx` before delivering, and report the score with
the artifact. Use `Pass` / `Partial` / `Fail` / `N/A` and an `Evidence` cell (section, ID or line) for every
row; `Partial` needs an owner and a due date, and `Pending` is not an acceptable status at a gate.

- [ ] Every element in the diagram traces to the SAD and a requirement ID; no orphan element.
- [ ] Notation is valid UML 2.0 for every element and relationship.
- [ ] The file imports into draw.io and every element remains editable.
- [ ] The diagram covers the view it claims to represent, with no missing flow or relationship.
- [ ] Labels follow the agreed style and language; a legend is present where needed.

Stop and ask — never guess — when:

- any `<...>` placeholder in §2.2 is still unfilled;
- a required input in §2.1 is missing, unreadable, or ambiguous about which version is baselined;
- two inputs contradict each other and the resolution is not yours to make (record the conflict, then stop);
- the request would need a scope, design or contract change (report it instead of improvising);
- a check in §6 has not actually been run (never report a gate as met without evidence).

---

## 7. Detailed specification

**SYSTEM OVERVIEW:**
[Provide detail description of your system - or attach your SRS/PRD or/and SAD documents at here]

**ACTORS (External Entities):**
Primary Actors:
1. [Actor 1] - [Role description]
2. [Actor 2] - [Role description]
3. [Actor 3] - [Role description]

Secondary Actors:
4. [Actor 4] - [Role description]
5. [Actor 5] - [Role description]

**USE CASES (Functional Requirements):**
Functional Areas:
- [Module 1]: [List use cases]
- [Module 2]: [List use cases]
- [Module 3]: [List use cases]

**RELATIONSHIPS:**
- Include relationships (required functionality)
- Extend relationships (optional functionality)
- Generalization relationships (inheritance)

**SPECIFICATIONS:**
- Use correct UML notation
- Include system boundary box
- Proper actor stick figures
- Clear use case oval shapes
- Include all <<include>> and <<extend>> stereotypes where applicable

**TECHNICAL FORMAT:**
Generate the output as a .drawio file and save it into `docs/04-design/diagrams/`
