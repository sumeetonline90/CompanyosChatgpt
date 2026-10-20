# IVL Company OS — Product Requirements Document

**Status:** Draft for discussion  
**Product:** Innoval Digital Solutions Company Operating System  
**Audience:** IVL leadership, BU owners, corporate function leads, design and engineering  
**Version:** 0.1 · 20 October 2026

## 1. Product summary

IVL Company OS is a role-aware operating workspace where business units and corporate functions create and maintain their operational records, run approvals, and connect work across the company. It also integrates with external systems of record and gives executives a consolidated view of the resulting work, people, financial events, knowledge, and decisions.

The first deliverable is a **public interactive concept demo** hosted as a static GitHub Pages site. It uses IVL’s business-unit names, public product/service context, and synthetic records. It does not connect to IVL systems or contain private company data. The production system is a later, separately secured product with an authenticated application, backend, data store, and governed integrations.

## 2. Problem and opportunity

IVL operates product, services, implementation, support, consulting, training, and non-SAP delivery lines. Work crosses sales, delivery, product, finance, people, and corporate operations. The source materials describe useful systems of record, but also several manual handoffs and cross-system reconciliations. Examples include order and project registration, milestone sign-off before billing, capacity and timesheet reporting, and employee joiner/leaver coordination.

The OS should make those handoffs visible, reduce management reporting effort, and provide a consistent place to understand status, ownership, decisions, and source freshness. It should complement existing systems of record rather than duplicate them without a migration plan.

## 3. Product vision and objectives

### Vision

One trusted operating view for IVL: the right role can see what needs attention, understand why, trace it to its source, and move the work through an approved process.

### Objectives

1. Give CXOs a cross-company view of commercial performance, cash, delivery, capacity, people, products, and decisions.
2. Give BU managers and function leads focused workspaces, queues, and approvals.
3. Link sales commitments to delivery plans, resource allocation, project milestones, and finance events.
4. Support HR processes across hiring, skills, allocation, appraisal, learning, recognition, and exits.
5. Manage product work from idea intake through prioritization, development, validation, release, and go-to-market.
6. Provide a visible integration and data-freshness layer across Microsoft 365, Zoho, Redmine PMS, Keka, AWS, and other approved sources.
7. Let authorized teams create and maintain records in their owned domains, with governed workflows, role-based access, source traceability, and human approvals for consequential actions.
8. Turn data from connected systems and OS workflows into role-appropriate queues and approved cross-company CXO reporting, with lineage, freshness, and reconciliation visible at each step.

### Non-goals for the public demo

- Live connections to IVL systems, real authentication, or real access control.
- Real employee, customer, vendor, payroll, project-finance, or account data.
- Sending email, publishing to LinkedIn, creating external bookings, approving payments, or writing to production systems.
- Replacing Zoho, Keka, Redmine PMS, Microsoft 365, or financial/accounting systems in the prototype.

## 4. Users and access model

| Role | Primary needs | Proposed default scope |
|---|---|---|
| CXO / executive | Company health, exceptions, forecasts, decisions, BU comparison | Approved company and BU aggregates; record-level detail only when separately granted |
| BU manager | BU pipeline, delivery, capacity summaries, risks, product/service performance | Assigned BU scope; no default access to appraisal details or finance transaction records |
| Project manager | Assigned project plan, tasks, milestones, staffing, time and billing handoff | Assigned projects and minimum related commercial evidence; submits billing case to Finance |
| Employee / contributor | Own assignments, timesheets, learning, profile evidence, and requests | Own records and assigned work only |
| HR lead / HR partner | Skills, capacity, hiring, appraisals, recognition, lifecycle and learning | Restricted population scope; appraisal, compensation, and employee-relations access split further as needed |
| Finance lead / analyst | Billing readiness, AR/AP, project finance, invoices and reconciliation | Finance records and linked project evidence; maker-checker and payment authority are separate |
| IT lead / operations | Assets, subscriptions, service/access requests, cloud and integrations | IT inventory and minimum employee details needed for fulfilment |
| Admin lead / desk | Travel, facilities, rooms, visitors and service cases | Requests and minimum employee/project context needed for fulfilment |
| Product owner | Idea intake, evidence, roadmap gates, release readiness and dependencies | Assigned products and linked delivery/GTM work |
| Campaign manager | Permitted audience, brief, creative review, approval and attribution | Approved campaign data and consent-filtered CRM segments |
| Design lead / designer | Creative briefs, assets, reviews, brand references and dependencies | Assigned briefs/assets and approved materials |
| System administrator | Identity/role mapping, connector health, configuration and audit | Platform configuration; no default business-record access |

The role selector in the public demo is a **navigation simulation**. Production access must be enforced by the server and source-system permissions, scoped by role, BU/project, data classification, and delegated authority. The proposed visibility and responsibility matrix is in the [User Manual](user-manual.md); prioritized, testable stories are in [Role-based User Stories](user-stories.md). These proposals require validation by IVL process owners and Security.

## 5. IVL operating structure

### Business units

1. Sales and Marketing
2. Product AMC
3. SAP Services
4. Products - Manoj
5. Products - Rine (Cloud)
6. Product Implementation
7. Consulting
8. Training
9. Digital (Non-SAP)

### Corporate units

HR, IT, Admin, Finance, and Design.

BU names are the user-provided working structure. Reporting ownership, cost-centre mapping, and relationships between the supplied BU list and current finance/HR structures must be confirmed before production configuration.

### Public product and service context

The demo can use public IVL product and service names, including OptiGST, OptiE-Invoice, OptiE-Invoice UAE, OptiEXIM, OptiEXIMc, Opti-Insurance, OptiSign, OptiTrack.Ai, and OptiVMS. Service examples include AMS, SAP implementation, migration and upgrades, Basis and security, BTP development, custom development, consulting, and training. Product claims and positioning should be traceable to approved public or internal collateral. [IVL website](https://www.ivldsp.com/)

## 6. Product areas and requirements

### 6.1 Executive cockpit

- Show a time-period selector, BU filter, role context, data freshness, and source links.
- Surface decisions and exceptions before trend charts.
- Include commercial, finance, delivery, capacity, people, and product indicators.
- Allow drill-down from a KPI to its underlying queue or records.
- Display current value, comparison period, target, variance, status, and data-as-of time where known.
- Distinguish confirmed source values, derived metrics, estimates, and stale or unavailable data.
- Aggregate only approved metrics from the integration and OS workflow layers; every KPI must drill through to its definition, source records, as-of time, and accountable data owner.
- Respect the viewer's role and BU scope from dashboard through every drill-down; executive access is explicitly granted and audited.

### 6.2 Business-unit portfolio

- Show all nine IVL BUs with configurable scorecards and active work.
- Allow executives to compare units and managers to focus on a permitted unit.
- Display revenue or plan metrics only when approved data and cost-centre definitions exist.
- Route shared work and dependencies to the owning function or BU.

### 6.3 Sales and marketing

- Track lead, qualification, presentation, demo, proposal, order, and handover stages.
- Require source, persona/segment, product or service line, value, expected close, owner, and dated next action for a qualified opportunity.
- Provide a campaign manager to define campaign goal, product/service, audience segment, offer, CTA, budget/approval reference, channel, owner, schedule, and target outcomes.
- Build audience previews from permissioned, approved datasets such as Zoho CRM segments, event registrations, or customer/product records; apply consent, suppression, and purpose rules before execution.
- Track campaign brief, asset review, approval, planned execution, response, lead creation/source attribution, and conversion outcomes. Link campaign-generated leads back to CRM and related opportunity records.
- Create human-reviewed drafts; sending email or publishing to LinkedIn or another external channel must require the approved connector, authorization, and final human approval.
- Hand off signed scope and payment milestones to Delivery and Finance.

### 6.4 Project and delivery management

- Let authorized PMs create and maintain projects, work breakdown/tasks, owners, dates, dependencies, risks, milestones, status, and delivery evidence in the OS.
- Associate each project with its BU, customer/account reference, signed SOW/PO, commercial terms, project manager, and source-system identifiers.
- Maintain milestone amount or billing rule, planned and actual dates, completion evidence, customer sign-off, invoice eligibility, and Finance review state.
- Track resource assignments by employee/skill, project role/task, allocation percentage, start/end dates, capacity impact, and assignment approval.
- Capture weekly timesheets by employee, project, task/milestone, date range, hours, billable status, and submission/manager approval state; link approved time to utilization and applicable Finance review.
- Link project creation and changes to approved source references, then sync or reference Redmine PMS where field ownership and write controls are agreed.
- Use the signed SOW and approved change requests as scope references.
- Make project health, utilization, milestone status, dependencies, and customer sign-offs visible.
- Support delivery patterns for SAP Services, Product Implementation, Consulting, Training, and Digital (Non-SAP).
- Require explicit approval evidence for milestone completion and billing readiness.

### 6.5 Product management

- Provide a brainstorm and idea-intake space with prompts for problem, user/customer, evidence/source, hypothesis, expected outcome, product, owner, and collaborators.
- Capture ideas from statutory changes, support tickets, implementations, sales, partner input, employee brainstorms, and market research.
- Classify requests as statutory update, core product, customer change, discovery/POC, or service work.
- Track product owner, value, urgency, affected products, effort estimate, dependencies, capacity, and decision.
- Support collaborative discussion, comments, attachments, duplicate linking, voting/scoring, and promote an idea into discovery or a formal product backlog item.
- Enforce configurable stage gates: new idea, discovery, prioritization, design/estimate, build, validation, release, and go-to-market; retain evidence, decision, owner, and next gate at each step.
- Represent on-premise SAP add-ons, SAP BTP cloud products, and non-SAP digital products.

### 6.6 HR and resource management

- Let authorized HR users maintain workforce plans, hiring requisitions, candidate stages, offers, onboarding and deployment workflows; retain employee master/payroll ownership in the approved HR system until ownership is explicitly changed.
- Maintain the OS-owned skills matrix with proficiency, evidence, learning plan, demand, and availability; link employee identity to Keka or the approved employee master.
- Match resource demand to capacity, skills, BU, project, allocation dates, and planned utilization.
- Maintain appraisal cycles, KRA/goal evidence, calibration, development plans, review status, and recognition nominations/approvals in restricted HR workflows, unless IVL assigns these to another approved system.
- Coordinate exit, knowledge transfer, clearances, asset return, account revocation, and finance settlement handoffs.
- Restrict compensation, performance, and employee relations information to specifically authorized roles.

### 6.7 Learning hub

- Organize learning paths by role, product, technology, policy, and customer-delivery need.
- Let learning admins create course records using YouTube video URLs, metadata, skill/product tags, audience, due date, and completion rule; the OS catalogs the link and does not host or copy the video.
- Allow admins to assign courses or learning paths to named employees, roles, or BUs; let employees browse the catalog, register/enroll, open course content, and record progress.
- Track completion, assessment, evidence, and certifications, and link results to the skills matrix and project capacity planning.
- Show renewal or expiry dates where relevant.

### 6.8 IT assets and internal service

- Let IT maintain the asset register, assignments, purchase/warranty dates, lifecycle, return status, support history, and software subscription owner, seat count, renewal date, and cost centre; connect to procurement/finance references as configured.
- Provide AWS account/service inventory and cost/security alert references; do not expose credentials.
- Route requests for access, hardware, software, network, support, and cloud changes through configurable approval paths.
- Log access changes and leaver revocation with timestamp, actor, and evidence.

### 6.9 Administration and Design

- Admin: create and maintain travel requests, manager approvals, booking references, itineraries, facilities, room/visitor requests, and service queue items.
- Design: creative intake, brief, brand/product owner, review rounds, approval, asset library, and delivery status.
- External bookings, publication, or payments must not occur without a confirmed production connector and appropriate approval.

### 6.10 Finance operations

- Maintain reconciliation cases and finance review states in the OS; reconcile order, signed scope, OS project, timesheet or milestone, sign-off, invoice, receipt, and outstanding AR against Zoho Books (or the confirmed accounting system).
- A PM-created milestone becomes a linked billing-readiness item only when completion and customer sign-off evidence meet the configured rule; Finance reviews it before invoice creation or sync.
- Track AP requests, budget/authority approval, purchase order, invoice match, payment preparation, and status.
- Surface mismatched identifiers, missing evidence, duplicate records, stale data, and unallocated balances for review.
- Keep payment initiation and accounting writes outside the demo; production writes require segregation of duties and audit evidence.
- Support BU reporting only after the chart of accounts, cost centres, revenue categories, and allocation rules are approved.

### 6.11 Integrations and knowledge

- Provide a connector registry with owner, purpose, status, scopes, last successful sync, record counts, and errors.
- Preserve source-system identifiers and link to the originating record/document.
- Index approved documents with version, owner, effective date, classification, and access permissions.
- Never imply that a source is connected when the demo only contains sample data.
- Feed approved source changes and OS-authored record events into role-specific queues; after validation and reconciliation, publish governed metrics to the reporting layer and CXO cockpit.
- Show connector state, last successful pull/push, data-as-of time, record counts, failed items, duplicates, mapping exceptions, and a named owner for remediation.

### 6.12 Record creation and ownership

- Every domain record has an owning function, creator, accountable owner, status, timestamps, BU/customer/project references as relevant, classification, and audit history.
- Users with the relevant role and scope can create, edit, submit, approve, and close records using validated forms and workflow gates.
- The OS is the working system of record for domains IVL assigns to it. External data is either a linked reference, a read-only projection, or a synchronized record with an explicitly named authoritative system and conflict rule.
- Create/update operations are permission-checked on the server, validated, versioned, audited, and idempotent where they trigger integration events.
- Do not silently overwrite conflicting source data. Queue conflicts and failed syncs for an identified data owner to resolve.

## 7. Core cross-functional journeys

1. **Opportunity to cash:** lead → qualification → proposal / DoA decision → signed PO and SOW → PM creates project/tasks/milestones in OS → resource assignment → milestone and timesheet sign-off → Finance billing-readiness review → invoice in accounting system → receipt and AR follow-up.
2. **Hire to deploy:** capacity need → HR creates requisition → hiring stages → offer → onboarding and IT setup → HR maintains skills and learning → project allocation → performance cycle → exit and access/asset/settlement clearance.
3. **Idea to launch:** intake → classification → prioritization → design and estimate → capacity approval → development → validation → release decision → GTM materials and training.
4. **Purchase to pay:** request → budget/authority check → approval → PO → vendor invoice → match and exception review → payment approval and accounting record.
5. **Campaign to opportunity:** approved company/product knowledge → audience and goal → brief → Design/Product review → human approval → channel activity → CRM lead source → attribution review.
6. **Travel and facilities request:** request → project/purpose context → manager approval → Admin fulfilment → itinerary or facility confirmation → expense or service closure.

## 8. Integration map

The integration strategy is a controlled data flow, not a collection of isolated dashboard widgets: approved sources and OS-authored records enter through connectors or validated forms, are mapped to common IVL entities, and route into role-owned work and approval queues. Reconciled and access-filtered records feed the reporting layer. The CXO cockpit reads the reporting layer and always links back to definitions and underlying evidence.

| Source | Likely domain | Initial production approach | Demo behavior |
|---|---|---|---|
| OneDrive / SharePoint | Documents and knowledge | Microsoft Graph, permission-aware references | Sample document inventory |
| Teams / Outlook | Collaboration, calendar, drafts | Microsoft Graph with user-delegated or approved service access | Simulated events and drafts; no messages sent |
| Zoho CRM | Leads, accounts, opportunities, activities | API/connector after field and ownership mapping | Synthetic pipeline and campaign attribution |
| Zoho Books | Orders, invoices, bills, payments, AR/AP | Accounting source; OS sends only approved invoice requests or references and reads accounting status | Synthetic milestone billing and reconciliation queues |
| Redmine PMS | Existing project/task delivery fields | OS owns its project plan by default proposal; selectively sync mapped fields after project owner and conflict rules are approved | Synthetic projects and delivery status |
| Keka HRMS | Employee master, leave, attendance, payroll interface | Approved HR connector; Keka remains source for designated employee/payroll fields; OS owns HR workflows, skills evidence, and allocations by proposal | Synthetic people and skills records |
| AWS | Account, service health, cost, access references | AWS API through a secured backend role | Connector status and synthetic account signals |
| LinkedIn | Marketing channel | Human-operated or approved platform capability | Campaign draft and analytics mock; no publishing |
| Additional systems | To be identified | Assess per owner, API, lawful purpose, and source of truth | Clearly labeled demo-only connector |

The first integration design decision is which system owns each entity and field. Avoid bidirectional sync until conflict handling, ownership, and audit requirements are agreed.

### Initial record ownership proposal

| Record/domain | Create and maintain in Company OS | External relationship / rule |
|---|---|---|
| Projects, tasks, milestones, risks, delivery approvals | PM/Delivery owns project workspace records | Link to Zoho CRM deal and signed scope; synchronize selected fields to Redmine only after field-level ownership and conflict rules are approved |
| Billing-readiness and reconciliation cases | Finance owns review case, evidence checklist, and resolution state | Zoho Books remains accounting source for invoices, receipts, vendor bills, and ledger transactions |
| Skills, capacity, allocation, appraisal, recognition workflows | HR owns these restricted operational records | Keka (or confirmed HRMS) remains employee master/payroll source unless IVL assigns otherwise |
| Hiring requisitions and onboarding/exit workflows | HR owns workflow case and approvals | Link to candidate/employee identity in the approved HR source; IT/Admin/Finance tasks are linked child work |
| Product ideas, prioritization, roadmap, release gates | Product owners own product lifecycle records | Link to support/customer inputs and source documents; downstream tickets may sync to a selected delivery tool |
| Hardware, subscriptions, IT service requests | IT owns asset/subscription inventory and service workflow | Reference purchase/accounting records and identity source; avoid secret values in the OS |
| Travel, facilities, creative requests | Admin / Design owns requests and fulfilment records | External bookings, calendar updates, and publication are gated connector actions |
| Leads, accounts, opportunities, invoices, employee master, collaboration files | Maintained in the current designated source | OS may display scoped projections and link back; ownership must be confirmed per field |

This table is a proposal for process validation, not a confirmed source-of-truth decision. A record can be authored in the OS while selected fields are synchronized to another application; designate one owner per field and define conflict behavior before enabling sync.

### Data-to-decision flow

1. **Ingest or author:** approved connector pulls or receives source data; employees also create OS-owned records through role-scoped forms.
2. **Identify and map:** preserve source IDs, resolve references to IVL employee, BU, customer, project, product, and finance entities, and mark ambiguous matches for review.
3. **Validate and reconcile:** apply field ownership, data-quality rules, duplicate checks, and source-specific freshness checks; route exceptions to a named owner.
4. **Work by role:** deliver valid records to the relevant Sales, PM/Delivery, HR, IT, Admin, Finance, Design, or Product queue with next actions and approvals.
5. **Commit and synchronize:** save approved OS-owned changes with audit history; publish mapped downstream updates through a retryable outbox where that sync is approved.
6. **Report and decide:** calculate versioned metrics from reconciled records, apply role/BU access filters, and surface exceptions, context, source links, and as-of time on the CXO dashboard.

## 9. Data, privacy, and controls

- Apply data classification: public, internal, confidential, and restricted.
- Use synthetic names, customers, figures, and records in the public demo.
- Keep employee compensation, appraisal content, employee relations, credentials, customer contracts, and non-public financial records out of the public repository and site.
- Production access must use identity federation, MFA, least privilege, separation of duties, and server-side authorization.
- Record source ID, source timestamp, sync timestamp, transformation, and action history for material data.
- Stale, failed, or incomplete data must be visible; do not silently present it as current.
- Sensitive changes require explicit human approval and a durable audit trail.
- Document retention, data residency, backup, recovery, and incident response must be decided for production.

## 10. Non-functional requirements

- Responsive layouts for desktop and tablet, with usable mobile navigation.
- Accessible keyboard navigation, visible focus, sufficient contrast, and semantic page structure.
- Fast initial load for the static demo; avoid dependence on external fonts or runtime services.
- Production should support observability, retries, idempotent ingestion, reconciliation reports, and graceful degradation when a source is unavailable.
- All user-facing dates and financial units must be explicit and consistent.

## 11. Demo acceptance criteria

- Users can navigate all major modules and see all nine named BUs and five corporate units.
- An Overview tile launches a guided, reversible step-by-step walkthrough across the CXO dashboard, BU portfolio, detailed PM workspace, Finance, HR, learning, product ideation, campaign manager, integrations, and workflows.
- A PM can create a synthetic project with tasks and milestones, and see a linked Finance setup check; an HR lead can create a synthetic HR workflow/record within the selected scope.
- The HR workspace visibly exposes skills/proficiency/evidence/demand mapping, appraisal/KRA review stages, hiring, recognition, joiner/exit workflows, and resource allocation views.
- The campaign manager can preview a synthetic audience from a selected source, require review/approval, and simulate execution without sending or publishing externally.
- Learning admins can add a YouTube URL course and assign synthetic employees; a demo employee can register and mark learning complete.
- Project delivery shows resource allocations and timesheets linked to projects; product ideas can be brainstormed and advanced through stage gates.
- The CXO experience can trace a synthetic cross-functional metric or exception to its module records and displayed source/freshness context; connector states remain explicitly simulated.
- The cockpit, BU scorecards, records, workflows, connector inventory, and detail drawers use clearly labeled synthetic data.
- The demo illustrates the six cross-functional journeys above, including approval and handoff steps.
- Search, BU filter, role-scope simulation, record inspection, local demo actions, and workflow progress controls are interactive.
- A separate User Manual area explains demo role workspaces and handoffs; a companion story backlog gives testable role-based requirements. The role picker remains explicitly labeled as simulated.
- No page claims to connect to a live source or performs an external write.
- A public viewer can distinguish current demo state from a proposed production capability.

## 12. Proposed delivery phases

1. **Concept demo:** public static site, synthetic data, IVL vocabulary, interactive navigation and flows.
2. **Process validation:** BU owners and corporate leads validate names, ownership, approvals, handoffs, dashboard questions, and unresolved policy gaps.
3. **Production foundation:** identity, tenant/security model, backend, audit, data model, deployment, and connector framework.
4. **Read-only integration pilot:** begin with a bounded set of sources and reconcile outputs with system owners.
5. **Workflow pilot:** add approvals and controlled writes only after policy, security, and segregation-of-duty review.
6. **Expansion:** additional units, learning, Admin, IT, product lifecycle, marketing, and analytics capabilities.

## 13. Open decisions before production

- Which legal entity, employee population, and office/site scope are in the first release?
- Which GitHub plan and hosting model apply to production? Public GitHub Pages is only for synthetic demo data.
- What are the authoritative BU hierarchy, cost centres, budget owners, and DoA thresholds?
- Which system is authoritative for each employee, project, milestone, customer, order, invoice, and product record?
- Who approves appraisals, hiring, purchases, discounts, credit terms, milestone sign-off, payments, and public marketing content?
- Which Microsoft 365 and Zoho licenses/APIs are enabled, and who owns connector consent and credentials?
- What are the agreed retention, privacy, audit, and data residency requirements?
- Which finance metrics and targets are approved for a CXO dashboard, and how are they calculated?
- Which operating policies in the Ver 0.1 draft SOPs have been approved, and which remain proposals?

## 14. Source basis and confidence

This PRD synthesizes the user-provided BU structure, the IVL public website, top-level IVL draft SOPs for HR, Finance, IT, Sales & Marketing, Product SDLC, Delivery, AMS, and Customer Support, plus the Professional Innoval process-agent specification and weekly MIS automation blueprint. The SOPs and several management materials are marked draft or contain placeholders. They are process references, not approval of policy or authority thresholds. Any unresolved item must be confirmed with the accountable IVL owner before production configuration.
