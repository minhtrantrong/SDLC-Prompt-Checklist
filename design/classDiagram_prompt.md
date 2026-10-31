# UML 2.0 Class Diagram Prompt

> **Version:** 2.0
> **Standard / basis:** UML 2.0 notation; draw.io (diagrams.net) XML; IEEE 1016-2009 Logical view
> **SDLC phase:** 5.4 Design and modeling ([AI_SDLC-SOP.md](../AI_SDLC-SOP.md) §5.4)
> **Role:** UML modeling specialist producing a class diagram
> **Companion checklist:** [design/Class_Diagram_UML2.0_Checklist.xlsx](./Class_Diagram_UML2.0_Checklist.xlsx)
> **Output:** `docs/04-design/diagrams/logical-view.drawio`

## 1. Role and mission

You are a **UML modelling specialist**. You produce a Class diagram that is valid UML 2.0, imports into
draw.io / diagrams.net without repair, stays editable, and is faithful to the architecture description it
illustrates. The diagram is a design artifact: it shows only elements that already exist in the SAD and the
requirements.

## 2. Inputs

### 2.1 Required inputs

| ID | Input | Required | Notes |
|---|---|---|---|
| IN-1 | `docs/04-design/SAD.md` | Yes | The Logical view this diagram illustrates; the only source of elements |
| IN-2 | `docs/03-analysis/PRD.md` or `SRS.md` | Yes | Requirement IDs the diagram must reflect |
| IN-3 | `docs/03-analysis/USER_STORIES.md` | Optional | User-visible flows and acceptance criteria |
| IN-4 | Existing `.drawio` source for this view | Optional | Extend it; do not rebuild what already exists |
| IN-5 | Organization modelling conventions | Optional | Naming, layout, colour and legend rules |

### 2.2 Project parameters (fill in before running)

```yaml
SYSTEM_NAME: "[SYSTEM NAME]"
DIAGRAM_SUBJECT: "[system domain or subsystem]"
VIEW_NAME: "Logical"
RELATED_REQUIREMENTS: "[FR-xxx, NFR-xxx this diagram must reflect]"
OUTPUT_PATH: "docs/04-design/diagrams/logical-view.drawio"
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

1. Read the Logical view in the SAD and list every element the diagram must contain, with the ID it comes from.
2. Reconcile that list with the specification in §7; anything not present in the SAD is out of scope — record
   it as `OQ-xxx` instead of drawing it.
3. Build the diagram with the layout, notation and labels required by §7, following class, attribute, operation, association, multiplicity and generalization notation.
4. Save the result to `OUTPUT_PATH` as draw.io XML that opens and edits without repair.
5. Report the element inventory (element | type | source ID) and a Mermaid preview in the reply.
6. Run the §6 self-check and report the score with the diagram.

## 4. Rules and constraints

- Draw only elements that exist in the SAD and the requirements; never invent a participant, class, component,
  node or actor.
- Use element names exactly as they appear in the SAD, so the diagram can be traced back.
- Follow class, attribute, operation, association, multiplicity and generalization notation strictly: no invented notation, no missing multiplicities, no floating unconnected
  elements.
- Keep the diagram readable at the size it will be reviewed: consistent spacing, no overlapping edges, a
  legend when more than one colour or stereotype is used.
- The `.drawio` file is the source of truth; exported PNG/SVG is for embedding only.
- Include every attribute and operation that the SAD names, with visibility, type and multiplicity.
- No orphan class: every class participates in at least one relationship or is a documented root entity.
## 5. Output contract

- Write the diagram to `OUTPUT_PATH`; a chat-only description is not an artifact.
- Produce valid, importable draw.io XML (`mxfile` / `mxGraphModel`) with the diagram name set to
  `SYSTEM_NAME` + view name.
- Label elements in `OUTPUT_LANGUAGE`; keep element names, IDs and stereotypes in English.
- In the reply, provide: the element inventory table, the Mermaid preview, the requirement coverage list, the
  checklist score and the prompt version used (`design/classDiagram_prompt.md` v2.0).
- Reference the saved file from the SAD section for this view; do not embed a copy of the XML in the SAD.

## 6. Self-check and stop conditions

Score the result row by row against `design/Class_Diagram_UML2.0_Checklist.xlsx` before delivering, and report the score with
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

**CLASS DIAGRAM SPECIFICATIONS:**

**1. CLASSES (List all domain classes):**

**Core Domain Classes:**
1. **[ClassName]** - [Brief description/responsibility]
   - Attributes:
     * -attributeName: dataType = defaultValue
     * -attributeName: dataType
     * +attributeName: dataType
   - Methods:
     * +methodName(parameters): returnType
     * +methodName(parameters): void
     * -privateMethod(parameters): returnType
   - Stereotypes: <<entity>>, <<value object>>, etc.
   - Color: #COLOR

2. **[ClassName]** - [Brief description/responsibility]
   - Attributes: [List with visibility]
   - Methods: [List with visibility]
   - Color: #COLOR

3. **[ClassName]** - [Brief description/responsibility]
   - Attributes: [List with visibility]
   - Methods: [List with visibility]
   - Color: #COLOR

**Abstract Classes:**
4. **<<abstract>> [ClassName]** - [Purpose]
   - Attributes: [List with visibility]
   - Abstract Methods: +abstractMethod(): returnType

**Interfaces:**
5. **<<interface>> [InterfaceName]** - [Purpose]
   - Methods: +methodName(): returnType (all abstract)

**Enumerations:**
6. **<<enumeration>> [EnumName]** - [Purpose]
   - Values: VALUE1, VALUE2, VALUE3

**2. RELATIONSHIPS (Specify all connections):**

**Association (Simple Relationship):**
- [ClassA] ↔ [ClassB] : [Multiplicity A] → [Multiplicity B]
  - Description: [Purpose of relationship]
  - Navigation: Bi-directional/Uni-directional
  - Role names: [roleA] and [roleB]

**Aggregation (Whole-Part Relationship):**
- [Container] ◇→ [Contained] : [Multiplicity]
  - Description: [Part-of relationship]
  - Shared ownership

**Composition (Strong Whole-Part):**
- [Container] ◆→ [Contained] : [Multiplicity]
  - Description: [Strong ownership, lifecycle dependency]
  - Exclusive ownership

**Inheritance/Generalization:**
- [Parent Class] ↑ [Child Class]
  - Description: [Is-a relationship]
  - Abstract: Yes/No

**Realization (Interface Implementation):**
- [Interface] - - - ↑ [Implementing Class]
  - Description: [Implements interface methods]

**Dependency (Usage):**
- [ClassA] - - - → [ClassB]
  - Description: [Temporary usage relationship]

**3. MULTIPLICITY (Specify cardinality):**

- 1 : Exactly one
- 0..1 : Zero or one
- * : Zero or more
- 1..* : One or more
- 0..* : Zero or more (same as *)
- m..n : Between m and n
- 2,4,6 : Specific values

**4. ATTRIBUTE DETAILS:**

**Visibility Symbols:**
- + : Public (accessible to all)
- - : Private (accessible only within class)
- # : Protected (accessible to subclasses)
- ~ : Package (accessible within package)

**Data Types:**
- Primitive: int, double, boolean, char, String
- Date/Time: Date, LocalDateTime, Time
- Collections: List<T>, Set<T>, Map<K,V>
- Custom: [Your domain types]

**5. PACKAGES (Organization):**
- Package 1: [Package Name]
  - Contains: [List of classes]
- Package 2: [Package Name]
  - Contains: [List of classes]

**TECHNICAL REQUIREMENTS:**

**VISUAL STYLING:**
- Class shapes: Rectangles divided into 3 sections (name, attributes, methods)
- Abstract classes: Italic class name
- Interfaces: <<interface>> above name, italic
- Enumerations: <<enumeration>> above name
- Inheritance: Hollow triangle arrow (pointing to parent)
- Realization: Dashed line with hollow triangle (pointing to interface)
- Association: Solid line with optional arrow (for navigation)
- Aggregation: Hollow diamond at whole end
- Composition: Filled diamond at whole end
- Dependency: Dashed line with arrow
- Colors:
  * Entity classes: Light blue (#DAE8FC)
  * Abstract classes: Light gray (#F5F5F5)
  * Interfaces: Light green (#D5E8D4)
  * Value objects: Light yellow (#FFF2CC)
  * Enumerations: Light purple (#E1D5E7)
  * Controller classes: Light orange (#FFE6CC)
- Font: Arial/Helvetica, 10pt (attributes/methods), 12pt (class names)
- Bold font: Class names and stereotypes

**LAYOUT REQUIREMENTS:**
- Logical grouping by packages/domains
- Clear inheritance hierarchies (top-to-bottom)
- Related classes grouped together
- Consistent spacing (minimum 50px between classes)
- Proper alignment
- Margin: 50px from page edges
- Page size: 1400 x 1000 pixels (adjustable)

**UML 2.0 STANDARDS:**
- Correct class notation (3 compartments)
- Proper visibility symbols
- Correct relationship notation
- Proper multiplicity notation
- Role names on associations
- Navigation arrows for direction
- Package notation (folder icon)
- Constraint notes where needed

**OUTPUT FORMAT:**
Generate valid Draw.io XML that:
- Can be imported directly into diagrams.net
- Is properly structured and editable
- Includes all UML 2.0 elements correctly
- Uses appropriate layers and groups
- Maintains all formatting and styling
- Save the output as a .drawio file into `docs/04-design/diagrams/`
