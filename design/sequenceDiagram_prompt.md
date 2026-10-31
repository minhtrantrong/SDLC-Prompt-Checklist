# UML 2.0 Sequence Diagram Prompt

> **Version:** 2.0
> **Standard / basis:** UML 2.0 notation; draw.io (diagrams.net) XML; IEEE 1016-2009 Process view
> **SDLC phase:** 5.4 Design and modeling ([AI_SDLC-SOP.md](../AI_SDLC-SOP.md) §5.4)
> **Role:** UML modeling specialist producing a sequence diagram
> **Companion checklist:** [design/Sequence_Diagram_UML2.0_Checklist.xlsx](./Sequence_Diagram_UML2.0_Checklist.xlsx)
> **Output:** `docs/04-design/diagrams/process-view.drawio`

## 1. Role and mission

You are a **UML modelling specialist**. You produce a Sequence diagram that is valid UML 2.0, imports into
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
DIAGRAM_SUBJECT: "[end-to-end flow the diagram covers]"
VIEW_NAME: "Process"
RELATED_REQUIREMENTS: "[FR-xxx, NFR-xxx this diagram must reflect]"
OUTPUT_PATH: "docs/04-design/diagrams/process-view.drawio"
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
3. Build the diagram with the layout, notation and labels required by §7, following lifeline, message, activation, fragment and gate notation.
4. Save the result to `OUTPUT_PATH` as draw.io XML that opens and edits without repair.
5. Report the element inventory (element | type | source ID) and a Mermaid preview in the reply.
6. Run the §6 self-check and report the score with the diagram.

## 4. Rules and constraints

- Draw only elements that exist in the SAD and the requirements; never invent a participant, class, component,
  node or actor.
- Use element names exactly as they appear in the SAD, so the diagram can be traced back.
- Follow lifeline, message, activation, fragment and gate notation strictly: no invented notation, no missing multiplicities, no floating unconnected
  elements.
- Keep the diagram readable at the size it will be reviewed: consistent spacing, no overlapping edges, a
  legend when more than one colour or stereotype is used.
- The `.drawio` file is the source of truth; exported PNG/SVG is for embedding only.
- Lifelines are components or actors that already exist in the SAD; never add a participant for convenience.
- Every message carries the requirement ID it satisfies, and every alternative path is a fragment with a guard.
- Include the failure branches: timeout, rejection, permission denied, not found.
## 5. Output contract

- Write the diagram to `OUTPUT_PATH`; a chat-only description is not an artifact.
- Produce valid, importable draw.io XML (`mxfile` / `mxGraphModel`) with the diagram name set to
  `SYSTEM_NAME` + view name.
- Label elements in `OUTPUT_LANGUAGE`; keep element names, IDs and stereotypes in English.
- In the reply, provide: the element inventory table, the Mermaid preview, the requirement coverage list, the
  checklist score and the prompt version used (`design/sequenceDiagram_prompt.md` v2.0).
- Reference the saved file from the SAD section for this view; do not embed a copy of the XML in the SAD.

## 6. Self-check and stop conditions

Score the result row by row against `design/Sequence_Diagram_UML2.0_Checklist.xlsx` before delivering, and report the score with
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

**SEQUENCE DIAGRAM SPECIFICATIONS:**

**1. LIFELINES (Participants):**
[List all participants in the interaction]

**Actors/External Entities:**
1. [Actor Name] - [Role description] - [Color: #COLOR]

**Internal Components:**
2. [Component/Class Name] - [Responsibility] - [Color: #COLOR]
3. [Component/Class Name] - [Responsibility] - [Color: #COLOR]
4. [Component/Class Name] - [Responsibility] - [Color: #COLOR]
5. [Component/Class Name] - [Responsibility] - [Color: #COLOR]

**Databases/External Systems:**
6. [Database/External System] - [Purpose] - [Color: #COLOR]

**2. MESSAGES (In chronological order):**

**Synchronous Messages (→ Solid arrow with filled head):**
1. [Sender] → [Receiver] : [Message Name](parameters)
   - Description: [What this message does]
   - Return: [Return value if any]

2. [Sender] → [Receiver] : [Message Name](parameters)
   - Description: [What this message does]
   - Return: [Return value if any]

**Asynchronous Messages (→ Solid arrow with open head):**
3. [Sender] → [Receiver] : [Message Name](parameters)
   - Description: [What this message does]
   - No return expected

**Return Messages (→ Dashed arrow):**
4. [Receiver] → [Sender] : [Return Value]
   - Description: [What is returned]

**Self-Messages (Self-loop):**
5. [Participant] → [Self] : [Message Name](parameters)
   - Description: [Internal processing]

**3. INTERACTION FRAMES (UML 2.0):**

**alt (Alternative):**
- Condition 1: [Condition description]
  * Messages: [List messages in this branch]
- Condition 2: [Condition description]
  * Messages: [List messages in this branch]
- Else: [Default branch]
  * Messages: [List messages]

**opt (Optional):**
- Condition: [Condition description]
  * Messages: [List messages executed only if condition is met]

**loop (Iteration):**
- Condition: [Loop condition]
  * Messages: [List messages that repeat]

**par (Parallel):**
- Parallel Block 1: [Description]
  * Messages: [List messages executed in parallel]
- Parallel Block 2: [Description]
  * Messages: [List messages executed in parallel]

**break (Exception):**
- Exception Condition: [Condition]
  * Messages: [List exception handling messages]

**ref (Reference):**
- Reference to: [Other interaction diagram name]
  * Purpose: [Why this interaction is referenced]

**4. CREATION AND DESTRUCTION:**
- Object Creation: [Message] creates [Object]
- Object Destruction: [Message] destroys [Object]
- Deletion marker: [X] at end of lifeline

**5. GATES (Interaction Points):**
- Input Gate: [Where interaction enters]
- Output Gate: [Where interaction exits]

**6. STATE INVARIANTS:**
- Condition at specific time: {condition description}
- Shown as: [Condition] at specific point on lifeline

**TECHNICAL REQUIREMENTS:**

**VISUAL STYLING:**
- Lifeline shapes: Rectangles with underlined names
- Lifeline style: "ClassName" (objectName: ClassName)
- Activation bars: Thin vertical rectangles
- Message arrows:
  * Synchronous: Solid line, filled arrowhead
  * Asynchronous: Solid line, open arrowhead
  * Return: Dashed line, open arrowhead
  * Self-message: Solid line, filled arrowhead (loop back to self)
- Colors:
  * Actor lifelines: Light blue (#DAE8FC)
  * Component lifelines: Light green (#D5E8D4)
  * Database lifelines: Light yellow (#FFF2CC)
  * Activation bars: Same color as lifeline (darker shade)
  * Alt/opt/loop frames: Light gray (#F5F5F5)
- Font: Arial/Helvetica, 10pt
- Message labels: Italic for parameter names

**LAYOUT REQUIREMENTS:**
- Left-to-right flow (time top-to-bottom)
- Top-to-bottom ordering of messages
- Consistent spacing (minimum 40px between lifelines)
- Proper alignment of activation bars
- Margin: 50px from page edges
- Page size: 1200 x 800 pixels (adjustable)
- Frames: Clearly bordered with labels

**UML 2.0 STANDARDS:**
- Correct lifeline notation: :ClassName or object:ClassName
- Proper message arrow notation
- Activation bars shown correctly
- Interaction frames with proper operators
- Correct nesting of frames
- Proper gate notation
- Clear, readable labels

**OUTPUT FORMAT:**
Generate valid Draw.io XML that:
- Can be imported directly into diagrams.net
- Is properly structured and editable
- Includes all UML 2.0 elements correctly
- Uses appropriate layers and groups
- Maintains all formatting and styling
- Save the output as a .drawio file into `docs/04-design/diagrams/`
