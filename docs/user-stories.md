# IVL Company OS — Role-based User Stories

**Version:** Draft 0.1 · 20 October 2026  
**Status:** Proposed backlog for process-owner review. Stories describe target behavior, not a claim that the current public demo implements it.  
**Story format:** As a [role], I want [capability], so that [outcome].

## Product principles captured by these stories

- Users maintain the records their function owns; source-owned fields retain their system of record.
- Cross-functional handoffs carry linked IDs, evidence, owner, due date, status, and audit history.
- Access is granted by assigned role, BU/project scope, data classification, and delegated authority.
- CXO reporting is calculated from reconciled and permission-filtered data and can be traced to source records.
- Consequential external actions and approvals are human-authorized and auditable.

Priority guide: **P0** = secure pilot foundation / first end-to-end path; **P1** = required operating capability for an initial release; **P2** = later expansion or optimization.

## Identity, roles, and user guidance

### US-001 — Open the correct role workspace · P0

As an IVL user, I want to sign in with my company identity and see only the workspaces and records assigned to my role and scope, so that I can work without exposing unrelated or restricted information.

**Acceptance criteria**

- Given an authenticated user, when the workspace loads, then role and BU/project scope come from the identity/authorization service rather than a user-editable browser selector.
- Given a URL or record ID outside the user's scope, when the user opens it directly or through search, then the server denies access and does not return the protected record.
- Given a role change or access revocation, when the next authorized request is evaluated, then the new permissions apply and the change is audited.
- Given restricted HR or Finance fields, when a user has only summary access, then only the approved aggregate/status is returned.

### US-002 — Find role instructions · P1

As a new user, I want a User Manual organized by role and common workflows, so that I know where to enter information, what I own, and which team receives the next handoff.

**Acceptance criteria**

- The manual lists role visibility, responsibilities, approval boundaries, and links to the relevant workspaces.
- The guide explains how project/time/milestone records hand off to Finance, how HR capacity links to Projects/Learning, and how product/campaign work is reviewed.
- Demo instructions and production instructions are clearly separated; synthetic examples are identified.

### US-003 — Use records within my BU scope · P0

As a BU Manager, I want portfolio, pipeline, delivery, capacity summaries, and decisions filtered to my assigned BU, so that I can act on my business without seeing another BU's restricted information.

**Acceptance criteria**

- BU scope is enforced for search, lists, detail drawers, exports, notifications, and APIs.
- Cross-BU work remains linked but exposes only the fields permitted to the viewer.
- A delegated cross-BU owner can see and act on the specific assigned record; the delegation is time-bound and audited.

## Executive and business operations

### US-004 — Review company health and drill down · P0

As a CXO, I want company and BU KPIs with definitions, source freshness, and links to their underlying records, so that I can make decisions from reconciled information.

**Acceptance criteria**

- Each KPI shows metric definition, period, currency/unit, as-of time, data quality/freshness, and role-filtered scope.
- Selecting a KPI or exception opens the responsible work queue and source evidence without bypassing authorization.
- Stale or unreconciled inputs are flagged and excluded or clearly qualified according to the approved metric definition.
- CXO decisions create an attributable decision record with owner and due date.

### US-005 — Create and qualify an opportunity · P1

As a Sales user, I want to maintain an opportunity with account, product/service, value, stage, next action, and source, so that delivery and Finance can prepare for a valid handoff.

**Acceptance criteria**

- Opportunity data links to the Zoho CRM source ID and shows which system owns each field.
- A won opportunity cannot create a project until required customer acceptance, scope/PO reference, BU, and delivery owner are present.
- The PM receives a linked project setup task; the CRM record receives only approved synchronized fields.

## Project delivery and Finance

### US-006 — Create a project and delivery plan · P0

As a Project Manager, I want to create a project with customer, BU, scope reference, owner, tasks, dependencies, milestones, acceptance criteria, and planned billing points, so that the team can execute and Finance can reconcile progress.

**Acceptance criteria**

- Project, task, and milestone records have stable IDs, owners, dates, status, evidence, and links to customer/opportunity/source records.
- Required fields and duplicate checks are validated before the project can move to active delivery.
- Project creation creates a linked Finance setup case with the same project ID and required PO/SOW checks.
- Authorized edits are versioned; changes to dates, amount, scope, and acceptance rules retain previous values and actor.

### US-007 — Allocate delivery capacity · P1

As a PM or BU resource owner, I want to request and confirm a person/skill allocation against a project and date range, so that delivery commitments use available capacity.

**Acceptance criteria**

- Allocation shows employee ID, skill match, project/task, percentage or hours, dates, approving owner, and status.
- Over-allocation and skill gaps are flagged before confirmation.
- HR and BU owners can review the request; confirmed allocations are visible in project staffing and HR capacity views.
- Sensitive employee information is not exposed to users who only need capacity totals.

### US-008 — Submit and approve timesheets · P0

As a project contributor, I want to submit hours against an assigned project/task and period, so that my manager can validate delivery effort and Finance can use approved time for billing.

**Acceptance criteria**

- Users can submit, revise before approval, and view the status of their own time entries.
- PM approval records actor, period, project/task, billable classification, and decision.
- Approved billable time links into the Finance billing case; rejected time returns to the submitter with reason.
- Duplicate periods, missing project assignments, and out-of-policy hours are flagged.

### US-009 — Reconcile billing and receivables · P0

As a Finance Analyst, I want to reconcile project scope, PO/SOW, milestone acceptance, approved timesheets, invoice, and receipt status, so that billing and AR follow-up are accurate.

**Acceptance criteria**

- The Finance case links source IDs and shows matched, missing, stale, or conflicting fields.
- Finance can assign an exception owner, request evidence, resolve/return the case, and record an approval decision.
- Invoice and receipt status comes from the accounting source; the OS does not silently overwrite accounting data.
- Approved billing readiness updates the CXO view only after required evidence and authority checks pass.

### US-010 — Reconcile accounts payable · P1

As a Finance Analyst, I want to match vendor invoice, purchase order, receipt/acceptance, budget, and approval, so that AP exceptions are resolved before payment.

**Acceptance criteria**

- The case presents matching fields and tolerance/exception rules approved by Finance.
- A mismatch is routed to a named requestor/approver with due date and evidence request.
- Payment release requires the configured maker-checker and delegated authority; the action is audited.

## HR, learning, and workforce

### US-011 — Maintain skills with verified evidence · P0

As an HR Partner or employee, I want to maintain skills, proficiency, evidence, validation date, demand, and development action, so that staffing and learning decisions are based on current capability.

**Acceptance criteria**

- Employee-submitted evidence remains pending until the authorized reviewer validates it.
- The matrix can be filtered by skill, proficiency, BU, project demand, and evidence age.
- Skill and demand summaries can be viewed by authorized BU/resource owners; private employee notes remain restricted.
- Approved skill data can be used in allocation matching without copying restricted appraisal content.

### US-012 — Run an appraisal cycle · P1

As an HR Lead, I want to configure a review cycle with goals/KRAs, self-review, manager review, calibration, and development planning, so that performance work is completed consistently and confidentially.

**Acceptance criteria**

- Cycle dates, participants, stages, reminders, and reviewer relationships are explicit.
- Employees see only their own self-review and permitted feedback; managers see only direct reports assigned to them; HR has specifically scoped cycle access.
- Calibration and compensation information are separately permissioned.
- Each completion or reopen decision records actor, timestamp, and change history; the CXO view uses aggregated status only.

### US-013 — Manage requisition through onboarding · P1

As an HR Recruiter, I want to open a BU-approved requisition and route candidate/hiring stages into onboarding tasks, so that capacity gaps are filled and new joiners are ready to work.

**Acceptance criteria**

- Requisition includes approved role, BU, skill, budget reference, owner, and approval.
- Candidate information is restricted to assigned hiring participants and retained per policy.
- Accepted hire creates linked HR, IT, Admin, manager, and learning setup tasks with accountable owners and due dates.
- Employee master/payroll entry is completed in the designated HR system and linked by source ID.

### US-014 — Assign and complete learning · P1

As a Learning Admin, I want to create a course from an approved YouTube URL and assign it by role, BU, or named employees, so that IVL can deliver product and compliance learning.

**Acceptance criteria**

- Course title, owner, URL, skill/product tags, audience, due date, completion rule, and version are stored.
- Each employee has an independent enrollment, progress, due date, and completion record.
- Employees can register when permitted, open the course, and record completion; completion evidence is auditable.
- Completion creates pending skill evidence for manager/HR validation and updates completion reporting after validation rules.

### US-015 — Recognize contribution and manage lifecycle · P2

As an HR Partner, I want to route recognition nominations and joiner/exit cases through designated reviewers and linked functions, so that the employee experience is timely and access/assets are handled correctly.

**Acceptance criteria**

- Recognition records include contribution evidence, nominator, review decision, and allowed visibility.
- Joiner/exit cases create only the required tasks for manager, IT, Admin, and Finance; sensitive settlement details stay Finance/HR restricted.
- Asset return, knowledge transfer, access closure, and final-settlement states have independent owners and auditable completion.

## Product, marketing, and creative work

### US-016 — Move an idea through product gates · P1

As a Product Owner, I want to capture a problem, evidence, hypothesis, product, owner, and expected outcome, then advance it through discovery and roadmap gates, so that capacity is committed to validated work.

**Acceptance criteria**

- Each gate captures required evidence and a go/hold/close decision with reviewer and rationale.
- Prioritization includes impact, risk, effort, customer/regulatory urgency, and capacity.
- A selected idea can create a linked project/epic, design brief, learning need, and GTM dependency while preserving the idea ID.
- Release cannot be marked complete until validation and release approvals are recorded.

### US-017 — Create and attribute a campaign · P1

As a Campaign Manager, I want to define an audience, campaign purpose, offer, channel, approval, and CRM attribution, so that marketing execution is permissioned and its commercial outcomes can be measured.

**Acceptance criteria**

- Audience preview shows source, freshness, consent/eligibility count, and permitted fields without exposing unnecessary PII.
- Campaign brief links product/service, target segment, goal, budget approval, creative asset, owner, and attribution tag.
- A named reviewer must approve before the authorized channel connector can execute.
- Leads/opportunities reconcile back to the CRM source IDs and campaign; attribution methodology and freshness are visible on CXO reports.

### US-018 — Deliver approved creative · P2

As a Designer, I want to receive a complete brief, create a versioned asset, and route it for product/brand/legal approval, so that only approved material is used in a campaign or release.

**Acceptance criteria**

- Brief records audience, channel, product, message, owner, due date, source references, and confidentiality.
- Review comments and asset versions remain linked; approval identifies reviewer and approved version.
- Marketing/Product can use only approved deliverables; published/used state links to the originating campaign or release.

## IT, Admin, and platform operations

### US-019 — Manage assets and access requests · P1

As an IT Operations Lead, I want hardware/software custody, renewals, service requests, and access changes linked to employee/project lifecycle events, so that resources are provisioned and removed on time.

**Acceptance criteria**

- Asset has owner/custodian, serial/reference, purchase/renewal dates, status, and service history; subscription has seats, owner, cost center, renewal, and approval reference.
- Joiner, role-change, and exit cases create access/asset tasks with least privilege and due dates.
- Access provisioning or revocation is approved and audited; secrets are never stored in the Company OS.
- Cloud/cost signals link to approved AWS accounts and show source time and owner.

### US-020 — Fulfil travel and facility requests · P2

As an Admin Desk user, I want to triage travel, room, visitor, and facility requests with purpose, dates, approvals, and project context, so that employee services are fulfilled and costs can be handed to Finance.

**Acceptance criteria**

- Requester sees their own case and status; Admin sees minimum information needed to fulfil it.
- Configured manager/spend approvals occur before a booking or commitment.
- Confirmation, cancellation, vendor reference, and expense handoff are recorded; no external booking is implied until connector action succeeds.

## Integrations, workflow, and reporting controls

### US-021 — Monitor integrations and resolve sync exceptions · P0

As a System Administrator, I want connector ownership, scope, freshness, failures, mappings, and conflict queues, so that users can tell whether source data is reliable.

**Acceptance criteria**

- Connector status reflects an actual monitored job and includes last success, next attempt, source, owner, and affected records.
- Failed/ambiguous records enter a retryable exception queue; resolution is assigned and audited.
- Secrets are kept server-side; consent/scopes are least-privilege; test/synthetic connections are labeled.
- Users can distinguish a live source value from an OS-owned value and see the field-level source-of-truth rule.

### US-022 — Route a workflow decision · P0

As a process owner, I want a workflow decision bound to a specific record, authorized approver, evidence, and next owner, so that advancing a process actually advances the work.

**Acceptance criteria**

- The workflow cannot advance without the required fields/evidence and a valid actor permission.
- Approve, reject, return, delegate, and cancel decisions capture reason, actor, timestamp, version, and next step.
- The underlying business record, downstream handoff, activity feed, and reporting status update atomically or provide visible partial-failure handling.
- Templates are distinguished from active workflow instances.

### US-023 — Trust consolidated CXO measures · P0

As an executive, I want approved metrics to aggregate the same records teams maintain, with reconciliation and access rules applied, so that the cockpit is not a separately maintained report.

**Acceptance criteria**

- Metric definitions, source fields, ownership, filters, calculation version, and refresh/as-of time are governed.
- Finance and delivery measures exclude or qualify unreconciled items according to the signed-off definition.
- A drill-down respects the viewer's authorization at every step; aggregates do not reveal restricted individuals.
- Metric changes and source quality issues are visible and auditable.

## Suggested release slices

1. **Secure foundation:** US-001, US-003, US-021, US-022, US-023, audit model, source ownership, data classification.
2. **Project-to-cash pilot:** US-005 through US-010, one service BU, one project pattern, selected Redmine and Zoho mappings, Finance sign-off.
3. **People capacity pilot:** US-007, US-011 through US-015, Keka identity linking and restricted HR permissions.
4. **Product and growth:** US-016 through US-018, US-005, CRM consent/attribution policy, human-approved channel execution.
5. **Corporate services:** US-019 and US-020 with identity lifecycle, travel/facility approvals, and audit controls.

## Decisions needed from IVL owners

- Confirm named roles, reporting relationships, BU assignments, and any delegated roles.
- Define whether access should be role-based only or combined role + BU + project + classification/attribute policies.
- Confirm which employee details a BU Manager, PM, and CXO may see; confirm HR subroles for appraisal, compensation, and employee relations.
- Approve maker-checker, DoA thresholds, campaign publishing consent, project milestone acceptance, and payment-release policy.
- Select source of truth and field ownership for every entity listed in these stories.
- Confirm first release BUs, user population, compliance needs, and priority cross-functional journey.

