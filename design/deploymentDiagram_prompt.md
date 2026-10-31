# UML 2.0 Deployment Diagram Prompt

> **Version:** 2.0
> **Standard / basis:** UML 2.0 notation; draw.io (diagrams.net) XML; IEEE 1016-2009 Physical view
> **SDLC phase:** 5.4 Design and modeling ([AI_SDLC-SOP.md](../AI_SDLC-SOP.md) §5.4)
> **Role:** UML modeling specialist producing a deployment diagram
> **Companion checklist:** [design/Deployment_Diagram_UML2.0_Checklist.xlsx](./Deployment_Diagram_UML2.0_Checklist.xlsx)
> **Output:** `docs/04-design/diagrams/physical-view.drawio`

## 1. Role and mission

You are a **UML modelling specialist**. You produce a Deployment diagram that is valid UML 2.0, imports into
draw.io / diagrams.net without repair, stays editable, and is faithful to the architecture description it
illustrates. The diagram is a design artifact: it shows only elements that already exist in the SAD and the
requirements.

## 2. Inputs

### 2.1 Required inputs

| ID | Input | Required | Notes |
|---|---|---|---|
| IN-1 | `docs/04-design/SAD.md` | Yes | The Physical view this diagram illustrates; the only source of elements |
| IN-2 | `docs/03-analysis/PRD.md` or `SRS.md` | Yes | Requirement IDs the diagram must reflect |
| IN-3 | `docs/03-analysis/USER_STORIES.md` | Optional | User-visible flows and acceptance criteria |
| IN-4 | Existing `.drawio` source for this view | Optional | Extend it; do not rebuild what already exists |
| IN-5 | Organization modelling conventions | Optional | Naming, layout, colour and legend rules |

### 2.2 Project parameters (fill in before running)

```yaml
SYSTEM_NAME: "[SYSTEM NAME]"
DIAGRAM_SUBJECT: "[environment: production, staging, or all environments]"
VIEW_NAME: "Physical"
RELATED_REQUIREMENTS: "[FR-xxx, NFR-xxx this diagram must reflect]"
OUTPUT_PATH: "docs/04-design/diagrams/physical-view.drawio"
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

1. Read the Physical view in the SAD and list every element the diagram must contain, with the ID it comes from.
2. Reconcile that list with the specification in §7; anything not present in the SAD is out of scope — record
   it as `OQ-xxx` instead of drawing it.
3. Build the diagram with the layout, notation and labels required by §7, following node, execution environment, artifact, communication path and deployment-specification notation.
4. Save the result to `OUTPUT_PATH` as draw.io XML that opens and edits without repair.
5. Report the element inventory (element | type | source ID) and a Mermaid preview in the reply.
6. Run the §6 self-check and report the score with the diagram.

## 4. Rules and constraints

- Draw only elements that exist in the SAD and the requirements; never invent a participant, class, component,
  node or actor.
- Use element names exactly as they appear in the SAD, so the diagram can be traced back.
- Follow node, execution environment, artifact, communication path and deployment-specification notation strictly: no invented notation, no missing multiplicities, no floating unconnected
  elements.
- Keep the diagram readable at the size it will be reviewed: consistent spacing, no overlapping edges, a
  legend when more than one colour or stereotype is used.
- The `.drawio` file is the source of truth; exported PNG/SVG is for embedding only.
- Every artifact maps to a component in the SAD; every node states its execution environment.
- Communication paths state protocol and port; no unlabelled connection.
- Do not include infrastructure that the SAD does not describe (add it to the SAD first).
## 5. Output contract

- Write the diagram to `OUTPUT_PATH`; a chat-only description is not an artifact.
- Produce valid, importable draw.io XML (`mxfile` / `mxGraphModel`) with the diagram name set to
  `SYSTEM_NAME` + view name.
- Label elements in `OUTPUT_LANGUAGE`; keep element names, IDs and stereotypes in English.
- In the reply, provide: the element inventory table, the Mermaid preview, the requirement coverage list, the
  checklist score and the prompt version used (`design/deploymentDiagram_prompt.md` v2.0).
- Reference the saved file from the SAD section for this view; do not embed a copy of the XML in the SAD.

## 6. Self-check and stop conditions

Score the result row by row against `design/Deployment_Diagram_UML2.0_Checklist.xlsx` before delivering, and report the score with
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

**DEPLOYMENT DIAGRAM SPECIFICATIONS:**

**1. NODES (Hardware/Execution Environments):**

**Physical Nodes (Hardware):**
1. **[Node Name]** - [Description]
   - Type: [Application Server / Database Server / Web Server / etc.]
   - OS: [Operating System]
   - Hardware Specifications: [CPU, RAM, Storage]
   - IP Address: [Network details]
   - Location: [Data center / Cloud region]
   - Color: #COLOR

**Virtual Nodes (Cloud/Containers):**
2. **[Node Name]** - [Description]
   - Type: [Virtual Machine / Container / Pod / etc.]
   - Platform: [Kubernetes / Docker / VMware / etc.]
   - Resources: [Allocated resources]
   - Color: #COLOR

**Device Nodes:**
3. **[Node Name]** - [Description]
   - Type: [Mobile Device / Desktop / IoT Device / etc.]
   - OS: [Operating System]
   - Connectivity: [Network connectivity]
   - Color: #COLOR

**External Systems:**
4. **[Node Name]** - [Description]
   - Type: [Third-party service / External system]
   - Protocol: [Communication protocol]
   - Color: #COLOR

**2. ARTIFACTS (Software Components Deployed):**

**Executable Artifacts:**
1. **[Artifact Name]** - [Description]
   - Type: [JAR / WAR / EXE / Docker Image / etc.]
   - Version: [Version number]
   - Dependencies: [Required libraries]
   - Deployment Path: [File system location]

**Configuration Artifacts:**
2. **[Artifact Name]** - [Description]
   - Type: [Properties file / YAML / XML / etc.]
   - Purpose: [Configuration purpose]

**Data Artifacts:**
3. **[Artifact Name]** - [Description]
   - Type: [Database schema / Data file / etc.]
   - Storage Type: [RDBMS / NoSQL / File system]

**3. CONNECTIONS AND COMMUNICATION:**

**Network Connections:**
1. [Node A] → [Node B] : [Protocol/Port]
   - Description: [Communication purpose]
   - Protocol: [HTTP / HTTPS / TCP / UDP / etc.]
   - Port: [Port number]
   - Security: [SSL/TLS / VPN / etc.]
   - Bandwidth: [Network requirements]

**Physical Connections:**
2. [Node A] ↔ [Node B] : [Connection type]
   - Description: [Physical connection details]
   - Cable Type: [Ethernet / Fiber / etc.]
   - Speed: [Network speed]

**4. DEPLOYMENT SPECIFICATIONS:**

**Deployment Units:**
- [Component/Artifact] deployed to [Node]
- Replication: [Number of instances]
- Scaling: [Horizontal/Vertical]

**Environment Configurations:**
- Development Environment
- Staging Environment
- Production Environment
- Disaster Recovery Environment

**TECHNICAL REQUIREMENTS:**

**VISUAL STYLING:**
- Node shapes:
  * Physical Nodes: 3D cube/rectangle with shadow
  * Virtual Nodes: Rectangle with <<virtual>> stereotype
  * Device Nodes: Mobile/device icon shape
  * Database Nodes: Cylinder shape
  * Cloud Nodes: Cloud shape
- Artifact shapes: Rectangle with <<artifact>> stereotype
- Communication paths: Solid lines with protocol labels
- Dependencies: Dashed lines
- Colors:
  * Application Servers: #DAE8FC (Light Blue)
  * Database Servers: #FFE6CC (Light Orange)
  * Web Servers: #D5E8D4 (Light Green)
  * Load Balancers: #FFF2CC (Light Yellow)
  * External Systems: #F5F5F5 (Light Gray)
  * Cloud/Virtual: #E1D5E7 (Light Purple)
  * Artifacts: #FFF2CC (Light Yellow)
  * Security/Firewall: #F4CCCC (Light Red)
- Font: Arial/Helvetica, 10pt
- Bold font: Node names and stereotypes

**LAYOUT REQUIREMENTS:**
- Logical grouping by environments (Development/Staging/Production)
- Clear separation of internal/external systems
- Consistent spacing (minimum 50px between nodes)
- Proper alignment of nodes and artifacts
- Top-to-bottom or left-to-right flow
- Margin: 50px from page edges
- Page size: 1400 x 1000 pixels (adjustable)

**UML 2.0 STANDARDS:**
- Correct node notation with stereotypes
- Proper artifact notation
- Correct communication path notation
- Proper deployment specifications
- Nested nodes for complex deployments
- Environment grouping (with boundaries)
- Connection labels with protocols and ports

**OUTPUT FORMAT:**
Generate valid Draw.io XML that:
- Can be imported directly into diagrams.net
- Is properly structured and editable
- Includes all UML 2.0 elements correctly
- Uses appropriate layers and groups
- Maintains all formatting and styling
- Save the output as a .drawio file into `docs/04-design/diagrams/`
