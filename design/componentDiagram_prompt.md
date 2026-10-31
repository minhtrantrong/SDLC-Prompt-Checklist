# UML 2.0 Component Diagram Prompt

> **Version:** 2.0
> **Standard / basis:** UML 2.0 notation; draw.io (diagrams.net) XML; IEEE 1016-2009 Development view
> **SDLC phase:** 5.4 Design and modeling ([AI_SDLC-SOP.md](../AI_SDLC-SOP.md) §5.4)
> **Role:** UML modeling specialist producing a component diagram
> **Companion checklist:** [design/Component_Diagram_UML2.0_Checklist.xlsx](./Component_Diagram_UML2.0_Checklist.xlsx)
> **Output:** `docs/04-design/diagrams/development-view.drawio`

## 1. Role and mission

You are a **UML modelling specialist**. You produce a Component diagram that is valid UML 2.0, imports into
draw.io / diagrams.net without repair, stays editable, and is faithful to the architecture description it
illustrates. The diagram is a design artifact: it shows only elements that already exist in the SAD and the
requirements.

## 2. Inputs

### 2.1 Required inputs

| ID | Input | Required | Notes |
|---|---|---|---|
| IN-1 | `docs/04-design/SAD.md` | Yes | The Development view this diagram illustrates; the only source of elements |
| IN-2 | `docs/03-analysis/PRD.md` or `SRS.md` | Yes | Requirement IDs the diagram must reflect |
| IN-3 | `docs/03-analysis/USER_STORIES.md` | Optional | User-visible flows and acceptance criteria |
| IN-4 | Existing `.drawio` source for this view | Optional | Extend it; do not rebuild what already exists |
| IN-5 | Organization modelling conventions | Optional | Naming, layout, colour and legend rules |

### 2.2 Project parameters (fill in before running)

```yaml
SYSTEM_NAME: "[SYSTEM NAME]"
DIAGRAM_SUBJECT: "[layer or subsystem the diagram covers]"
VIEW_NAME: "Development"
RELATED_REQUIREMENTS: "[FR-xxx, NFR-xxx this diagram must reflect]"
OUTPUT_PATH: "docs/04-design/diagrams/development-view.drawio"
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

1. Read the Development view in the SAD and list every element the diagram must contain, with the ID it comes from.
2. Reconcile that list with the specification in §7; anything not present in the SAD is out of scope — record
   it as `OQ-xxx` instead of drawing it.
3. Build the diagram with the layout, notation and labels required by §7, following component, provided/required interface, port, connector and package notation.
4. Save the result to `OUTPUT_PATH` as draw.io XML that opens and edits without repair.
5. Report the element inventory (element | type | source ID) and a Mermaid preview in the reply.
6. Run the §6 self-check and report the score with the diagram.

## 4. Rules and constraints

- Draw only elements that exist in the SAD and the requirements; never invent a participant, class, component,
  node or actor.
- Use element names exactly as they appear in the SAD, so the diagram can be traced back.
- Follow component, provided/required interface, port, connector and package notation strictly: no invented notation, no missing multiplicities, no floating unconnected
  elements.
- Keep the diagram readable at the size it will be reviewed: consistent spacing, no overlapping edges, a
  legend when more than one colour or stereotype is used.
- The `.drawio` file is the source of truth; exported PNG/SVG is for embedding only.
- Every provided interface has a matching required interface on the consuming component.
- Component boundaries follow the SAD decomposition; no component may span two SAD components.
## 5. Output contract

- Write the diagram to `OUTPUT_PATH`; a chat-only description is not an artifact.
- Produce valid, importable draw.io XML (`mxfile` / `mxGraphModel`) with the diagram name set to
  `SYSTEM_NAME` + view name.
- Label elements in `OUTPUT_LANGUAGE`; keep element names, IDs and stereotypes in English.
- In the reply, provide: the element inventory table, the Mermaid preview, the requirement coverage list, the
  checklist score and the prompt version used (`design/componentDiagram_prompt.md` v2.0).
- Reference the saved file from the SAD section for this view; do not embed a copy of the XML in the SAD.

## 6. Self-check and stop conditions

Score the result row by row against `design/Component_Diagram_UML2.0_Checklist.xlsx` before delivering, and report the score with
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

**COMPONENT DIAGRAM SPECIFICATIONS:**

**1. SYSTEM BOUNDARY:**
- System name and version
- Clear boundary box with system label
- External components shown outside the boundary
- Internal components inside the boundary

**2. COMPONENTS (List all architectural components):**

**Core Components:**
1. [Component Name] - [Brief description/responsibility]
2. [Component Name] - [Brief description/responsibility]
3. [Component Name] - [Brief description/responsibility]

**Subsystems:**
4. [Subsystem Name] - [Contains multiple components]
5. [Subsystem Name] - [Contains multiple components]

**External Components:**
6. [External Component] - [Third-party service]
7. [External Component] - [External system]

**3. INTERFACES:**

**Provided Interfaces (Component provides services):**
- Interface 1: [Name] - [Description of services offered]
- Interface 2: [Name] - [Description of services offered]

**Required Interfaces (Component needs services):**
- Interface 3: [Name] - [Description of services required]
- Interface 4: [Name] - [Description of services required]

**4. RELATIONSHIPS:**

**Dependencies:**
- Component A depends on Component B (uses)
- Component C requires Interface X

**Associations:**
- Component A communicates with Component B
- Bi-directional or uni-directional

**Realizations:**
- Component A realizes Interface Y
- Subsystem implements multiple interfaces

**5. PORT CONNECTIONS:**
- Ports with provided interfaces (shown as lollipop)
- Ports with required interfaces (shown as socket)
- Connect ports with assembly connectors

**6. DEPLOYMENT CONSIDERATIONS:**
- Which components are deployable
- Runtime instances
- Version information

**TECHNICAL REQUIREMENTS:**

**VISUAL STYLING:**
- Component node shapes: Rectangles with component stereotype
- Interface shapes: Circle (provided) and half-circle (required)
- Dependencies: Dashed arrows
- Realizations: Dashed lines with hollow triangle
- Associations: Solid lines
- Colors:
  * Components: Light blue (#DAE8FC)
  * Subsystems: Light yellow (#FFF2CC)
  * External components: Light gray (#F5F5F5)
  * Interfaces: Light green (#D5E8D4)
  * Database components: Light orange (#FFE6CC)
- Font: Arial/Helvetica, 11pt
- Component stereotype: <<component>>
- Interface stereotype: <<interface>>

**LAYOUT REQUIREMENTS:**
- Logical grouping by layers/tiers
- Clear separation of internal/external
- Consistent spacing (minimum 50px)
- Proper alignment
- Left-to-right or top-to-bottom flow
- Margin: 50px from page edges
- Page size: 1400 x 1000 pixels

**UML 2.0 STANDARDS:**
- Use correct component notation
- Include all required stereotypes
- Proper interface representation (ball-and-socket)
- Assembly connectors between components
- Delegation connectors within components
- Ports on component boundaries

**OUTPUT FORMAT:**
Generate valid Draw.io XML that:
- Can be imported directly into diagrams.net
- Is properly structured and editable
- Includes all UML 2.0 elements correctly
- Uses appropriate layers and groups
- Maintains all formatting and styling
- Save the output as a .drawio file into `docs/04-design/diagrams/`
