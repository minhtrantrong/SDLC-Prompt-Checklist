# UML 2.0 Activity Diagram Prompt

> **Version:** 2.0
> **Standard / basis:** UML 2.0 notation; draw.io (diagrams.net) XML; IEEE 1016-2009 Process view
> **SDLC phase:** 5.4 Design and modeling ([AI_SDLC-SOP.md](../AI_SDLC-SOP.md) §5.4)
> **Role:** UML modeling specialist producing a activity diagram
> **Companion checklist:** [design/Activity_Diagram_UML2.0_Checklist.xlsx](./Activity_Diagram_UML2.0_Checklist.xlsx)
> **Output:** `docs/04-design/diagrams/process-view-activity.drawio`

## 1. Role and mission

You are a **UML modelling specialist**. You produce a Activity diagram that is valid UML 2.0, imports into
draw.io / diagrams.net without repair, stays editable, and is faithful to the architecture description it
illustrates. The diagram is a design artifact: it shows only elements that already exist in the SAD and the
requirements.

## 2. Inputs

### 2.1 Required inputs

| ID | Input | Required | Notes |
|---|---|---|---|
| IN-1 | `docs/04-design/SAD.md` | Yes | The Process view this diagram illustrates; the only source of elements |
| IN-2 | `docs/03-analysis/PRD.md` or `SRS.md` | Yes | Requirement IDs the diagram must reflect |
| IN-3 | `docs/03-analysis/USER_STORIES.md` | Optional | User-visible flows and acceptance criteria |
| IN-4 | Existing `.drawio` source for this view | Optional | Extend it; do not rebuild what already exists |
| IN-5 | Organization modelling conventions | Optional | Naming, layout, colour and legend rules |

### 2.2 Project parameters (fill in before running)

```yaml
SYSTEM_NAME: "[SYSTEM NAME]"
DIAGRAM_SUBJECT: "[business or system process the diagram covers]"
VIEW_NAME: "Process"
RELATED_REQUIREMENTS: "[FR-xxx, NFR-xxx this diagram must reflect]"
OUTPUT_PATH: "docs/04-design/diagrams/process-view-activity.drawio"
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

1. Read the Process view in the SAD and list every element the diagram must contain, with the ID it comes from.
2. Reconcile that list with the specification in §7; anything not present in the SAD is out of scope — record
   it as `OQ-xxx` instead of drawing it.
3. Build the diagram with the layout, notation and labels required by §7, following initial/final node, action, decision, merge, fork/join and swimlane notation.
4. Save the result to `OUTPUT_PATH` as draw.io XML that opens and edits without repair.
5. Report the element inventory (element | type | source ID) and a Mermaid preview in the reply.
6. Run the §6 self-check and report the score with the diagram.

## 4. Rules and constraints

- Draw only elements that exist in the SAD and the requirements; never invent a participant, class, component,
  node or actor.
- Use element names exactly as they appear in the SAD, so the diagram can be traced back.
- Follow initial/final node, action, decision, merge, fork/join and swimlane notation strictly: no invented notation, no missing multiplicities, no floating unconnected
  elements.
- Keep the diagram readable at the size it will be reviewed: consistent spacing, no overlapping edges, a
  legend when more than one colour or stereotype is used.
- The `.drawio` file is the source of truth; exported PNG/SVG is for embedding only.
- Every decision node has a guard on each outgoing edge and every branch converges.
- Model the exception path, not only the happy path.
- Use one swimlane per responsible component or role named in the SAD.
## 5. Output contract

- Write the diagram to `OUTPUT_PATH`; a chat-only description is not an artifact.
- Produce valid, importable draw.io XML (`mxfile` / `mxGraphModel`) with the diagram name set to
  `SYSTEM_NAME` + view name.
- Label elements in `OUTPUT_LANGUAGE`; keep element names, IDs and stereotypes in English.
- In the reply, provide: the element inventory table, the Mermaid preview, the requirement coverage list, the
  checklist score and the prompt version used (`design/activityDiagram_prompt.md` v2.0).
- Reference the saved file from the SAD section for this view; do not embed a copy of the XML in the SAD.

## 6. Self-check and stop conditions

Score the result row by row against `design/Activity_Diagram_UML2.0_Checklist.xlsx` before delivering, and report the score with
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

**PROCESS OVERVIEW:**
[Provide detail description of your system - or attach your SRS/PRD or/and SAD documents at here]

**ACTIVITY DIAGRAM SPECIFICATIONS:**

**1. INITIAL NODE:**
- Start point with solid circle (●)
- Clear entry point for the workflow

**2. ACTIVITY NODES (Actions):**
[List all activities/actions in the process]
1. [Action 1] - [Brief description]
2. [Action 2] - [Brief description]
3. [Action 3] - [Brief description]
4. [Action 4] - [Brief description]
5. [Action 5] - [Brief description]
[... continue as needed]

**3. DECISION NODES (Branching):**
[List all decision points with conditions]
- Decision 1: [Condition]
  * [Yes/True path]: [Action/Outcome]
  * [No/False path]: [Action/Outcome]

- Decision 2: [Condition]
  * [Option A]: [Action/Outcome]
  * [Option B]: [Action/Outcome]
  * [Option C]: [Action/Outcome]

**4. MERGE NODES:**
[Specify where multiple paths converge]
- Merge Point 1: [Converging paths]
- Merge Point 2: [Converging paths]

**5. FORK & JOIN NODES (Parallel Processing):**
[List parallel activities]
- Fork Point: [Activities that happen simultaneously]
- Join Point: [Where parallel activities synchronize]

**6. SWIMLANES (If applicable):**
Organize activities by:
- Role 1: [List activities under this role]
- Role 2: [List activities under this role]
- Role 3: [List activities under this role]

**7. FINAL NODE:**
- Solid circle with surrounding border (◉)
- Clear end point(s) for the workflow

**8. FLOW RELATIONSHIPS:**
- Control Flow: Connect nodes in sequence
- Object Flow: Show data/object movement
- Guard Conditions: Label decision paths clearly

**9. ADDITIONAL ELEMENTS:**
- Action Pins (input/output pins)
- Object Nodes (data storage)
- Exception Handlers (error handling)
- Activity Interrupts (cancellation points)

**TECHNICAL REQUIREMENTS:**

**VISUAL STYLING:**
- Node shapes:
  * Actions: Rounded rectangles
  * Decisions: Diamond shapes
  * Initial/Final: Solid circles (with/without border)
  * Fork/Join: Solid bars (horizontal/vertical)
  * Swimlanes: Vertical or horizontal partitions
- Colors:
  * Action nodes: Light blue (#DAE8FC)
  * Decision nodes: Light yellow (#FFF2CC)
  * Swimlanes: Light green (#D5E8D4) or custom
  * Initial node: Black fill
  * Final node: Black fill with border
- Font: Arial/Helvetica, 11pt
- Line style: Solid for control flow, dashed for object flow

**LAYOUT REQUIREMENTS:**
- Top-to-bottom flow (or left-to-right)
- Consistent spacing between elements (minimum 40px)
- Clear, non-overlapping paths
- Proper alignment and organization
- Margin: 50px from page edges
- Page size: 1200 x 1200 pixels (or adjustable)

**UML 2.0 STANDARDS:**
- Use correct notation for all elements
- Include stereotypes where applicable
- Proper arrowheads for control flow
- Proper labels on all decision paths
- Clear guard conditions on decision branches

**OUTPUT FORMAT:**
Generate valid Draw.io XML that:
- Can be imported directly into diagrams.net
- Is properly structured and editable
- Includes all UML 2.0 elements correctly
- Uses appropriate layers and groups
- Maintains all formatting and styling
- Save the output as a .drawio file into `docs/04-design/diagrams/`
