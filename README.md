# AI-SDLC-Docs

A lightweight repository of AI-assisted software development lifecycle (SDLC) prompts and standards-aligned checklist artifacts for architecture, design, database modeling, UX, and test planning.

## Purpose

This repo provides reusable prompt templates and supporting checklist documents that help generate structured engineering outputs such as:

- API design documents
- Blueprint / architecture design artifacts
- UML diagrams
- Database design specifications
- UI/UX design prompts
- Test plans and QA documentation

The materials are intended to support teams working with AI tools to create standards-based software engineering artifacts faster and more consistently.

## Repository Contents

Documents are organized by SDLC phase, in folders matching the phase numbers in [AI_SDLC-SOP.md](./AI_SDLC-SOP.md):

| Folder | SDLC phase | Contents |
|---|---|---|
| [`requirements/`](./requirements) | Requirements and discovery (5.2) | Business requirements document template |
| [`analysis/`](./analysis) | Analysis (5.3) | PRD prompts and the requirements checklist |
| [`design/`](./design) | Design, modeling (5.4) | SAD, blueprint, UML diagram, API, database and UI/UX prompts with their checklists |
| [`verification/`](./verification) | Verification and testing (5.7) | Test plan prompt and checklist |

### Prompt Templates

Prompt files for common SDLC activities, kept in the folder of the phase that uses them:

- `requirements/` — the BRD template
- `analysis/PRD_prompt.md`, `analysis/PRD_Prompt_IEEE_standard.md`, `analysis/PRD_Prompt_with_template.md`
- `design/SAD_prompt.md`, `design/SAD_Prompt_IEEE_standard.md`, `design/SAD_Prompt_with_template_.md`
- `design/bluePrint_design_prompt.md`
- `design/classDiagram_prompt.md`, `design/componentDiagram_prompt.md`, `design/deploymentDiagram_prompt.md`
- `design/sequenceDiagram_prompt.md`, `design/activityDiagram_prompt.md`, `design/useCase_prompt.md`
- `design/apiDesign_prompt.md`, `design/UI-UX-Design_prompt.md`
- `design/databaseDesign_SQL_prompt.md`, `design/databaseDesign_NoSQL_prompt.md`, `design/databaseDesign_GraphrDB_prompt.md`, `design/databaseDesign_VectorDB_prompt.md`
- `verification/testPlan_prompt.md`

### Checklist Artifacts

Supporting checklist spreadsheets sit next to the prompts they validate:

- `analysis/PRD_IEEE_29148_Checklist.xlsx`
- `design/BluePrint_Design_IEEE_1016_2009_Checklist.xlsx`, `design/SAD_IEEE_1016_Checklist.xlsx`
- `design/Class_Diagram_UML2.0_Checklist.xlsx`, `design/Component_Diagram_UML2.0_Checklist.xlsx`, `design/Deployment_Diagram_UML2.0_Checklist.xlsx`
- `design/Sequence_Diagram_UML2.0_Checklist.xlsx`, `design/Activity_Diagram_UML2.0_Checklist.xlsx`, `design/UseCase_Document_UML2.0_Checklist.xlsx`
- `design/API_Design_IEEE-1016-2009Checklist.xlsx`, `design/UI_UX_Design_IEEE-1016-2009_Checklist.xlsx`
- `design/Database_Design_Checklist.xlsx`, `design/Polyglot_DB_Design_Checklist.xlsx`, `design/Checklist_Database Design Review.xlsx`
- `verification/Test_Plan_IEEE_829_Checklist.xlsx`

### Standards:

- IEEE 1016-2009, IEEE 829, IEEE 29148
- UML 2.0

## Typical Usage

1. Choose the prompt for the phase you are working in, from that phase's folder.
2. Fill in the placeholder system or project details in the prompt.
3. Use the prompt with your preferred AI assistant or generation workflow.
4. Save the generated output into the target project's `docs/<phase>` folder as defined in [AI_SDLC-SOP.md](./AI_SDLC-SOP.md).
5. Use the spreadsheet checklists to validate completeness and standards alignment.

## Suggested Workflow

- Requirements and architecture inputs -> blueprint / API / database prompts
- Design and user experience inputs -> UI/UX prompt
- Verification and quality inputs -> test plan prompt

## Notes

This repository is organized as a collection of reusable prompts and review checklists. It is best used as a starting point for generating structured SDLC documentation rather than as a completed product application.

## License

This repository does not currently declare a specific license. If you plan to redistribute or reuse it publicly, add an appropriate license file and terms.
