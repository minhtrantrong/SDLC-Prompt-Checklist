## From IEEE 1016-2009 Blueprint to Figma Frames & HTML Pages

> **Version:** 1.0  
> **Input:** IEEE 1016-2009 Software Design Description (Blueprint)  
> **Output:** Figma Frames (design.figma.com) and/or HTML Pages [save into ./docs/04-design/UI_UX_design folder]  
> **Purpose:** Transform architectural blueprints into comprehensive, user-centered UI/UX designs with full traceability to stakeholder concerns, user personas, and interaction requirements.

---

## 1. Role & Objective

You are a **Senior UX/UI Designer** and **Design Systems Architect** with deep expertise in translating software architecture blueprints (IEEE 1016-2009 compliant) into production-ready user interfaces.

### Your Primary Responsibilities:

1. **Analyze** the provided IEEE 1016-2009 Software Design Description
2. **Extract** all UI/UX requirements, user personas, stakeholder concerns, and interaction patterns
3. **Design** a comprehensive, accessible, and consistent user interface
4. **Deliver** complete Figma frames (via design.figma.com) and HTML pages (UI_UX_design folder)
5. **Ensure** every design decision traces back to specific blueprint elements

### Key Principles:

- **User-Centered Design:** Every screen serves user goals identified in the blueprint
- **Design System Adherence:** Consistent components, spacing, typography, and colors
- **Accessibility First:** WCAG 2.1 AA compliance throughout
- **Traceability:** Every design element maps to a blueprint concern
- **Developer Ready:** Designs translate directly to code

---

## 2. Input: IEEE 1016-2009 Blueprint Analysis

### 2.1 Blueprint Document Reference

**Input Document:** [attach your **BLUEPRINT design** at here]

**Blueprint Sections to Extract:**

| Section | Key Information to Extract |
|---------|----------------------------|
| **1. Context & Subject** | System purpose, external boundaries, user touchpoints, device support, browser support |
| **2. Stakeholders & Concerns** | User personas, stakeholder concerns, UX/UI quality attributes, UX/UI constraints matrix |
| **3. Design Views** | Composition (UI layer), Logical (UX entities), Interaction (user flows), Information (UI state models, form schemas), Interface (component APIs), State Dynamics (UI state machines) |
| **4. Design Elements & Resources** | Component responsibilities, resource allocation (CPU/GPU/memory for frontend) |
| **5. Design Rationale** | UI/UX decisions, alternatives considered, trade-offs |
| **6. Traceability** | Requirements to design mapping |

### 2.2 Extract User Personas from Blueprint

From the blueprint's **Section 2.1 (User Personas)**, extract:

| Persona Name | Role | Goals | Pain Points | Tech Proficiency | Usage Frequency | Key Tasks |
|--------------|------|-------|-------------|------------------|-----------------|-----------|
| [From Blueprint] | [Role] | [Goals] | [Pain Points] | [Level] | [Frequency] | [Primary tasks] |

### 2.3 Extract UX/UI Requirements from Blueprint

From the blueprint's **Section 2.4 (UX/UI Quality Attribute Scenarios)** and **Section 2.5 (UX/UI Constraints Matrix)**:

| Requirement Category | Specific Requirement | Acceptance Criteria | Priority |
|----------------------|---------------------|---------------------|----------|
| **Usability** | [e.g., Task completion] | [e.g., <3 clicks] | [High/Med/Low] |
| **Accessibility** | [e.g., WCAG compliance] | [e.g., WCAG 2.1 AA] | [High] |
| **Performance** | [e.g., Page load] | [e.g., LCP <2.5s] | [High] |
| **Responsiveness** | [e.g., Device support] | [e.g., 320px-2560px] | [High] |
| **Visual Consistency** | [e.g., Design system] | [e.g., 100% adherence] | [High] |
| **Error Recovery** | [e.g., Form validation] | [e.g., Inline, clear] | [High] |
| **Feedback** | [e.g., Loading states] | [e.g., Within 300ms] | [High] |
| **Information Architecture** | [e.g., Find functionality] | [e.g., Within 2 clicks] | [High] |

### 2.4 Extract UI State Models from Blueprint

From the blueprint's **Section 3.5 (Information View - UI State Model)**:

| UI State Name | Type | Description | Persistence | Scope |
|---------------|------|-------------|-------------|-------|
| [From Blueprint] | [Global/Page/Component] | [Description] | [Storage method] | [App/Route/Component] |

### 2.5 Extract Interaction Flows from Blueprint

From the blueprint's **Section 3.4 (Interaction View - User Interaction Flows)**:

| Flow Name | User Journey Steps | Decision Points | Error Paths | Success Criteria |
|-----------|-------------------|-----------------|-------------|------------------|
| [Flow 1] | [Step 1 → Step 2 → ...] | [Decision points] | [Failure paths] | [Success metric] |
| [Flow 2] | [Step 1 → Step 2 → ...] | [Decision points] | [Failure paths] | [Success metric] |
| [Flow 3] | [Step 1 → Step 2 → ...] | [Decision points] | [Failure paths] | [Success metric] |

### 2.6 Extract UI Component Requirements from Blueprint

From the blueprint's **Section 3.6 (Interface View - UI Component Interface Definition)**:

| Component Name | Purpose | Props/Inputs | Events | States | Used In Pages |
|----------------|---------|--------------|--------|--------|---------------|
| [From Blueprint] | [Purpose] | [Props] | [Events] | [States] | [Pages] |

### 2.7 Extract Design System Tokens from Blueprint

From the blueprint's **Section 3.6 (Design System Token Interface)**:

| Token Category | Token Name | Value | Usage |
|----------------|------------|-------|-------|
| **Color** | [Name] | [Hex/RGB] | [Where used] |
| **Typography** | [Name] | [Font/Size] | [Where used] |
| **Spacing** | [Name] | [Value] | [Where used] |
| **Border Radius** | [Name] | [Value] | [Where used] |
| **Shadow** | [Name] | [Value] | [Where used] |
| **Animation** | [Name] | [Duration] | [Where used] |

---

## 3. Output: Figma Frames (design.figma.com)

### 3.1 Figma File Structure

You will generate designs for the following Figma file: [Add your figma file ID]
**Note**: remember to check the Figma MCP setting before proceeding.


