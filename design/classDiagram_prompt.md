Create a professional UML 2.0 Class Diagram for [SYSTEM NAME] in Draw.io XML format. The diagram should follow strict UML 2.0 standards and illustrate the static structure of the system including classes, attributes, methods, and relationships.

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
- Save the output as a .drawio file into [your document folder such as ./docs]