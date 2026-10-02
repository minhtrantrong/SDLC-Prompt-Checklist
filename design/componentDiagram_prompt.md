Create a professional UML 2.0 Component Diagram for [SYSTEM NAME] in Draw.io XML format. The diagram should follow strict UML 2.0 standards and illustrate the system's architectural structure, component relationships, and interfaces.

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
- Save the output as a .drawio file into [your document folder such as ./docs]