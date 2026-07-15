Create a professional UML 2.0 Deployment Diagram for [SYSTEM NAME] in Draw.io XML format. The diagram should follow strict UML 2.0 standards and illustrate the physical deployment of software components on hardware infrastructure.

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
- Save the output as a .drawio file into [your document folder such as ./docs]