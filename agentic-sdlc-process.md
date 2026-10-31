# Agentic SDLC — Quy trình thực hành

> **Từng Phase → Từng Bước → Từng Tài liệu**
>
> Spec → Generate → Verify → Refine
>


---

## 1. Tổng quan Agentic SDLC

**Vòng lặp:** mỗi phase commit artifact → phase sau đọc artifact đó

### Chuỗi 11 Phase

1. **Intake** → 2. **Requirements** → 3. **Analysis** → 4. **Design** → 5. **Planning** → 6. **Build** → 7. **Verify** → 8. **Review** → 9. **Release** → 10. **Operate** → 11. **Decommission**

### 🔄 Vòng lặp cốt lõi cho MỌI đơn vị công việc

| SPECIFY | → GENERATE | → VERIFY | → REFINE | ↩ |
|---------|------------|----------|----------|---|

### 🤖 Agent làm

- Sinh bản nháp tài liệu theo template
- Audit theo rubric/checklist
- Vẽ sơ đồ, sinh code, chạy test
- Tìm mâu thuẫn, đề xuất sửa

### 👤 Con người làm

- Phỏng vấn stakeholder
- Phê duyệt, sign-off
- Quyết định trade-off, ưu tiên
- Review & chịu trách nhiệm

---

## 2. Phase 1 — Intake: Tiếp nhận ý tưởng

> Biến ý tưởng/yêu cầu thô thành work item có chủ sở hữu

| Bước | Nội dung |
|:----:|----------|
| 1 | **Thu thập ý tưởng & bối cảnh** — Agent đọc ticket/email/ghi chú, tổng hợp vấn đề, tìm prior art. Con người phỏng vấn stakeholder. |
| 2 | **Soạn intent.md** — 7 mục: Problem, Proposed outcome, Affected users, Constraints, Success measures, Out of scope, Open questions. |
| 3 | **Tạo tài liệu nền** — `glossary.md` (thuật ngữ), `stakeholders.md` (ai, vai trò, concern), `sources.md` (nguồn dữ liệu) |
| 4 | **Xác định risk tier & phê duyệt intent** — PO duyệt intent. Gán owner, acceptance criteria, risk tier (Low/Medium/High). |

**📄 Tài liệu tạo ra:** `intent.md` · `glossary.md` · `stakeholders.md` · `sources.md`
**📁 Lưu tại:** `docs/01-intake/` hoặc work item tracker

---

## 3. Phase 2 — Requirements: Thu thập yêu cầu nghiệp vụ

> Tạo BRD — tài liệu yêu cầu nghiệp vụ chuẩn ISO/IEC/IEEE 29148

| Bước | Nội dung |
|:----:|----------|
| 1 | **Elicitation — Khám phá nhu cầu** — Agent đóng vai AI-as-client đặt câu hỏi. Con người phỏng vấn stakeholder, quan sát hiện trường.<br>Prompt: `analysis/BRD_Elicitation_Prompt_IEEE_standard.md` |
| 2 | **Soạn BRD theo chuẩn** — Agent sinh BRD từ template chuẩn. Bao gồm: mục tiêu kinh doanh, stakeholders, yêu cầu nghiệp vụ, ràng buộc.<br>Prompt: `analysis/BRD_Prompt_IEEE_standard.md` |
| 3 | **Kiểm tra chất lượng BRD** — Đối chiếu với checklist IEEE 29148. Kiểm 7 thuộc tính: Correct, Unambiguous, Complete, Consistent, Verifiable, Traceable, Prioritised.<br>Checklist: `analysis/BRD_IEEE_29148_Checklist.xlsx` |
| 4 | **PM/PO Review & Approve** — PM/PO xác nhận nội dung. Baseline BRD trong git. |

**📄 Tài liệu tạo ra:** `BRD.md` · `interviews/*.md`
**📁 Lưu tại:** `docs/02-requirements/`

---

## 4. Phase 3 — Analysis: Phân tích yêu cầu

> Từ BRD → SRS/PRD + User Stories — yêu cầu cụ thể, đo được, kiểm thử được

| Bước | Nội dung |
|:----:|----------|
| 1 | **Phân tích BRD → Đặc tả yêu cầu** — Agent phân tích BRD, tách FR/NFR, gán mã ID, kiểm mâu thuẫn. Con người xác nhận ý nghĩa nghiệp vụ.<br>Prompt: `analysis/PRD_Prompt_IEEE_standard.md` |
| 2 | **Viết User Stories + Acceptance Criteria** — "As a [role], I want [capability], so that [benefit]". Mỗi story gắn FR-ID, có AC rõ ràng. |
| 3 | **Audit chất lượng yêu cầu** — Đối chiếu PRD checklist IEEE 29148. Mỗi yêu cầu phải: cần thiết, đơn nghĩa, đầy đủ, nhất quán, kiểm chứng được, truy vết được.<br>Checklist: `analysis/PRD_IEEE_29148_Checklist.xlsx` |
| 4 | **Traceability + Review + Baseline** — Lập ma trận truy vết BRD→SRS→US. PM/PO + Tech Lead review. Baseline trong git. |

**📄 Tài liệu tạo ra:** `SRS.md / PRD.md` · `USER_STORIES.md` · `traceability.md`
**📁 Lưu tại:** `docs/03-analysis/`

---

## 5. Phase 4 — Design: Thiết kế kiến trúc & mô hình

> SAD + Blueprint + Sơ đồ 4+1/C4 + ADR + UI/UX + Interface contracts

| Bước | Nội dung |
|:----:|----------|
| 1 | **SAD — Kiến trúc hệ thống (arc42 / IEEE 1016)** — Agent sinh SAD theo 12 mục arc42. Ghi building block CMP-xx, quyết định kiến trúc, quality attributes.<br>Prompt: `design/SAD_Prompt_IEEE_standard.md` · Checklist: `design/SAD_IEEE_1016_Checklist.xlsx` |
| 2 | **Mô hình hóa 4+1 Views** — **Logical** (class) · **Process** (sequence/activity) · **Development** (component) · **Physical** (deployment) · **Scenarios** (use case). Mỗi view có prompt + checklist UML 2.0 riêng. |
| 3 | **ADR + Blueprint + Interface + Data Model** — ≥3 ADR cho quyết định khó đảo ngược. Blueprint (IEEE 1016). OpenAPI contracts. Database design (SQL/NoSQL/Vector).<br>Prompt: `design/bluePrint_design_prompt.md`, `design/apiDesign_prompt.md`, `design/databaseDesign_*_prompt.md` |
| 4 | **UI/UX Design + Cross-view Audit + Review** — UI/UX design với personas, WCAG 2.1 AA. Chạy audit nhất quán giữa các view. Tech Lead + Architect review.<br>Prompt: `design/UI-UX-Design_prompt.md` |

**📄 Tài liệu tạo ra:** `SAD.md` · `ADR-*.md` · `blueprint.md` · `diagrams/*.drawio` · `openapi.md` · `database-design.md` · `UI_UX_design/`
**📁 Lưu tại:** `docs/04-design/`

---

## 6. Phase 5 — Planning: Lập kế hoạch thực thi

> Từ SAD + User Stories → Plan chia nhỏ thành vertical slices build được

| Bước | Nội dung |
|:----:|----------|
| 1 | **Phân rã công việc (Work Breakdown)** — Agent phân tích SDP + SAD + USER_STORIES → dựng WBS hướng deliverable, WBS dictionary và task card. Mỗi task đủ nhỏ cho agent xử lý trong vài vòng lặp.<br>Prompt: `development/TaskBreakdown_ISO_21511_Prompt.md` |
| 2 | **Xác định thứ tự, phụ thuộc, ước lượng** — Mỗi task có: owner, FR-ID, dependencies, estimate, file chạm, rủi ro. Ưu tiên vertical slice. |
| 3 | **Ghi nhận quyết định & rủi ro** — Record decisions with rationale. Ghi open risks, unknowns, gaps — mỗi item có owner. |
| 4 | **PM/PO + Tech Lead Review** — PM/PO duyệt scope & sequencing. Tech Lead duyệt technical feasibility. |

**📄 Tài liệu tạo ra:** `Software_Development_Plan.md` · `tasks/*.md`
**📁 Lưu tại:** `docs/05-development/`

---

## 7. Phase 6 — Implementation: Phát triển mã nguồn

> Mỗi User Story = một vòng SPECIFY → GENERATE → VERIFY → REFINE

| Bước | Nội dung |
|:----:|----------|
| 1 | **SPECIFY — Đọc US + AC, viết test trước** — Đọc docs/ như nguồn sự thật. AC → test case (TDD). Cấu hình AGENTS.md: stack, conventions, điều cấm. |
| 2 | **GENERATE — Code theo vertical slice** — DB → API → UI → test, mỗi slice chạy được. Commit nhỏ, Conventional Commits, gắn US/FR trong message. |
| 3 | **VERIFY — Lint · test · CI** — L0: format, lint, type check, unit test, secret scan, dependency scan, build. Tất cả deterministic. |
| 4 | **REFINE — Sửa nhỏ nhất theo phát hiện** — Lặp lại cho đến khi mọi AC xanh. Cập nhật traceability.md: US ↔ FR ↔ code ↔ test. |

**📄 Tài liệu tạo ra:** Source code (`app/`) · Tests (`tests/`) · `AGENTS.md` · `traceability.md` ↻ · ADR mới (nếu có)
**📁 Lưu tại:** `app/`, `tests/`, root repo

---

## 8. Phase 7–8 — Verify & Review: Kiểm chứng & Phê duyệt

> Tháp đảm bảo chất lượng: L0 (máy) → L1 (agent) → L2 (người) → L3–L4 (rủi ro cao)

### 🔍 Verification (Phase 7)

- **L0 — CI tự động:** lint, type, test, coverage ≥70%, secret scan, build < 10 min
- **L1 — Agent review:** review theo rubric, trích dẫn dòng lỗi, chạy trên diff, không có quyền merge
- **Test plan:** dùng `verification/testPlan_prompt.md` + `verification/Test_Plan_IEEE_829_Checklist.xlsx`
- **Code review checklist:** `verification/Code_Review_IEEE_1028_Checklist.xlsx`

### ✅ Code Review (Phase 8)

- **L2 — Human review:** 1 approver ≠ author. PR ≤ 400 dòng. Đọc diff, không đọc tóm tắt
- **Rubric 7 tiêu chí:** Đúng AC, Test, Thiết kế, An toàn, Hiệu năng, Dễ đọc, Truy vết (≥10/14 mới merge)
- **L3–L4:** Inspection cho diff rủi ro cao (auth, PII, tiền). Demo validation với stakeholder
- **Agent KHÔNG được:** approve, merge hoặc deploy

**📄 Tài liệu tạo ra:** `test-report` · `CI log` · `review-record.md` · PR + approval · coverage report
**📁 Lưu tại:** PR/work item + `docs/07-verification/`

---

## 9. Phase 9–11 — Release · Operate · Decommission

> Deploy có kiểm soát, vận hành có giám sát, nghỉ hưu có kế hoạch

### 🚀 Release (Phase 9)

- Confirm artifact = reviewed commit
- Release notes, feature flags
- Staged rollout / canary
- **Human** authorize deploy
- Monitor health indicators
- Rollback plan sẵn sàng

### ⚙️ Operate (Phase 10)

- Agent giám sát telemetry, logs
- Incident → control band → intent.md mới
- Agent KHÔNG thay đổi production
- Post-incident review
- Feed lessons → tests, docs, SOP

### 🏚 Decommission (Phase 11)

- Agent inventory dependents, data
- Verify data retention/deletion
- Revoke access & credentials
- Update diagrams & docs
- Owner sign-off retirement

**📄 Tài liệu tạo ra:** `release record` · `runbooks` · `dashboards` · `incident record` · `decommission record`
**📁 Lưu tại:** `docs/09-release/`, `docs/10-operations/`, `docs/11-decommissioning/`

---

## 10. 📋 Dòng chảy tài liệu — Toàn bộ Agentic SDLC

> Mỗi bước tạo ra artifact → artifact đó là đầu vào cho bước sau → chuỗi commit = audit trail

| Phase | 📁 Thư mục | Tài liệu (theo thứ tự) | Chuẩn / Prompt | Người duyệt |
|-------|-----------|------------------------|----------------|-------------|
| **1. Intake** | `docs/01-intake/` | `intent.md` → `glossary.md` → `stakeholders.md` → `sources.md` | AI-native SDLC model | PO |
| **2. Requirements** | `docs/02-requirements/` | `BRD.md` | IEEE 29148 · `analysis/BRD_Prompt_IEEE_standard.md` | PM/PO |
| **3. Analysis** | `docs/03-analysis/` | `SRS.md / PRD.md` → `USER_STORIES.md` → `traceability.md` | IEEE 29148 · `analysis/PRD_prompt.md` | PM/PO + Tech Lead |
| **4. Design** | `docs/04-design/` | `SAD.md` → `ADR-*.md` → `diagrams/` → `blueprint.md` → `openapi.md` → `database-design.md` → `UI_UX_design/` | IEEE 1016 · ISO 42010 · UML 2.0 · 4+1 · C4 | Architect + Tech Lead |
| **5. Planning** | `docs/05-development/` | `Software_Development_Plan.md` → `WBS.md` → `tasks/*.md` | ISO/IEC/IEEE 24748-5 · ISO 21511 · `development/DevPlan_ISO_24748_5_Prompt.md` · `development/TaskBreakdown_ISO_21511_Prompt.md` | PM/PO + Tech Lead |
| **6. Build** | code trong repo; bản ghi ở PR/work item | `AGENTS.md` → `app/` → `tests/` → `traceability.md ↻` | ISO 25010 · Conventional Commits | Human owner |
| **7. Verify** | `docs/07-verification/` | `test-report` → `CI log` → `coverage` | IEEE 829 · IEEE 29119 · `verification/testPlan_prompt.md` | QA + Reviewer |
| **8. Review** | bản ghi ở PR/work item | `PR + review record` → `approval` | IEEE 1028 · `verification/Code_Review_IEEE_1028_Checklist.xlsx` | Reviewer ≠ Author |
| **9–11. Release→Op→Retire** | `docs/09-release/`, `docs/10-operations/`, `docs/11-decommissioning/` | `release record` → `runbooks` → `incident record` → `decommission record` | ISO 12207 · ISO 9001 | Release owner |

> **⚠️ Luật bất biến:** Người/agent tạo nội dung ≠ người phê duyệt. Sau baseline, mọi thay đổi phải qua change control có bản ghi.

---

## 11. 📚 Nguồn tham khảo & Công cụ

### 🏗 Repo SDLC-Prompt-Checklist

- `requirements/BRD-Template.md`, `requirements/BRD-Template.docx` — BRD template
- `analysis/BRD_IEEE_29148_Checklist.xlsx`, `analysis/PRD_IEEE_29148_Checklist.xlsx` — IEEE 29148 checklists
- `design/` — SAD, Blueprint, UML, API, DB, UI/UX prompts + checklists
- `development/DevPlan_ISO_24748_5_Prompt.md`, `development/DevPlan_ISO_24748_5_Checklist.xlsx` — SDP prompt + ISO/IEC/IEEE 24748-5 checklist
- `verification/testPlan_prompt.md`, `verification/Test_Plan_IEEE_829_Checklist.xlsx`, `verification/Code_Review_IEEE_1028_Checklist.xlsx` — Test plan prompt + IEEE 829 checklist, Code review checklist IEEE 1028
- `AI_SDLC-SOP.md` — Quy trình SOP đầy đủ
- `agentic-sdlc-process.md` — Tài liệu này

### 📖 Chuẩn quốc tế

- **ISO/IEC/IEEE 29148** — Requirements engineering
- **ISO/IEC 25010** — Quality attributes (NFR)
- **ISO/IEC/IEEE 42010** — Architecture description
- **IEEE 1016** — Software Design Description
- **IEEE 1028** — Software reviews & audits
- **IEEE 829 / 29119** — Test documentation

### 🛠 Công cụ & Phương pháp

- **arc42** — Template SAD 12 mục
- **Kruchten 4+1** — 5 view model
- **C4 model** — 4 mức trừu tượng
- **draw.io (diagrams.net)** — Sơ đồ kiến trúc dạng `.drawio`
- **ADR (Nygard)** — Architecture Decision Records
- **ATAM-lite** — Đánh giá kiến trúc

### 🎯 Nguyên tắc then chốt

- **Artifact = audit trail** — commit chain là bằng chứng
- **Agent tạo ≠ Agent/Người duyệt**
- **Baseline trước, change control sau**
- **Deterministic trước, LLM critic sau**
- **Không có bằng chứng = chưa xong**
