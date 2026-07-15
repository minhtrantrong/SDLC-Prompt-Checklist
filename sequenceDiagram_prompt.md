Create a professional UML 2.0 Sequence Diagram for [SYSTEM/PROCESS NAME] in Draw.io XML format. The diagram should follow strict UML 2.0 standards and illustrate the interaction flow between objects over time.

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
- Save the output as a .drawio file into [your document folder such as ./docs]