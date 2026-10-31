# Step-by-Step Guidance — Running Any Project Through the Agentic SDLC

A project-agnostic playbook for the prompts and checklists in this repository. It walks the lifecycle
phase by phase and, inside each phase, step by step: which kit document to use, what it produces, what
must be true before the next step starts.

This guide contains no product, customer or project assumptions. Everything project-specific is a
placeholder you fill in.

**Companion documents**

| Document | Use it for |
|---|---|
| [README.md](./README.md) | Inventory of prompts and checklists, and the phase each belongs to |
| [AI_SDLC-SOP.md](./AI_SDLC-SOP.md) | Roles (§4), mandatory operating principles (§3), phase goals and exit criteria (§5), agent controls (§6), exceptions (§7), work-item/PR contract (§8), completion checklist (§9) |
| [agentic-sdlc-process.md](./agentic-sdlc-process.md) | Phase-by-phase steps, artifacts, document flow, identifier conventions (§2–§10) |
| `requirements/` | BRD presentation template |
| `analysis/` | BRD elicitation/authoring prompts, PRD prompts, IEEE 29148 checklists |
| `design/` | SAD, blueprint, UML diagram, API, database and UI/UX prompts with their checklists |
| `development/` | Software Development Plan and WBS/task-breakdown prompts, ISO/IEC/IEEE 24748-5 checklist |
| `verification/` | Test plan prompt, IEEE 829 test-plan checklist, IEEE 1028 code-review checklist |

---

## Contents

**Part A — Before you start**
A1. Everything here is a template · A2. Adapt prompts and checklists first · A3. How the kit fits together ·
A4. The loop every step follows · A5. Artifact layout and naming · A6. Gates, evidence and approvals ·
A7. How to run a prompt · A8. How to score a checklist · A9. Identifier scheme · A10. Roles ·
A11. Template coverage by phase

**Part B — Phase-by-phase steps**
Phase 1 Intake · Phase 2 Requirements · Phase 3 Analysis · Phase 4 Design · Phase 5 Planning ·
Phase 6 Implementation · Phase 7 Verification · Phase 8 Review · Phase 9 Release ·
Phase 10 Operations · Phase 11 Decommissioning

**Part C — Cross-cutting steps**
C1 Change control · C2 Traceability upkeep · C3 Prompt/checklist versioning · C4 Evidence and data handling · C5 Agent controls

**Appendices**
A. Kit document map · B. Gate summary · C. Standards referenced · D. First-use customization checklist ·
E. Common failure modes

**Conventions used in this guide**

- `<...>` is a placeholder you replace (project name, path, role, command).
- `docs/0X-<phase>/` are folders in the project that *consumes* the kit, per [AI_SDLC-SOP.md](./AI_SDLC-SOP.md) §5.
- Paths without `docs/` are files in this kit repository.
- "Gate" means the conditions that must hold before the phase is called complete (SOP §5, §5.12).
- "Owner" always means a named human, never an agent.
- `@<path-to-folder>/<phase-folder>/<template>.md` is the literal invocation of a prompt template: the file
  already holds the input, task and output contract, so nothing else is typed into the chat (§A7).

---

# Part A — Before you start

## A1. Everything in this repository is a template

> **Important note 1 — these documents are templates, not finished standards.**
> Every prompt, document template and checklist in this kit is a starting point that encodes one generic
> reading of a standard (IEEE 29148, IEEE 1016-2009, IEEE 829, IEEE 1028, ISO/IEC/IEEE 24748-5,
> ISO 21511, UML 2.0, …). None of them knows your organization's document template, terminology,
> approval matrix, risk tiers, regulatory obligations, technology stack, tooling or working language.
> They must be reviewed and updated carefully before they are used on real work, and the result must be
> validated against your own standard — a kit checklist that was filled in is **not** by itself proof of
> compliance.

Consequences that apply to every step in Part B:

1. **Adapt before use, every time.** Read the prompt end to end, replace every placeholder, delete what
   does not apply, add what your organization requires. A prompt sent unchanged will produce a document
   that looks standard-compliant and is still wrong for your context.
2. **Adapt the checklist with the prompt.** The checklist is the acceptance test for the prompt output.
   If the prompt was adapted and the checklist was not (or the reverse), the gate measures the wrong thing.
3. **Treat output as a draft.** Agent output is a proposal, not evidence (SOP §3, principle 1). A human owner edits,
   validates and signs it.
4. **Expect to iterate.** First-pass output from an adapted prompt is rarely complete; the audit step
   exists to close the gap, not to prove the first pass was perfect.
5. **Do not redistribute project-filled versions.** Once a template is filled with real project data or
   organizational rules, it is a project document, not a kit template.
6. **Keep the template contract intact.** Every prompt in this kit carries the same six sections — role,
   inputs, task, rules, output, self-check (§A7). Adapt the content of those sections; do not delete a section,
   or the run depends on chat instructions again.

## A2. Adapt prompts and checklists to your organization and project first

> **Important note 2 — update all prompt and checklist templates according to your organization or
> project standard and conventions before applying them.** The adaptation below is not optional
> housekeeping; it is the step that decides whether the artifacts are usable.

| Area | What to adapt | Why it matters |
|---|---|---|
| Document control | Document ID, owner, version, status, approver, review date | Kit headers are generic; your QMS/records process needs controlled documents |
| House template | Section order and numbering, mandatory appendices, front matter | Presentation must match the approved template (e.g. [requirements/BRD-Template.md](./requirements/BRD-Template.md)) |
| Terminology | Domain glossary, role names, product vocabulary | Otherwise the agent invents synonyms and breaks traceability |
| Identifier scheme | ID prefixes and numbering for BR/FR/NFR/US/AC/TC/CMP/ADR/API/TASK/DEF/RISK | IDs must join across documents and tools (see A9) |
| Roles and approvals | Who owns, reviews and approves each artifact and gate; risk tiers | SOP §4 defines generic roles; map them to real people and groups |
| Regulatory context | Applicable standards, data classification, retention, accessibility, licensing | Changes what must be documented, and what is forbidden |
| Technology constraints | Approved stack, hosting, security controls, vendor limits | Generic prompts must not pick your technology |
| Language and style | Output language, tense, voice, units, date format, heading style | Mixed-language or mixed-style artifacts fail review |
| Tooling | Build/test/lint/scan commands, CI provider, diagram and design tools | Prompts that guess commands produce unverifiable claims |
| Checklist rows | Add, remove, merge or re-word rows; mark mandatory rows; set thresholds | Kit rows are one interpretation of a standard, not your interpretation |
| Checklist columns | Add `Evidence`, `Owner`, `Due`, `Gate` next to `Status`, `Notes / Action Items` | An audit must be actionable and provable |
| Status vocabulary | Define Pass / Partial / Fail / N/A and forbid `Pending` at a gate | Prevents gates from being passed by inaction |

**How to adapt safely**

1. Keep a pristine copy of the kit; put your adapted versions in a separate layer (an internal fork, or a
   project folder such as `docs/00-kit/`). Never edit the pristine copy in place if you plan to take kit
   updates later.
2. Record every change in an adaptation log, so a reviewer can see what diverged from the standard text:

   | Document | Change made | Reason / source | Owner | Date | Version |
   |---|---|---|---|---|---|
   | `<kit/path>` | `<what changed>` | `<org standard, clause, decision>` | `<name>` | `<YYYY-MM-DD>` | `<x.y>` |

3. Validate the adapted prompt against one already-approved artifact from a past project. If the output
   structure changes materially, the adaptation changed the contract — review it before rollout.
4. Re-run the audit tooling (if any) and re-check the checklist after the adaptation; stale
   cross-references between prompt sections and checklist rows are the most common defect.
5. Re-review adaptations on a fixed cadence and whenever the standard, the tooling or the org template
   changes.
6. Keep the six-section contract when you adapt a template (§A7); put organization rules into
   `## 4. Rules and constraints`, parameters into `## 2.2`, and output requirements into `## 5`. A template
   whose sections were merged or deleted cannot be invoked with a single reference any more.

## A3. How the kit fits together

Each phase has the same shape: an **input artifact** that is already baselined, a **generation prompt**
that drafts the next artifact, an **audit checklist** that scores it, and a **gate** that a human approves.

```text
request → intake → BRD → PRD/SRS + user stories → design (SAD, blueprint, diagrams, API, data, UI/UX)
        → plan (SDP, WBS, task cards) → code + tests → verification evidence → review
        → release → operate → decommission
```

At every arrow the artifact is committed, baselined and handed over with a record (SOP §5.12). Chat
history is never the handover medium, and a later phase reads files, not conversations.

## A4. The loop every step follows

| Step | What the human does | What the agent does | Stop condition |
|---|---|---|---|
| 1. Specify | Pick the artifact, list the exact input files, choose and adapt the prompt, define "done" as checklist + gate | — | Inputs exist, are baselined, and the prompt has no unfilled placeholder |
| 2. Generate | Confirms the output path and scope | Drafts the artifact into the target path | Draft exists at the agreed path, in the agreed language and structure |
| 3. Audit | Starts a clean session or auditor sub-agent and hands it the artifact + adapted checklist | Scores every checklist row; never edits the artifact | Every row has Status and Evidence |
| 4. Fix | Assigns Fail/Partial items by risk, fixes the artifact | Re-audits after fixes | 0 Fail; every Partial has an owner and a date |
| 5. Approve | Named human reviews, signs, baselines (commit + tag), issues the handoff record | — | Gate conditions in Appendix B are met |

**Three-round rule:** generate → audit → fix, at most three rounds. If a phase still fails after three
rounds, the problem is usually the requirement or the prompt, not the artifact. Stop and escalate.

## A5. Artifact layout and naming

Folder layout for the consuming project, from [AI_SDLC-SOP.md](./AI_SDLC-SOP.md) §5:

| Phase | Folder | Typical artifacts |
|---|---|---|
| 1 Intake | `docs/01-intake/` | `intent.md`, `glossary.md`, `stakeholders.md`, `sources.md` (or equivalent work-item fields) |
| 2 Requirements | `docs/02-requirements/` | `BRD.md`, `interviews/SRC-*.md`, `brd-audit.md` |
| 3 Analysis | `docs/03-analysis/` | `PRD.md` or `SRS.md`, `USER_STORIES.md`, `traceability.md`, `prd-audit.md` |
| 4 Design | `docs/04-design/` | `SAD.md`, `ADR-*.md`, `blueprint.md`, `diagrams/*.drawio`, `openapi.yaml`, `data/model.md`, `UI_UX_design/`, `design-audit.md` |
| 5 Planning | `docs/05-development/` | `Software_Development_Plan.md`, `WBS.md`, `tasks/<task-id>.md` |
| 6 Implementation | the repository itself | source code, tests, updated `traceability.md`; records live in the PR/work item |
| 7 Verification | `docs/07-verification/` | `TEST_PLAN.md`, `TEST_CASES.md`, `RTM.md`, `TEST_REPORT.md`, `evidence/<run-id>/` |
| 8 Review | the review system | PR + review record + approvals |
| 9 Release | `docs/09-release/` | release record, release notes, rollout and rollback plan |
| 10 Operations | `docs/10-operations/` | runbooks, dashboards/alerts inventory, incident records |
| 11 Decommissioning | `docs/11-decommissioning/` | decommissioning record, evidence of data disposition and access revocation |

Rules:

- One artifact, one home. Do not leave phase documents loose in `docs/` or in the repository root.
- Phase 6 has no document folder (its artifact is the code), and phase 8 has none (its record lives in the
  review system) — link them from the work item instead of duplicating them.
- Every diagram is stored as an editable `.drawio` file; PNG/SVG exports exist only to be embedded.
- Name evidence by run: `evidence/<run-id>/` with the run-id containing the commit and environment.

## A6. Gates, evidence and approvals

A phase is complete only when all five rules hold:

1. **Checklist:** 0 `Fail`, and every `Partial` has a named owner and a due date. `N/A` needs a reason.
2. **Traceability:** the artifact links upward to the IDs it implements and downward to what will verify it.
3. **Evidence:** claims point to an openable artifact — file §, ID, command output, log, screenshot, query
   result. "The agent said it passed" is not evidence (SOP §3, principle 5).
4. **Independent approval:** author ≠ approver; an agent is never the approver and cannot satisfy a
   required independent review (SOP §5.8).
5. **Handoff:** the outgoing owner records status, linked evidence, incoming owner and unresolved
   risks/actions; the incoming owner acknowledges (SOP §5.12).

A baseline is a commit plus a tag (for example `requirements-v1`, `design-v1` or `release-v1`) whose tag
message or attached record names the checklist result and the approver.

## A7. How to run a prompt template

Every prompt in this kit is self-contained: **input, task and output are inside the file, not in your chat
message.** Calling one is a single reference: the absolute or workspace-relative location of the kit, followed by
the template's own phase folder and file name.

```text
@<path-to-folder>/analysis/BRD_Prompt_IEEE_standard.md
```

`<path-to-folder>` is the folder that holds this kit (for example `~/work/SDLC-Prompt-Checklist`); everything
after it is the template path as written in this guide.

That is the whole invocation. What the template carries, and what you must do before sending it:

| Section in the template | Contains | Your job before running it |
|---|---|---|
| Header block | Version, standard, SOP phase, role, companion checklist, output path | Confirm the phase and the output path match this project |
| `1. Role and mission` | Who the agent is and what it must not do | Adjust the role only if your organization defines it differently |
| `2. Inputs` | `2.1` required inputs with IDs, `2.2` project parameters, `2.3` input handling rules | **Fill every parameter in `2.2`** and attach or path the files in `2.1` |
| `3. Task` | The numbered steps the agent must execute | Do not add task instructions in the chat; change the template if the task is wrong |
| `4. Rules and constraints` | Quality bar, forbidden actions, standards to apply | Add organization rules here, not as chat remarks |
| `5. Output contract` | Exact path, language, structure, document control, closing sections | Adjust the path only if the project layout differs from SOP §5 |
| `6. Self-check and stop conditions` | The checklist to score against, the gate items, and when to stop and ask | Point it at your adapted checklist |
| `7. Detailed specification` | The long-form structure, question bank, templates or notation rules | Adapt it to your standard; it is where most adaptation happens |

Rules that hold for every template:

1. **One reference, no restatement.** Send `@<path-to-folder>/<phase-folder>/<template>.md`;
   do not repeat the task in the chat. If the task is wrong, fix the template — otherwise the next
   run diverges from this one.
2. **No unfilled placeholder.** `<...>`, `[...]`, `[Insert ...]`, `[SYSTEM NAME]` and the `2.2` YAML block are
   inputs, not decoration. An unfilled placeholder silently becomes a fabrication.
3. **Attachment is explicit.** Reference real files by path; never say "my document".
4. **The output path is part of the prompt.** Without it the agent answers in chat, and a chat answer is not
   an artifact.
5. **The self-check is part of the prompt.** A run that does not report the checklist score is incomplete.
6. **Record the prompt version** — path plus version — in the artifact's document control, so the artifact can
   be reproduced.
7. **Adapt the template, not the conversation** (A2). A chat-level correction is invisible to the next run,
   the next project and the next reviewer.

When a step has no template yet, write one with the same six sections rather than improvising a chat prompt:
role, inputs, task, rules, output contract, self-check — plus the header block that names the checklist and the
output path. Then adapt it with A2, version it, and add it to [Appendix A](#appendix-a--kit-document-map).

## A8. How to score a checklist

The kit checklists are `.xlsx` files with the columns
`Category | Checklist Item | Description / Question | Status | Notes / Action Items`.
Keep `Status` and `Notes / Action Items`, and add `Evidence`, `Owner` and `Gate`:

| Column | Fill with | Not acceptable |
|---|---|---|
| `Status` | `Pass` / `Partial` / `Fail` / `N/A` | `Pending` at a gate; blank rows |
| `Evidence` | Section number, requirement ID, line reference, file path, log name | "OK", "checked", "looks fine" |
| `Notes / Action Items` | The fix, phrased as an action, plus owner and due date | A restatement of the checklist question |
| `Owner` | The human who fixes it | The agent that generated the artifact |
| `Gate` | Contribution to the gate (`Blocking` / `Non-blocking`) | Percentages that average a blocking failure away |

Scoring rules:

- `Pass` requires evidence the auditor can open independently.
- `Partial` is allowed only with owner + due date; it does not count as done.
- `Fail` is blocking for the phase gate, even if only one row fails.
- `N/A` requires a one-line justification (for example "no external interface in this release").
- An auditor must not edit the artifact it audits; the audit output is a separate report
  (`brd-audit.md`, `prd-audit.md`, `design-audit.md`, …).

## A9. Identifier scheme

Keep the scheme stable across phases so the matrices can be checked mechanically:

| Prefix | Meaning | Introduced in | Traced to |
|---|---|---|---|
| `SRC-xxx` | Source document / interview record | Phase 1–2 | `intent.md`, `BRD.md` |
| `BO-xxx` | Business objective | Phase 2 | `BR-xxx`, success measures |
| `SN-xxx` / `STK-xxx` | Stakeholder need / stakeholder | Phase 2 | `BR-xxx` |
| `BR-xxx` | Business requirement | Phase 2 | `FR-xxx` |
| `FR-xxx` / `NFR-xxx` | Functional / non-functional requirement | Phase 3 | `US-xxx`, `CMP-xxx`, `TC-xxx` |
| `US-xxx` | User story | Phase 3 | `FR-xxx`, screens, `TASK-xxx` |
| `AC-xxx` | Acceptance criterion | Phase 3 | `TC-xxx` |
| `CMP-xxx` | Component / building block | Phase 4 | `FR-xxx`, `TASK-xxx` |
| `ADR-xxx` / `DEC-xxx` | Architecture decision | Phase 4 | `BR-xxx`/`NFR-xxx`, risks |
| `API-xxx` | Interface operation | Phase 4 | `FR-xxx`, `TC-xxx` |
| `TASK-xxx` | Task card / WBS element | Phase 5 | `US-xxx`, `FR-xxx`, commits |
| `TC-xxx` | Test case | Phase 7 | `AC-xxx`, evidence path |
| `DEF-xxx` | Defect | Phase 7 | `TC-xxx`, `TC-xxx` rerun |
| `OQ-xxx` / `ASM-xxx` / `RISK-xxx` | Open question / assumption / risk | any phase | owner + due date |

`traceability.md` (phase 3) and `RTM.md` (phase 7) are the two matrices that must stay two-way complete:
every child has a parent, every parent has a child.

## A10. Roles

Generic roles from SOP §4; map each to a named person or group during A2.

| Role | Accountable for | Main phases |
|---|---|---|
| BA / product owner | Problem, users, priorities, acceptance criteria, business approvals | 1–3 |
| Human owner / engineer | Agent selection and scope, data protection, validation of output, traceability | 3–7 |
| Reviewer | Independent review of the change as software, with evidence | 8 |
| Tech lead / architect | Design and risk decisions, architecture approvals, exceptions | 3–5, 8 |
| Security / privacy / compliance owner | Threat/risk assessment, sensitive data, regulated use, exceptions | 1, 4, 7, 8 |
| Release owner / on-call engineer | Release authorization, deployment, monitoring, rollback, incidents | 9–10 |

One person may hold several roles in a small team, but the author never waives a mandatory independent
review or approval.

## A11. Template coverage by phase

Each phase below names the template it runs and the gap it closes. Use the mapping so no step is improvised
in chat:

| Phase | Templates in this kit | How to proceed |
|---|---|---|
| 1 Intake | `requirements/Intake_Intent_Prompt.md`; no checklist | Use the template; gate on the SOP §5.1 exit criteria |
| 4 Design (cross-artifact audit) | `design/Design_Audit_Prompt.md` plus the per-artifact checklists | Use the template; it runs the ten pairwise checks and scores each artifact |
| 6 Implementation | `development/Implementation_Task_Prompt.md`; review checklist | Use the template with the task card; the IEEE 1028 checklist is read before coding |
| 7 Verification | `verification/TestPlan_IEEE 829-2008_prompt.md`, `TestCase_RTM_IEEE_829_Prompt.md`, `TestReport_IEEE_829_Prompt.md`; IEEE 829 checklist | Use the three templates in order: plan → cases and matrix → report |
| 8 Review | `verification/Code_Review_IEEE_1028_Prompt.md`; IEEE 1028 checklist | Use the template as a read-only reviewer; a human approves |
| 9–11 Release, Operations, Decommissioning | No templates | Follow SOP §5.9–§5.11 and record the evidence the SOP asks for; write a project template if the work repeats |

Every phase from 1 to 8 therefore has a template with the same six sections. Phases 9–11 are governed by the
organization's release, incident and decommissioning processes — do not invent a prompt where a controlled
process already exists.

If a phase keeps falling back to a chat prompt, that is a signal to write a project template with the A7
structure, adapt it with A2, version it, and share it back into the kit.

---

# Part B — Phase-by-phase steps

Every phase below uses the same layout: goal, inputs, kit documents, steps, prompt pattern, outputs,
gate, watch-outs. The handoff record from SOP §5.12 closes each phase.

## Phase 1 — Intake

**Goal:** turn a raw request into a bounded work item with a named owner, acceptance criteria and a risk
tier, so later phases have an unambiguous starting point (SOP §5.1).

**Inputs:** ticket, email, meeting notes, incident report, or sponsor brief.

**Kit documents**

| Kind | Document | Use |
|---|---|---|
| Guidance | [AI_SDLC-SOP.md](./AI_SDLC-SOP.md) §5.1 | Goal, risk tiers and controls, exit criteria |
| Guidance | [agentic-sdlc-process.md](./agentic-sdlc-process.md) §2 | Four intake steps and the 7 intent sections |
| Prompt | [requirements/Intake_Intent_Prompt.md](./requirements/Intake_Intent_Prompt.md) | Drafts `intent.md`, `sources.md`, `glossary.md`, `stakeholders.md` and proposes the risk tier |
| Checklist | None in this kit | Gate on the SOP §5.1 exit criteria; the template's §6 encodes them as self-check items |

**Steps**

| # | Step | Produce |
|---|---|---|
| 1 | Collect every source into one list; give each its own `SRC-xxx` and a one-line reliability note | `docs/01-intake/sources.md` |
| 2 | Draft `intent.md` with exactly seven sections: Problem · Proposed outcome · Affected users · Constraints · Success measures · Out of scope · Open questions — or run the intake template to draft it | `docs/01-intake/intent.md` |
| 3 | Write `glossary.md` (term, definition, synonyms to avoid) and `stakeholders.md` (person, role, concern, influence) | `docs/01-intake/glossary.md`, `stakeholders.md` |
| 4 | Set success measures with baseline, target and measurement method; number open questions `OQ-xxx` with the person who answers | `intent.md` |
| 5 | Assign owner, acceptance criteria and risk tier (Low/Medium/High per SOP §5.1), list required reviewers and data/tool constraints | work item |
| 6 | Requester confirms the problem and outcome statement; record the confirmation and hand off to requirements | work item + handoff record |

**Run**

```text
@<path-to-folder>/requirements/Intake_Intent_Prompt.md
```

The template carries the seven `intent.md` sections, the source registry, the glossary and stakeholder
tables, and the risk-tier proposal; fill §2.2 with the request, the accountable owner and your organization's
risk-tier table before sending it.

**Outputs:** `docs/01-intake/` (or the equivalent work-item fields), plus the risk tier and approver list.

**Gate**

- Owner, acceptance criteria and risk tier recorded.
- Every scope-blocking question is answered or has an owner and date.
- Required reviewers and any agent/tool/data constraints identified.
- Requester confirmed the problem statement.

**Watch-outs**

- Intake is not a design phase: no technology, no architecture, no estimates.
- A vague success measure ("faster", "better UX") is a defect; require a number and a method.
- Do not start requirements work while ownership or the outcome is unclear.

## Phase 2 — Requirements

**Goal:** produce a baselined BRD by running a structured elicitation session and authoring the document
to IEEE 29148, then auditing it before baseline (SOP §5.2).

**Inputs:** baselined intake records (`intent.md`, `stakeholders.md`, `glossary.md`, `sources.md`).

**Kit documents**

| Kind | Document | Use |
|---|---|---|
| Prompt | [analysis/BRD_Elicitation_Prompt_IEEE_standard.md](./analysis/BRD_Elicitation_Prompt_IEEE_standard.md) | Runs the elicitation session and can author `BRD.md` |
| Prompt | [analysis/BRD_Prompt_IEEE_standard.md](./analysis/BRD_Prompt_IEEE_standard.md) | Fuller BRD structure when a complete document is required |
| Template | [requirements/BRD-Template.md](./requirements/BRD-Template.md), [requirements/BRD-Template.docx](./requirements/BRD-Template.docx) | Presentation layer only — content quality comes from the standard |
| Checklist | [analysis/BRD_IEEE_29148_Checklist.xlsx](./analysis/BRD_IEEE_29148_Checklist.xlsx) | Audit: IEEE 29148 characteristics and BRD completeness |

**Steps**

| # | Step | Produce |
|---|---|---|
| 1 | Fill `## 2.2 Project parameters` (business foundation, sponsor, source evidence, house template) and finish the A2 adaptation | adapted prompt |
| 2 | Run the elicitation session against the real stakeholders: at most three questions per turn, priority order goal → scope → rules, no answering on the stakeholder's behalf, a session status after each turn | `docs/02-requirements/interviews/SRC-xxx.md` |
| 3 | Author the BRD with the authoring prompt; keep the elicitation prompt for the session and the authoring prompt for the document when both are needed | `docs/02-requirements/BRD.md` |
| 4 | Check every business requirement has an acceptance criterion and a verification method; collect `OQ-xxx` at the end | `BRD.md` |
| 5 | Audit in a clean session or auditor sub-agent against the checklist: `Pass`/`Partial`/`Fail`/`N/A`, evidence per row, no edits to the BRD | `docs/02-requirements/brd-audit.md` |
| 6 | Fix by risk, re-audit (max three rounds), then request PM/PO approval and baseline | git tag `requirements-v1` |

**Run**

```text
@<path-to-folder>/analysis/BRD_Elicitation_Prompt_IEEE_standard.md
```
Or 

```text
@<path-to-folder>/analysis/BRD_Prompt_IEEE_standard.md
```

Run the elicitation template to conduct the session and record `interviews/SRC-*.md`; run the authoring
template when the BRD needs the full document structure. Both write the BRD through their §5 output contract.

**Outputs:** `docs/02-requirements/BRD.md`, `interviews/SRC-xxx.md`, `brd-audit.md`, baseline tag.

**Gate**

- Every `BR-xxx` traces to a business objective or stakeholder need.
- Every objective and success measure has baseline, target and measurement method.
- 0 `Fail`; every `Partial` has owner and due date.
- PM/PO approved and the BRD is baselined.

**Watch-outs**

- The house template changes presentation, not substance; do not delete required content to fit a form.
- Requirements phrased as solutions ("the system shall use X") belong in design, not in the BRD.
- An audit that edits the document it audits is not an audit.

## Phase 3 — Analysis

**Goal:** turn the baselined BRD into measurable, testable, traceable requirements (SRS or PRD) plus user
stories with acceptance criteria, and baseline them (SOP §5.3).

**Inputs:** baselined `BRD.md`, interviews, glossary, stakeholders.

**Kit documents**

| Kind | Document | Use |
|---|---|---|
| Prompt | [analysis/PRD_Prompt_IEEE_standard.md](./analysis/PRD_Prompt_IEEE_standard.md) | PRD with strategy, personas, FR/US, UX requirements, release criteria |
| Prompt | [analysis/PRD_prompt.md](./analysis/PRD_prompt.md) | Full IEEE 29148 PRD generator with input analysis and traceability sections |
| Prompt | [analysis/PRD_Prompt_with_template.md](./analysis/PRD_Prompt_with_template.md) | Same generator when a house PRD template must be followed |
| Checklist | [analysis/PRD_IEEE_29148_Checklist.xlsx](./analysis/PRD_IEEE_29148_Checklist.xlsx) | Audit: requirement characteristics, completeness, traceability |

**Steps**

| # | Step | Produce |
|---|---|---|
| 1 | Choose the prompt variant: full IEEE 29148 generator for regulated or engineering-led work, house-template variant when the organization mandates a form | adapted prompt |
| 2 | Derive `FR-xxx` and `NFR-xxx` from `BR-xxx`; give every requirement an ID, source, priority, acceptance criterion and verification method | `docs/03-analysis/PRD.md` or `SRS.md` |
| 3 | Make every NFR measurable: metric, threshold, measurement method, and where it is observed. Ban adjectives ("fast", "friendly") | `PRD.md` |
| 4 | Write user stories — one user-visible outcome each — in "As a <role>, I want <capability>, so that <benefit>" form, ≤5 Given-When-Then acceptance criteria, and the `FR-xxx` IDs it covers | `docs/03-analysis/USER_STORIES.md` |
| 5 | Audit against the checklist in a clean session; mark requirement-level defects with § and ID | `docs/03-analysis/prd-audit.md` |
| 6 | Build the two-way matrix BO → BR → FR → US and flag every broken branch as `[ORPHAN]` | `docs/03-analysis/traceability.md` |
| 7 | Fix, re-audit, then request PM/PO approval (plus tech lead when architecture, data or NFRs are affected) and baseline | git tag `analysis-v1` |

**Run**

```text
@<path-to-folder>/analysis/PRD_prompt.md
```

Use `@<path-to-folder>/analysis/PRD_Prompt_IEEE_standard.md` for the shorter five-part PRD, or
`@<path-to-folder>/analysis/PRD_Prompt_with_template.md` when a house template is mandated. All
three carry the same inputs, task, rules and IEEE 29148 self-check.

**Outputs:** `PRD.md` or `SRS.md`, `USER_STORIES.md`, `traceability.md`, `prd-audit.md`, baseline tag.

**Gate**

- 100% of `FR-xxx`/`NFR-xxx` trace to a `BR-xxx`; 0 orphan.
- 100% of `US-xxx` have acceptance criteria and requirement IDs.
- Every NFR has a metric, threshold and measurement method.
- 0 `Fail`; conflicts and duplicates resolved or recorded as `OQ-xxx`/`RISK-xxx`.

**Watch-outs**

- Do not restate the BRD as a PRD; the PRD adds specificity and measurable criteria.
- Unresolved conflicts must not become silently accepted requirements.
- Stories sized too large to verify on their own are a planning risk; split them now.

## Phase 4 — Design

**Goal:** translate baselined requirements into an implementable design — SAD with 4+1 views, IEEE 1016
blueprint, UML diagram sources, interface contracts, data model and UI/UX — each audited before baseline
(SOP §5.4; [agentic-sdlc-process.md](./agentic-sdlc-process.md) §5).

**Inputs:** baselined `BRD.md`, `PRD.md`/`SRS.md`, `USER_STORIES.md`, `traceability.md`, plus architecture
constraints (approved stack, hosting, security, regulatory).

**Kit documents**

| Kind | Document | Use |
|---|---|---|
| Prompt | [design/SAD_Prompt_IEEE_standard.md](./design/SAD_Prompt_IEEE_standard.md) | SAD following IEEE 1016-2009 |
| Prompt | [design/SAD_prompt.md](./design/SAD_prompt.md) | Full IEEE 1016 view set with stakeholder concerns and quality scenarios |
| Prompt | [design/SAD_Prompt_with_template_.md](./design/SAD_Prompt_with_template_.md) | SAD when a house template applies |
| Checklist | [design/SAD_IEEE_1016_Checklist.xlsx](./design/SAD_IEEE_1016_Checklist.xlsx) | Audit the SAD |
| Prompt | [design/bluePrint_design_prompt.md](./design/bluePrint_design_prompt.md) | IEEE 1016-2009 blueprint: eight design views linked back to stakeholder concerns and quality scenarios |
| Checklist | [design/BluePrint_Design_IEEE_1016_2009_Checklist.xlsx](./design/BluePrint_Design_IEEE_1016_2009_Checklist.xlsx) | Audit the blueprint |
| Prompt | [design/classDiagram_prompt.md](./design/classDiagram_prompt.md), [design/sequenceDiagram_prompt.md](./design/sequenceDiagram_prompt.md), [design/activityDiagram_prompt.md](./design/activityDiagram_prompt.md), [design/componentDiagram_prompt.md](./design/componentDiagram_prompt.md), [design/deploymentDiagram_prompt.md](./design/deploymentDiagram_prompt.md), [design/useCase_prompt.md](./design/useCase_prompt.md) | 4+1 view diagrams as draw.io XML |
| Checklist | [design/Class_Diagram_UML2.0_Checklist.xlsx](./design/Class_Diagram_UML2.0_Checklist.xlsx), [design/Sequence_Diagram_UML2.0_Checklist.xlsx](./design/Sequence_Diagram_UML2.0_Checklist.xlsx), [design/Activity_Diagram_UML2.0_Checklist.xlsx](./design/Activity_Diagram_UML2.0_Checklist.xlsx), [design/Component_Diagram_UML2.0_Checklist.xlsx](./design/Component_Diagram_UML2.0_Checklist.xlsx), [design/Deployment_Diagram_UML2.0_Checklist.xlsx](./design/Deployment_Diagram_UML2.0_Checklist.xlsx), [design/UseCase_Document_UML2.0_Checklist.xlsx](./design/UseCase_Document_UML2.0_Checklist.xlsx) | Audit each diagram |
| Prompt | [design/apiDesign_prompt.md](./design/apiDesign_prompt.md) | Interface contracts (OpenAPI) |
| Checklist | [design/API_Design_IEEE-1016-2009Checklist.xlsx](./design/API_Design_IEEE-1016-2009Checklist.xlsx) | Audit the API design |
| Prompt | [design/databaseDesign_SQL_prompt.md](./design/databaseDesign_SQL_prompt.md), [design/databaseDesign_NoSQL_prompt.md](./design/databaseDesign_NoSQL_prompt.md), [design/databaseDesign_VectorDB_prompt.md](./design/databaseDesign_VectorDB_prompt.md), [design/databaseDesign_GraphrDB_prompt.md](./design/databaseDesign_GraphrDB_prompt.md) | Data design per workload type |
| Checklist | [design/Database_Design_Checklist.xlsx](./design/Database_Design_Checklist.xlsx), [design/Polyglot_DB_Design_Checklist.xlsx](./design/Polyglot_DB_Design_Checklist.xlsx), [design/Checklist_Database Design Review.xlsx](./design/Checklist_Database%20Design%20Review.xlsx) | Audit the data design |
| Prompt | [design/UI-UX-Design_prompt.md](./design/UI-UX-Design_prompt.md) | Personas, flows, frames/HTML from the blueprint |
| Checklist | [design/UI_UX_Design_IEEE-1016-2009_Checklist.xlsx](./design/UI_UX_Design_IEEE-1016-2009_Checklist.xlsx) | Audit the UI/UX design |
| Prompt | [design/Design_Audit_Prompt.md](./design/Design_Audit_Prompt.md) | Cross-artifact audit: SAD ↔ blueprint ↔ diagrams ↔ API ↔ data ↔ UI/UX |

**Steps**

| # | Step | Produce |
|---|---|---|
| 1 | Pick the SAD template variant, fill `## 2.2` (system foundation, approved stack, constraints), and keep the output in the organization's SAD template | `docs/04-design/SAD.md` |
| 2 | Cover the five views — Logical, Process, Development, Physical, Scenarios — and record which requirement IDs each view satisfies | `SAD.md` |
| 3 | Record at least the decisions that are hard to reverse as ADRs: context, options, decision, consequences, status | `docs/04-design/ADR-xxx.md` |
| 4 | Draw one canonical diagram per view with the matching diagram prompt; save the `.drawio` source and export images only for embedding | `docs/04-design/diagrams/*.drawio` |
| 5 | Audit every diagram with its UML 2.0 checklist; fix high-severity notation and completeness defects | audit notes per diagram |
| 6 | Author the blueprint and check traceability from stakeholder concern to design element | `docs/04-design/blueprint.md` |
| 7 | Define interface contracts: auth and authorization per role, request/response schemas with examples, error codes and messages, rate limits, idempotency, requirement mapping | `docs/04-design/openapi.yaml`, `api.md` |
| 8 | Design data: choose SQL, NoSQL, vector or graph per workload, include migration and rollback, document retention and classification | `docs/04-design/data/model.md` |
| 9 | Design UI/UX from the blueprint: persona goals, flows, states (empty/error/loading), WCAG 2.1 AA; add every screen to `USER_STORIES.md` with the story and requirement IDs it serves | `docs/04-design/UI_UX_design/`, updated `USER_STORIES.md` |
| 10 | Run a cross-artifact audit in a read-only session: SAD ↔ blueprint ↔ diagrams ↔ API ↔ data ↔ UI/UX. Orphan elements, missing flows, contract drift and ownerless NFRs are blocking | `docs/04-design/design-audit.md` |
| 11 | Fix discrepancies through ADRs (never by silent edit), then obtain tech lead/architect approval, security review where sensitive data or external interfaces are involved, and PO review where user-visible behaviour changes | git tag `design-v1` |

**Run**

```text
@<path-to-folder>/design/SAD_Prompt_IEEE_standard.md
```

Every other design artifact has its own template with the same contract: `design/SAD_prompt.md` and
`design/SAD_Prompt_with_template_.md` for the SAD variants, `design/bluePrint_design_prompt.md`, the six UML
diagram prompts, `design/apiDesign_prompt.md`, the four `design/databaseDesign_*_prompt.md` prompts,
`design/UI-UX-Design_prompt.md`, and `design/Design_Audit_Prompt.md` for step 10.

**Outputs:** `SAD.md`, `ADR-*.md`, `blueprint.md`, `diagrams/*.drawio`, `openapi.yaml`, `data/model.md`,
`UI_UX_design/`, `design-audit.md`, baseline tag.

**Gate**

- Every view has an editable diagram source and an audit result.
- Every NFR has an identified place in the design where it is realized.
- Contracts and data model agree with the SAD; any difference is captured in an ADR.
- Every screen traces to a story and requirement IDs; 0 orphan diagram elements or screens.
- 0 blocking contradictions; 0 `Fail`; required approvals and security review recorded.

**Watch-outs**

- Do not invent components, lifelines or nodes that do not exist in the SAD.
- A diagram that exists only as an image cannot be reviewed or maintained.
- UI/UX without an error and empty state is incomplete, not "phase 2".
- Silent contract changes break phase 5 and phase 7; force them into an ADR.

## Phase 5 — Planning

**Goal:** turn the approved design and baselined requirements into an executable plan the team can commit
to — SDP, WBS and task cards small enough for a single agent session (SOP §5.5;
[agentic-sdlc-process.md](./agentic-sdlc-process.md) §6).

**Inputs:** `SAD.md`, ADRs, `PRD.md`, `USER_STORIES.md`, `traceability.md`, delivery constraints.

**Kit documents**

| Kind | Document | Use |
|---|---|---|
| Prompt | [development/DevPlan_ISO_24748_5_Prompt.md](./development/DevPlan_ISO_24748_5_Prompt.md) | Software Development Plan per ISO/IEC/IEEE 24748-5 |
| Checklist | [development/DevPlan_ISO_24748_5_Checklist.xlsx](./development/DevPlan_ISO_24748_5_Checklist.xlsx) | Audit the SDP |
| Prompt | [development/TaskBreakdown_ISO_21511_Prompt.md](./development/TaskBreakdown_ISO_21511_Prompt.md) | WBS, WBS dictionary, dependencies and task cards per ISO 21511 |

**Steps**

| # | Step | Produce |
|---|---|---|
| 1 | Fill `## 2.2` in both templates (project name/ID, document IDs, owner, approvers, language, delivery model, task-size limit, agent iteration limit, regulatory context) — this is the A2 adaptation for this phase | adapted prompts |
| 2 | Author the Software Development Plan with the DevPlan prompt; keep its output contract and front matter | `docs/05-development/Software_Development_Plan.md` |
| 3 | Derive the deliverable-oriented WBS, WBS dictionary, dependency model and task cards with the TaskBreakdown prompt | `docs/05-development/WBS.md`, `docs/05-development/tasks/<task-id>.md` |
| 4 | Write each task card with: objective, inputs, files to touch, acceptance criteria, verification method, and explicit "do not do" scope | task cards |
| 5 | Size every task to one agent session (iteration and file limits from step 1); split anything larger instead of stuffing it | task cards |
| 6 | Sequence by dependency, add estimates, owners and the `US-xxx`/`FR-xxx` IDs each task satisfies; mark the critical path | `PLAN`/`WBS.md` |
| 7 | Record open decisions, assumptions and risks with owner and date; unresolved items appear in the appendix the prompt defines | plan appendices |
| 8 | Audit the plan against the ISO 24748-5 checklist; verify every task card has the mandatory fields | plan audit notes |
| 9 | Review: PM/PO approve scope and sequencing, tech lead/architect approve feasibility and dependencies; baseline | git tag `plan-v1` |

**Run**

```text
@<path-to-folder>/development/DevPlan_ISO_24748_5_Prompt.md
@<path-to-folder>/development/TaskBreakdown_ISO_21511_Prompt.md
```

The first writes the plan; the second decomposes it into the WBS and task cards. Both take their parameter
block from §2.2, so the project IDs, owners, language, size limits and regulatory context are set once in each.

**Outputs:** `Software_Development_Plan.md`, `WBS.md`, `tasks/<task-id>.md`, baseline tag.

**Gate**

- Every task has acceptance criteria, files to touch, a verification method and US/FR links.
- Every task fits the agreed size limit; no task hides multiple deliverables.
- Dependency order is buildable; critical path and risks have owners.
- 0 `Fail`; PM/PO and tech lead approvals recorded.

**Watch-outs**

- Task cards that name non-existent paths cause phase 6 drift; mark planned paths explicitly.
- Estimates without assumptions are guesses; keep the assumption next to the number.
- A plan that ignores the agent size limit will fail in implementation, not in planning.

## Phase 6 — Implementation

**Goal:** implement one approved task as a bounded, reviewable change the human owner can explain,
validate and defend (SOP §5.6).

**Inputs:** approved task card, repository instructions (`AGENTS.md`, `CLAUDE.md` or equivalent),
existing tests, related ADRs.

**Kit documents**

| Kind | Document | Use |
|---|---|---|
| Guidance | [AI_SDLC-SOP.md](./AI_SDLC-SOP.md) §5.6 and §3 (operating principles) | Controls for agent-assisted edits |
| Prompt | [development/Implementation_Task_Prompt.md](./development/Implementation_Task_Prompt.md) | Binds the run to one task card: allowed files, checks, iteration limit, stop rules |
| Checklist | [verification/Code_Review_IEEE_1028_Checklist.xlsx](./verification/Code_Review_IEEE_1028_Checklist.xlsx) | Used at phase 8; read it before coding so the change is reviewable |

**Steps**

| # | Step | Produce |
|---|---|---|
| 1 | Confirm repository, branch and working-tree state; read the repository instructions, the task card and the affected tests before any edit | clean branch |
| 2 | Ask the agent to restate the plan in five lines (files, approach, checks) and approve or reject it before edits start | approved plan |
| 3 | Constrain edits to the files listed in the task card; no unrelated refactors, no vendored/generated edits, no new dependencies without approval | diff |
| 4 | Forbid weakening or deleting tests to make a run pass; new behaviour gets new assertions | tests |
| 5 | Run the project's real checks (format, lint, type, unit, integration, secret and dependency scans, build) and paste the actual output, not a summary | command output |
| 6 | Update `traceability.md` (US ↔ FR ↔ code ↔ test) and record significant agent assistance in the work item or PR | `traceability.md`, work item |
| 7 | Commit in small, conventional commits linked to the task and work item; state the deviation from the approved design if any | commits |
| 8 | Inspect the complete diff yourself, then hand the change to verification with known gaps and unverified behaviour listed | handoff record |

**Run**

```text
@<path-to-folder>/development/Implementation_Task_Prompt.md
```

The template binds the run to one task card: it reads `FILES_ALLOWED`, the check commands and the iteration
limit from §2.2, refuses to weaken tests, and stops rather than guessing when the task needs a design change.

**Outputs:** source and test changes on the approved branch, updated traceability, PR linked to the work
item, handoff record.

**Gate**

- The owner can explain every hunk and the reasoning behind it.
- Required checks actually pass, with output recorded; failing or skipped checks are disclosed.
- No scope drift, no unrelated edits, no temporary files or debug code.
- Traceability updated; agent assistance recorded.

**Watch-outs**

- An agent's "tests pass" claim is not evidence; read the command output (SOP §3, principle 5).
- Stop and escalate on unexplained broad changes, suspicious dependencies or credential requests (SOP §7).
- Never let implementation silently redefine a design decision; that is an ADR in phase 4.

## Phase 7 — Verification

**Goal:** produce evidence, appropriate to the risk tier, that the change meets its acceptance criteria
and does not regress existing behaviour (SOP §5.7).

**Inputs:** `PRD.md`, `USER_STORIES.md`, `SAD.md`, `openapi.yaml`, the plan, the change under test.

**Kit documents**

| Kind | Document | Use |
|---|---|---|
| Prompt | [verification/TestPlan_IEEE 829-2008_prompt.md](./verification/TestPlan_IEEE%20829-2008_prompt.md) | IEEE 829 test plan from requirements, design, UI, API and stories |
| Checklist | [verification/Test_Plan_IEEE_829_Checklist.xlsx](./verification/Test_Plan_IEEE_829_Checklist.xlsx) | Audit the test plan, and anchor cases and report sections |
| Prompt | [verification/TestCase_RTM_IEEE_829_Prompt.md](./verification/TestCase_RTM_IEEE_829_Prompt.md) | Derives test cases from acceptance criteria and builds the two-way RTM |
| Prompt | [verification/TestReport_IEEE_829_Prompt.md](./verification/TestReport_IEEE_829_Prompt.md) | Writes the IEEE 829 test summary report and the GO/NO-GO recommendation from recorded evidence |

**Steps**

| # | Step | Produce |
|---|---|---|
| 1 | Gather all inputs — requirements, stories, design, contracts, plan — not only the code | input list |
| 2 | Author the test plan with the prompt: scope, items, features to test, approach, environment, data, entry/exit criteria, risks | `docs/07-verification/TEST_PLAN.md` |
| 3 | Audit the plan against the IEEE 829 checklist before executing anything | plan audit notes |
| 4 | Derive test cases from acceptance criteria, not from the implementation, using the test-case template: `TC-xxx` with preconditions, steps, concrete data, expected result and how it is proven | `docs/07-verification/TEST_CASES.md` |
| 5 | Ensure every acceptance criterion has at least one case, and that P0 paths also get boundary, negative and permission cases | `TEST_CASES.md` |
| 6 | Build the two-way matrix AC → TC → result → evidence path; an acceptance criterion without a case is a blocking gap, recorded as `GAP` not left blank | `docs/07-verification/RTM.md` |
| 7 | Pin the commit, environment and run-id; execute; store logs, screenshots, responses and query results per run | `docs/07-verification/evidence/<run-id>/` |
| 8 | Triage failures: minimal reproduction, log, suspected cause, defect `DEF-xxx`. Do not fix source or tests mid-run, do not delete or silence failing tests | defect list, updated RTM |
| 9 | Write the test summary report from the RTM and evidence with the report template: summary · scope and environment · variances · coverage and what was not tested · results by test level · defects and risks · GO/NO-GO with approvals | `docs/07-verification/TEST_REPORT.md` |
| 10 | Have the verification owner and QA reviewer confirm the evidence covers the acceptance criteria and that limitations are disclosed | approval |

**Run**

```text
@<path-to-folder>/verification/TestPlan_IEEE 829-2008_prompt.md
@<path-to-folder>/verification/TestCase_RTM_IEEE_829_Prompt.md
@<path-to-folder>/verification/TestReport_IEEE_829_Prompt.md
```

Plan first, then design the cases and the matrix, then write the report from the recorded evidence. Each
template refuses to state a result it cannot trace to an evidence path. The test-plan file name contains a space:
attach it if your tool cannot resolve a reference containing one.

**Outputs:** `TEST_PLAN.md`, `TEST_CASES.md`, `RTM.md`, `evidence/<run-id>/`, defect list,
`TEST_REPORT.md`, approval record.

**Gate**

- 100% of acceptance criteria have at least one executed case with evidence.
- NFRs are measured against their thresholds, or explicitly reported as not measured.
- 0 acceptance criteria without a case or a recorded `GAP` with owner.
- Every result points to an openable evidence artifact; skips have a reason and an approver.
- Required checks pass; limitations and residual risks disclosed.

**Watch-outs**

- Tests written against the current implementation prove the code, not the requirement.
- A pass rate without an RTM is a number, not evidence.
- Deleting or silencing a failing test converts a defect into a false GO.

## Phase 8 — Review

**Goal:** obtain independent, qualified review of the change as software, plus the approvals its risk tier
requires, before merge (SOP §5.8).

**Inputs:** pull request or equivalent review request, complete diff, task card, verification evidence,
risk tier.

**Kit documents**

| Kind | Document | Use |
|---|---|---|
| Checklist | [verification/Code_Review_IEEE_1028_Checklist.xlsx](./verification/Code_Review_IEEE_1028_Checklist.xlsx) | Review record: objective, entry criteria, design conformance, logic, tests, security, documentation |
| Guidance | [AI_SDLC-SOP.md](./AI_SDLC-SOP.md) §5.8, §8 | Review rules and what the PR record must contain |
| Prompt | [verification/Code_Review_IEEE_1028_Prompt.md](./verification/Code_Review_IEEE_1028_Prompt.md) | Read-only review: findings per line, blocking separated from non-blocking, no approval |

**Steps**

| # | Step | Produce |
|---|---|---|
| 1 | Open the review request linked to the work item, summarizing problem, behaviour change, risk tier, checks run, checks not run and material agent assistance | PR record |
| 2 | Keep the diff reviewable; split large changes by deliverable rather than by file type | PR |
| 3 | Assign a qualified reviewer who is not the author. An agent may summarize the diff but is never the reviewer or approver | reviewer assignment |
| 4 | Reviewer reads the code itself, not the summary: correctness against acceptance criteria, design conformance, maintainability, tests and evidence, security and data handling, dependencies and licensing, accessibility and compatibility as applicable, and whether generated artifacts are intended | review notes |
| 5 | Score the IEEE 1028 checklist with line-level evidence; blocking findings are explicit | review record |
| 6 | Author resolves blocking findings and re-runs affected checks; replies with the change or the rationale | updated PR |
| 7 | Obtain the domain, security or architecture approvals the risk tier requires and confirm they apply to the exact commit to be merged | approvals |
| 8 | Record accepted non-blocking follow-ups with an owner, then merge under branch protection | merge + follow-ups |

**Run**

```text
@<path-to-folder>/verification/Code_Review_IEEE_1028_Prompt.md
```

The template is a read-only reviewer: it scores the IEEE 1028 checklist with `file:line` evidence, separates
blocking from non-blocking findings, and states that it is not the approval.

**Outputs:** PR with review record, approvals on the exact commit, follow-up items with owners.

**Gate**

- Independent review by a qualified human who is not the author.
- 0 unresolved blocking findings; required checks pass on the reviewed commit.
- Required domain/security/architecture approvals recorded.
- Disclosed limitations accepted explicitly; no self-waived approvals.

**Watch-outs**

- Rubber-stamping because "the agent wrote it" or because "the agent reviewed it" violates SOP §5.8.
- Reviewing only the summary lets scope drift through; review the diff.
- Approvals on an older commit do not approve the merged commit.

## Phase 9 — Release

**Goal:** deploy the reviewed artifact under the existing release process, with the ability to detect and
reverse an unhealthy release (SOP §5.9).

**Inputs:** approved change, risk tier, release criteria, rollback plan, release calendar.

**Kit documents**

| Kind | Document | Use |
|---|---|---|
| Guidance | [AI_SDLC-SOP.md](./AI_SDLC-SOP.md) §5.9 | Release controls, authorization, evidence |
| Prompt / checklist | none in this kit | Use the organization's release checklist; record it with the release record |

**Steps**

| # | Step | Produce |
|---|---|---|
| 1 | Confirm the artifact corresponds to the reviewed commit and that checks and approvals are still valid | release pre-check |
| 2 | Prepare release notes, feature flags, migration sequence, monitoring and support readiness, and rollback or recovery steps | release plan |
| 3 | Have a named human release owner authorize and perform or supervise the deployment; an agent may prepare materials but must not authorize or execute privileged production changes | authorization |
| 4 | Deploy with staged rollout, canary or equivalent risk-appropriate control where available | deployment |
| 5 | Observe health indicators against pre-agreed thresholds for the observation window; stop or roll back when criteria are not met | health record |
| 6 | Record version or commit, environment, deployment time, authorizing owner and rollout result | `docs/09-release/<release-id>.md` |
| 7 | Hand the service to its operational owner with current runbooks, dashboards, alerts, support contacts and watch items | handoff record |

**Gate**

- A human authorized the release and the record names them.
- Deployment evidence and health observation are recorded.
- The service is stable, or the rollback/incident process is active with an owner.
- Outstanding risks have owners and a response plan.

**Watch-outs**

- Release control is not reduced because an agent assisted the change.
- A "successful deploy" without observed health indicators is not a successful release.
- Do not declare release complete while required health checks are outstanding.

## Phase 10 — Operations

**Goal:** keep the running service healthy and the operational record current, and handle defects and
incidents that follow a release (SOP §5.10).

**Inputs:** telemetry, logs, alerts, support tickets, incident reports, runbooks.

**Kit documents**

| Kind | Document | Use |
|---|---|---|
| Guidance | [AI_SDLC-SOP.md](./AI_SDLC-SOP.md) §5.10, §10 | Operational controls, incident authority, process health |
| Prompt / checklist | none in this kit | Use the organization's incident and operations process |

**Steps**

| # | Step | Produce |
|---|---|---|
| 1 | Monitor service health and user impact against the release success criteria for the observation window | watch record |
| 2 | Feed every incident or defect back through the normal process; a material change spawns a new intake item rather than an undocumented fix | work item |
| 3 | Let agents assist with log analysis, incident summaries or remediation proposals only on approved tools and approved data; redact sensitive content | incident notes |
| 4 | Keep decision and execution authority with the incident commander and authorized operators; never let an agent change production or present unverified conclusions as fact | incident log |
| 5 | Treat agent-introduced defects as normal defects: preserve evidence, follow reporting requirements, include agent use in the post-incident review where useful | post-incident review |
| 6 | Feed verified lessons into tests, documentation, prompts, repository instructions and the SOP — no secrets, no sensitive incident data | updated artifacts |
| 7 | Update runbooks, dashboards, alerts, support contacts and watch items, and record the operational record | `docs/10-operations/` |

**Gate**

- Operational ownership, monitoring, alerting and support information are current.
- Incidents and follow-up actions are tracked with owners.
- Lessons that affect prompts, checklists or tests have been applied or scheduled.
- Outstanding operational risks are accepted by the service owner.

**Watch-outs**

- Logs and telemetry may contain sensitive data; check the tool's approved data classification first.
- Closing a deployment task does not close the service; operational ownership stays active.
- Suppressing repeat incidents hides them from process health and from the next design cycle.

## Phase 11 — Decommissioning

**Goal:** retire a feature, service or repository without leaving data, access, dependencies or customer
commitments unresolved (SOP §5.11).

**Inputs:** service inventory, dependency map, data retention obligations, access and credential list,
customer and support commitments.

**Kit documents**

| Kind | Document | Use |
|---|---|---|
| Guidance | [AI_SDLC-SOP.md](./AI_SDLC-SOP.md) §5.11 | Retirement steps, evidence and approvals |
| Prompt / checklist | none in this kit | Use the organization's decommissioning checklist |

**Steps**

| # | Step | Produce |
|---|---|---|
| 1 | Inventory dependents, data stores, integrations, scheduled jobs, credentials and contracts; assign an owner per item | inventory |
| 2 | Define the disposition of each data set (retain, archive, delete) with the retention rule and the approving owner | data disposition plan |
| 3 | Plan the communication and support path (customers, internal consumers, on-call) and the retirement date | communication plan |
| 4 | Remove or redirect dependents, revoke access and credentials, remove resources, and stop scheduled work | change record |
| 5 | Verify from the authoritative systems — not from an agent's confirmation — that traffic stopped, access is revoked, resources are gone and data disposition matches the plan | verification evidence |
| 6 | Update inventories, runbooks, diagrams, architecture records and any published documentation | updated docs |
| 7 | Obtain service, data, security and business owner acceptance of the evidence; record exceptions and residual risks with owners | `docs/11-decommissioning/<id>.md` |

**Gate**

- Required owners accepted the retirement evidence; the retirement date and accountable owner are recorded.
- Data disposition and access revocation verified in the authoritative systems.
- Residual risks and follow-ups have owners; documentation and inventories updated.

**Watch-outs**

- An agent's statement that data was deleted is not evidence of deletion or compliance.
- Orphaned credentials outlive the service; revoke them explicitly.
- Do not close the retirement item while the service still has unresolved customer commitments.

---

# Part C — Cross-cutting steps

## C1. Change control after a baseline

Once an artifact is baselined (BRD, PRD, design, plan), a change goes through a recorded decision, not a
silent edit: raise the change, identify the affected IDs, update every downstream artifact and matrix,
re-audit the changed artifact, and re-baseline with a new tag. Keep the previous baseline so a reviewer can
diff intent against outcome.

## C2. Traceability upkeep

`traceability.md` (phase 3) and `RTM.md` (phase 7) are living documents:

- Regenerate them at the end of each phase that adds or renames IDs.
- Check both directions: every child has a parent; every parent has at least one child.
- Record deliberate gaps as `GAP`/`OQ` with owner and date. Never delete a row to make a matrix look complete.
- Use the identifier scheme in A9 so the check is mechanical rather than a reading exercise.

## C3. Prompt and checklist versioning

Treat prompts and checklists as versioned engineering assets:

- Keep them in the repository, with a version and an owner, next to the artifacts they produce.
- Change them through review, not ad hoc mid-session edits; note the version used in each artifact.
- Validate a change on real past cases before rollout; if output structure changes, re-run the audit that
  depends on it.
- Retire prompts that no longer match the standard or the organization, rather than leaving two variants.

## C4. Evidence and data handling

- Evidence must be openable by a reviewer who was not present when it was produced.
- Never place credentials, personal data, customer data or confidential prompts into artifacts, evidence
  folders or the work item (SOP §3, principle 2; §6).
- Define the retention period for evidence with the records owner; the kit makes no assumption about it.
- Record material agent assistance in the work item or PR, per SOP §8, and never record sensitive prompt content.

## C5. Agent and environment controls

Apply SOP §3 and §6 at every phase: approved tools and data only, least privilege, reviewable changes,
independent verification, protection of production, respected policy and provenance, transparency. When a
control must be bypassed, use SOP §7 — record the waived requirement, business reason, risk, compensating
controls, scope, approver and expiry — and stop agent activity if it requests sensitive data, attempts an
unauthorized action, or produces changes the owner cannot validate.

---

# Appendices

## Appendix A — Kit document map

| Phase | Prompt(s) in this kit | Checklist(s) in this kit | Primary artifacts |
|---|---|---|---|
| 1 Intake | `requirements/Intake_Intent_Prompt.md` | — (SOP §5.1 exit criteria) | `intent.md`, `glossary.md`, `stakeholders.md`, `sources.md` |
| 2 Requirements | `analysis/BRD_Elicitation_Prompt_IEEE_standard.md`, `analysis/BRD_Prompt_IEEE_standard.md`; template `requirements/BRD-Template.md`/`.docx` | `analysis/BRD_IEEE_29148_Checklist.xlsx` | `BRD.md`, `interviews/SRC-*.md`, `brd-audit.md` |
| 3 Analysis | `analysis/PRD_Prompt_IEEE_standard.md`, `analysis/PRD_prompt.md`, `analysis/PRD_Prompt_with_template.md` | `analysis/PRD_IEEE_29148_Checklist.xlsx` | `PRD.md`/`SRS.md`, `USER_STORIES.md`, `traceability.md`, `prd-audit.md` |
| 4 Design | `design/SAD_Prompt_IEEE_standard.md`, `design/SAD_prompt.md`, `design/SAD_Prompt_with_template_.md` | `design/SAD_IEEE_1016_Checklist.xlsx` | `SAD.md`, `ADR-*.md` |
| 4 Design | `design/bluePrint_design_prompt.md` | `design/BluePrint_Design_IEEE_1016_2009_Checklist.xlsx` | `blueprint.md` |
| 4 Design | `design/classDiagram_prompt.md`, `design/sequenceDiagram_prompt.md`, `design/activityDiagram_prompt.md`, `design/componentDiagram_prompt.md`, `design/deploymentDiagram_prompt.md`, `design/useCase_prompt.md` | `design/Class_Diagram_UML2.0_Checklist.xlsx`, `design/Sequence_Diagram_UML2.0_Checklist.xlsx`, `design/Activity_Diagram_UML2.0_Checklist.xlsx`, `design/Component_Diagram_UML2.0_Checklist.xlsx`, `design/Deployment_Diagram_UML2.0_Checklist.xlsx`, `design/UseCase_Document_UML2.0_Checklist.xlsx` | `diagrams/*.drawio` |
| 4 Design | `design/apiDesign_prompt.md` | `design/API_Design_IEEE-1016-2009Checklist.xlsx` | `openapi.yaml`, `api.md` |
| 4 Design | `design/databaseDesign_SQL_prompt.md`, `databaseDesign_NoSQL_prompt.md`, `databaseDesign_VectorDB_prompt.md`, `databaseDesign_GraphrDB_prompt.md` | `design/Database_Design_Checklist.xlsx`, `design/Polyglot_DB_Design_Checklist.xlsx`, `design/Checklist_Database Design Review.xlsx` | `data/model.md` |
| 4 Design | `design/UI-UX-Design_prompt.md` | `design/UI_UX_Design_IEEE-1016-2009_Checklist.xlsx` | `UI_UX_design/` |
| 4 Design | `design/Design_Audit_Prompt.md` | `design/SAD_IEEE_1016_Checklist.xlsx` + per-artifact checklists | `design-audit.md` |
| 5 Planning | `development/DevPlan_ISO_24748_5_Prompt.md`, `development/TaskBreakdown_ISO_21511_Prompt.md` | `development/DevPlan_ISO_24748_5_Checklist.xlsx` | `Software_Development_Plan.md`, `WBS.md`, `tasks/*.md` |
| 6 Implementation | `development/Implementation_Task_Prompt.md` | `verification/Code_Review_IEEE_1028_Checklist.xlsx` (used at review) | code, tests, updated `traceability.md` |
| 7 Verification | `verification/TestPlan_IEEE 829-2008_prompt.md`, `verification/TestCase_RTM_IEEE_829_Prompt.md`, `verification/TestReport_IEEE_829_Prompt.md` | `verification/Test_Plan_IEEE_829_Checklist.xlsx` | `TEST_PLAN.md`, `TEST_CASES.md`, `RTM.md`, `TEST_REPORT.md`, `evidence/` |
| 8 Review | `verification/Code_Review_IEEE_1028_Prompt.md` | `verification/Code_Review_IEEE_1028_Checklist.xlsx` | PR + review record + approvals |
| 9 Release | — (organization release process) | — | release record |
| 10 Operations | — (organization incident process) | — | runbooks, incident records |
| 11 Decommissioning | — (organization decommissioning process) | — | decommissioning record |

## Appendix B — Gate summary

| Phase | Gate in one line |
|---|---|
| 1 Intake | Named owner, acceptance criteria, risk tier, required approvals; no blocking scope question |
| 2 Requirements | Every BR traces upward; measurable objectives; 0 Fail; PM/PO baseline |
| 3 Analysis | 100% FR sourced, 100% US have AC and FR IDs, NFRs measurable, 0 orphan |
| 4 Design | Every view and artifact audited; no orphan element or screen; contracts match; approvals recorded |
| 5 Planning | Every task has AC, file list, verification method and US/FR links; sized to one agent session |
| 6 Implementation | Bounded diff the owner can explain; real checks green; traceability updated |
| 7 Verification | Every AC has an executed case with openable evidence; limitations disclosed |
| 8 Review | Independent human review complete; 0 blocking findings; approvals on the merged commit |
| 9 Release | Human authorization recorded; deployment and health evidence recorded; rollback ready |
| 10 Operations | Ownership, monitoring and support current; incidents tracked with owners |
| 11 Decommissioning | Data disposition and access revocation verified; owners accepted the evidence |

## Appendix C — Standards referenced by the kit

- IEEE 29148-2018 — requirements engineering (BRD, PRD/SRS, requirement characteristics)
- IEEE 1016-2009 — software design descriptions (SAD, blueprint)
- IEEE 829-2008 / IEEE 29119 — test documentation and test processes
- IEEE 1028 — software reviews and audits
- ISO/IEC/IEEE 24748-5:2017 — software development planning
- ISO 21511:2018 — work breakdown structures
- ISO/IEC/IEEE 42010 — architecture description
- ISO/IEC 25010 — quality model (the language of NFRs)
- UML 2.0 — diagram notation

Confirm which editions and interpretations your organization mandates during A2; the kit does not decide
that for you.

## Appendix D — First-use customization checklist

Before the first run in any project:

- [ ] Organization standards, templates and required document IDs identified and mapped to the kit documents.
- [ ] Every prompt to be used read end to end; placeholders, house-template hooks and parameter blocks filled or removed.
- [ ] Every checklist to be used extended with `Evidence`, `Owner`, `Due`, `Gate`; mandatory rows marked; thresholds set.
- [ ] Status vocabulary agreed, including what disqualifies `N/A`.
- [ ] Identifier scheme (A9) adopted, or mapped to the organization's existing scheme.
- [ ] Roles and approvers named per phase; author ≠ approver enforced.
- [ ] Risk tiers and their controls confirmed against SOP §5.1.
- [ ] Output language, units, date format and heading style agreed.
- [ ] Build, test, lint, scan and diagram tooling recorded so prompts can name real commands.
- [ ] Data classification and retention rules recorded; nothing sensitive in prompts or evidence.
- [ ] Baseline/tagging convention and handoff record agreed.
- [ ] Adaptation log started, with owner and review date.
- [ ] One pilot artifact produced and reviewed with the adapted prompt + checklist before team-wide rollout.

## Appendix E — Common failure modes

| Failure | Symptom | Fix |
|---|---|---|
| Kit used unadapted | Artifact looks standard-compliant but misses org sections, terminology or approvals | Run A2, log the adaptations, re-audit |
| Checklist not adapted with the prompt | Gate scores the wrong criteria; real defects pass | Adapt both together; re-verify row by row |
| `Pending` at a gate | Phase "complete" with unassessed rows | Ban `Pending`; require Pass/Partial/Fail/N/A |
| Audit edits the artifact | No independent check; findings disappear | Separate session, read-only auditor, separate report |
| Evidence is a claim | Numbers cannot be traced; release decisions rest on trust | Require file/§/ID/log evidence per row |
| Tests written from the code | Green tests, unmet requirements | Derive cases from acceptance criteria |
| Test weakened to pass | Defect converted to a pass | Forbid assertion weakening; review the test diff |
| Silent contract drift | Design, code and tests disagree | Force differences into ADRs and update matrices |
| Prompt edited per session | Inconsistent artifacts; no reproducibility | Version prompts; record version in the artifact |
| Agent approves its own work | Independent review bypassed | Enforce author ≠ approver; agent never approves |
| Traceability maintained by hand at the end | Broken chains, orphan IDs | Regenerate matrices each phase (C2) |
| Scope blocking question left open | Later phases re-litigate the requirement | `OQ-xxx` with owner and date, gated at intake |
