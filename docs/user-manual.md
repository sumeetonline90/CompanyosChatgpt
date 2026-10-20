# IVL Company OS — User Manual

**Version:** Draft 0.1 · 20 October 2026  
**Audience:** IVL employees, BU leaders, corporate functions, product teams, and implementation partners  
**Status:** Operating model proposal for review. The current public demo uses synthetic data and only simulates role-based navigation.

## 1. Start here

1. Sign in with your company identity in the eventual production OS. The public demo has no sign-in; choose a **Simulated viewer role** from the top bar to preview a workspace.
2. Open **User Manual** in the left navigation to see the proposed role directory, responsibilities, and cross-team task guides.
3. Use **Business Units** to scope work to one of IVL’s nine BUs when your role allows it. Corporate teams see their function queues.
4. Open a work item to inspect its owner, status, linked records, next decision, and source evidence. In production, each record should show an as-of time and source lineage.
5. Create or update information in the owning workspace. A linked handoff should carry the record ID and evidence to the next function; do not re-enter the same information in a dashboard.
6. Use the CXO Overview for approved metrics and exceptions. Drill down to the responsible record before acting.

## 2. Role-based access and responsibility

The matrix proposes default access. It is a starting point for IVL process owners and security to validate. Access should be assigned per user from identity groups and scoped by BU, project, data classification, and delegated authority. Job title alone must not grant sensitive access.

| Role | What the role sees | What the role does | Approval boundary |
|---|---|---|---|
| **CXO / Executive** | Company-wide approved scorecards, BU comparisons, high-priority exceptions, forecasts, and decision history. Detailed restricted records only when separately granted. | Review outcomes, drill into evidence, make explicitly delegated executive decisions, assign an accountable owner. | No automatic access to employee relations, compensation, credentials, or transaction-level records. No self-service edits to source-owned transactions. |
| **BU Manager** | Assigned BU portfolio, pipeline, delivery/projects, product or service work, summarized capacity and skills demand, learning coverage, and BU exceptions. | Create BU work, prioritize, resolve dependencies, propose allocation, review team progress, and submit approval requests. | View only approved people/capacity summaries; appraisal content and Finance transaction detail remain separately restricted. Approve within DoA only. |
| **Project Manager** | Assigned projects, tasks, milestones, project documents, team allocations, time entries, risks, customer acceptance, and linked Finance case status. | Create project plan, assign owners, maintain scope/tasks/dates, request staffing, validate time, attach milestone evidence, submit billing-readiness case. | Cannot approve own milestone evidence or invoice/payment; Finance owns billing reconciliation and approval. |
| **Employee / Contributor** | Own profile fields permitted by HR policy, assigned tasks, own projects, learning catalog/enrollments, own requests, own appraisal steps and submitted timesheets. | Update assigned work, submit time, maintain skills/evidence, enroll in learning, request travel/facilities/access, complete assigned reviews. | No access to another employee’s appraisal, HR case, compensation, private request, or unassigned customer/finance data. |
| **HR Lead / HR Partner** | Employee master references and restricted HR cases for assigned population; skills, capacity, requisitions, appraisal cycles, recognition, joiners/exits, learning assignments. | Maintain HR-owned workflow records, validate skill evidence, run review cycles, manage requisition and lifecycle stages, assign learning, route approvals. | Compensation and employee relations require named, narrower HR access. Separation of duties applies to sensitive outcomes. Payroll source fields remain source-owned. |
| **Finance Lead / Finance Analyst** | Approved project commercial references, PO/SOW, timesheets, milestones, billing readiness, invoices/receipts, AR, vendor bills/AP, budgets, and reconciliation evidence. | Match source records, resolve exceptions, request evidence, maintain billing/AP case status, prepare and approve transactions by delegated authority. | Maker-checker and approval limits apply. Finance does not change delivery acceptance or HR records. Payment release requires separate permission. |
| **IT Lead / IT Operations** | Hardware/software inventory, subscriptions, renewal dates, service/access requests, cloud-account/cost signals, connector health, and minimum identity attributes needed for fulfilment. | Maintain asset custody and subscription records, route/fulfil service requests, review access and renewal cases, monitor integrations. | Privileged access is time-bound and audited. No access to appraisal, compensation, customer finance, or secrets by default. |
| **Admin Lead / Admin Desk** | Travel, facility, office, room, visitor, and service requests with the minimum employee/project context needed to fulfil them. | Triage, request approvals, arrange service/booking, record confirmation, close request, and hand expenses to Finance. | Booking and spend limits follow approved delegation. No access to HR case details or financial account credentials. |
| **Product Owner / Product Manager** | Product ideas, customer/problem evidence, roadmap, product backlog, release gates, capacity dependencies, validation and GTM readiness. | Capture and score ideas, run discovery/prioritization, request design and delivery capacity, coordinate release gates, training, and launch readiness. | Product release and roadmap funding decisions follow assigned product/BU authority. Customer PII is minimized. |
| **Campaign Manager / Marketing** | Approved brand/product knowledge, permitted CRM audience segments, consent/eligibility result, campaign briefs, creative approvals, launch status, and attribution. | Define segment and goals, preview audience, create brief, request review, launch approved activity, reconcile response to CRM. | Export, email, and social publishing require consent controls and human approval. No unrestricted CRM database export. |
| **Design Lead / Designer** | Assigned briefs, approved source assets, brand library, review comments, due dates, product/campaign dependencies. | Triage creative requests, produce/revise assets, request review, record approval, hand off approved deliverables. | Access only assigned customer/company assets; publication is owned by an authorized channel role. |
| **System Administrator** | Identity/role mapping, integration health, configuration, audit and retention operations. Business data only where operationally necessary and explicitly delegated. | Configure approved role groups, connector scopes and mappings, monitor failures, route security incidents, maintain service settings. | Administrative privilege is separated from business approval. Secrets stay in managed secret storage; admin actions are audited. |

### Workspace access map

`R` = read; `W` = create/update owned records; `A` = approve within delegated authority; `—` = no default access. `Summary` means an aggregate or limited status view, not employee-level restricted detail.

| Workspace | CXO | BU Mgr | PM | Employee | HR | Finance | IT | Admin | Product | Campaign | Design | Sys Admin |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| CXO overview | R/A | Summary | Assigned | Own summary | HR summary | Finance summary | IT summary | Admin summary | Product summary | Campaign summary | Design summary | Service summary |
| Business units | R | Assigned R/W | — | — | Summary | Summary | — | — | Assigned R/W | Assigned R/W | — | — |
| Sales pipeline | R | Assigned R/W | Linked context | Assigned tasks | — | Commercial reference | — | — | Customer evidence | Assigned R/W | Brief context | — |
| Campaign Manager | R | Assigned R/A | — | — | — | Campaign billing reference | — | — | Product review | R/W/A | Assigned R/W | — |
| Finance | R/A* | Summary | Project status | Own time status | — | R/W/A | — | Expense handoff | Product budget status | Campaign budget status | — | — |
| Projects & Delivery | R | Assigned R/A | Assigned R/W | Assigned R | Capacity summary | Billing evidence R | — | Service context | Assigned R/W | — | Dependency R |
| Product Management | R | Assigned R/A | Delivery dependency | Submit feedback | Skill demand R | Budget summary | Cloud service context | — | R/W/A | GTM dependency | Design dependency | — |
| People & Capacity | Summary | Capacity summary | Assigned allocation R | Own record | R/W/A | — | Joiner minimum fields | Joiner minimum fields | Skill demand summary | — | — | — |
| Learning Hub | Summary | BU completion summary | Team learning status | Own R/W | R/W/A | — | Required training status | — | Product paths W | Sales enablement path W | Creative tools path W | — |
| IT Assets & Services | Summary | — | Project setup status | Own request | Joiner request status | — | R/W/A | — | — | — | — | Connector service view |
| Admin & Travel | Summary | Team requests summary | Project travel context | Own R/W | Joiner workflow status | Expense handoff | — | R/W/A | — | — | — | — |
| Design Studio | Summary | — | — | Assigned review R | — | — | — | — | Assigned R/A | R/A | R/W/A | — |
| Integrations / Workflows | Summary | Assigned workflow | Assigned workflow | Own workflow | HR workflows | Finance workflows | R/W/A | Admin workflows | Product workflows | Campaign workflows | Design workflows | R/W/A |

`*` CXO sees approved company-level finance reporting and only those record-level details granted by policy. This matrix is not a substitute for access-control design or a confirmed IVL authority matrix.

## 3. How the major work paths operate

### Project delivery and billing

1. The PM creates the project and records BU, customer/account reference, SOW/PO reference, owner, tasks, milestones, and planned billing points.
2. The PM requests resource allocations. HR/BU owners review capacity and confirm the assignment.
3. Contributors update assigned work and submit time against project/task and week. The PM reviews time and delivery progress.
4. The PM attaches milestone evidence and requests customer acceptance. An authorized approver records the decision.
5. The OS creates or updates the linked Finance billing-readiness case. Finance checks PO/SOW, milestone evidence, approved time, tax/commercial terms, and invoice state.
6. Finance resolves mismatches or approves the billing handoff. Accounting remains in Zoho Books or the confirmed accounting system. The CXO dashboard shows reconciled status with a drill-down to the case.

### HR capacity, skill, and learning

1. HR/BU reviews demand against the skill matrix and project forecast.
2. HR opens a requisition or proposes an existing employee allocation. The BU/PM confirms role, dates, and project need.
3. HR records skill level and evidence; employees can submit evidence for authorized review.
4. Learning admins assign a YouTube course/path to a role, BU, or employee. The employee registers and records progress/completion.
5. Course completion creates proposed skill evidence; a manager/HR reviewer validates proficiency before it is treated as confirmed capacity.
6. Appraisal goals and development plans can reference validated skills, project outcomes, and learning. Restricted performance content remains visible only to authorized participants.

### Campaign execution

1. Marketing chooses an approved source and permitted audience criteria. The system displays matched and eligible counts with source and consent context.
2. The campaign manager records audience purpose, offer, product/service, channel, budget reference, goal, and attribution tag.
3. Product and Design review content; the named approver approves the campaign.
4. An authorized channel action executes only after approval. The OS records the external campaign reference and execution result.
5. CRM responses and opportunity attribution reconcile back to the campaign. CXO metrics show source, as-of time, and contribution definition.

### Product idea to release

1. Any permitted contributor submits the problem, user, evidence/source, hypothesis, product, and expected outcome.
2. The Product Owner triages and scores the idea, gathers discovery evidence, and records a go/hold/close decision.
3. Prioritized ideas get an estimate, dependency map, capacity decision, and delivery/project reference.
4. The delivery team tracks build and validation evidence; release authority records go/no-go.
5. Product, Training, Design, and Marketing coordinate documentation, learning, release assets, and campaign readiness.

## 4. Operating conventions

- Keep one owning record and link downstream cases to it using stable IDs.
- Record a clear owner, status, next action, due date, BU/project, evidence, and source on work that crosses teams.
- Use “submitted”, “approved”, “rejected”, “returned”, or “completed” only when the designated actor and evidence are recorded.
- A workflow template step is not an approval until the underlying record captures actor, timestamp, decision, and evidence.
- Mark data source and freshness. Keep stale, missing, or conflicting data visible as an exception.
- Do not use public demo values for company decisions; all sample names, metrics, customer references, and transactions are synthetic.

## 5. Current demo limitations

The demo has no sign-in, backend, durable storage, source integrations, or server-side permissions. Role selection filters navigation only; the JavaScript and synthetic data are public. Some actions described above are future-state guidance rather than current controls. Use the [operating readiness review](operating-readiness-review.md) for module-by-module implementation status and gaps.

