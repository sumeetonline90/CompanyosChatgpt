# IVL Company OS — Proposed Architecture

**Status:** Concept for review · 20 October 2026

This document separates the architecture of the public demo from the target production system. GitHub Pages is suitable for the static demo; it is not the secure application runtime for real HR, finance, customer, or operational data. In production, the OS is an operational workspace: authorized users create and maintain records in OS-owned domains, while connected source systems remain authoritative for their assigned entities or fields.

## 1. Public demo architecture

The demo is a static client-side experience. Its mock data is bundled with the public site and must contain synthetic records only. Role selection changes the visible demo experience but does not secure data.

~~~mermaid
flowchart LR
  V[Public viewer] --> GH[GitHub Pages]
  GH --> UI[Static IVL Company OS UI]
  UI --> MOCK[Bundled synthetic data]
  UI --> LOCAL[Browser memory interactions]
  UI -. no API calls .-> SYS[IVL systems remain disconnected]
  UI -. no writes .-> OUT[No email, payment, booking, or social publishing]
~~~

## 2. Proposed production logical architecture

~~~mermaid
flowchart TB
  subgraph Users[IVL users]
    CXO[CXO / executive]
    BU[BU managers]
    FUN[Corporate function leads]
    EMP[Employees / contributors]
    ADM[System administrators]
  end

  subgraph Access[Identity and access]
    IDP[Enterprise identity provider · SSO + MFA]
    AUTH[Server-side authorization · role + BU + data classification]
    AUD[Audit trail · approvals · access events]
  end

  subgraph App[Company OS application]
    UX[Responsive web workspace]
    COCKPIT[CXO cockpit and BU scorecards]
    HR[HR, skills, capacity, learning]
    DELIVERY[Projects, tasks, milestones, timesheets]
    PRODUCT[Product idea-to-launch]
    FIN[Finance reconciliation and approvals]
    OPS[IT assets, Admin, Design, marketing]
    WF[Workflow and approval service]
    KNOW[Policy and knowledge index]
  end

  subgraph Data[Data and integration layer]
    API[API gateway / backend services]
    CONN[Connector workers and change queue]
    CANON[Canonical entity model + field ownership]
    DB[(Operational database)]
    OUTBOX[Validated change / event outbox]
    DOC[(Permission-aware document references)]
    METRICS[(Reporting store / semantic metrics)]
    MON[Freshness, errors, monitoring, reconciliation]
  end

  subgraph Sources[Systems of record and sources]
    M365[Microsoft 365 · OneDrive · SharePoint · Teams · Outlook]
    ZCRM[Zoho CRM]
    ZBOOKS[Zoho Books]
    REDMINE[Redmine PMS]
    KEKA[Keka HRMS]
    AWS[AWS accounts and cost signals]
    SOCIAL[LinkedIn · human-reviewed channel]
  end

  CXO --> IDP
  BU --> IDP
  FUN --> IDP
  EMP --> IDP
  ADM --> IDP
  IDP --> UX
  UX --> AUTH
  AUTH --> COCKPIT
  AUTH --> HR
  AUTH --> DELIVERY
  AUTH --> PRODUCT
  AUTH --> FIN
  AUTH --> OPS
  COCKPIT --> API
  HR --> WF
  DELIVERY --> WF
  PRODUCT --> WF
  FIN --> WF
  OPS --> WF
  WF --> AUD
  AUTH --> AUD
  UX -->|Create / edit / submit| API
  API -->|Validate + authorize| WF
  WF -->|Approved domain write| DB
  WF -->|Approval and change history| AUD
  DB -->|Committed event| OUTBOX
  OUTBOX --> CONN
  API --> DB
  API --> DOC
  API --> METRICS
  API --> CONN
  CONN --> M365
  CONN --> ZCRM
  CONN --> ZBOOKS
  CONN --> REDMINE
  CONN --> KEKA
  CONN --> AWS
  OPS -. approved draft only .-> SOCIAL
  CONN --> CANON
  CANON --> DB
  CANON --> METRICS
  CONN --> MON
  DB --> API
  DOC --> KNOW
  KNOW --> API
  METRICS --> COCKPIT
  MON --> COCKPIT
~~~

### Architectural responsibilities

- **Identity and authorization:** SSO/MFA plus server-side role, BU, and data-classification checks. A UI role switch is never a production authorization control.
- **Company OS application:** workflows, task views, dashboards, and approved operational actions. It should preserve links to source records.
- **Domain record ownership:** each entity and field is classified as OS-owned, source-owned, or synchronized. The OS can be the authoritative workspace for projects, tasks, milestones, skills, allocations, product lifecycle, requests, and workflow cases if IVL assigns ownership there.
- **Workflow service:** routes create/update/submit/approve/close actions, validates required fields and evidence, applies approved authority rules, and records actor, decision, and version.
- **Connector layer:** handles source-specific auth, rate limits, retries, incremental sync, field mapping, conflict queues, and errors. Outbound writes are limited to approved fields/actions; credentials stay server-side in a managed secrets store.
- **Canonical entity model:** gives common references for employee, BU, customer, opportunity, campaign, project, task, milestone, resource allocation, time entry, product idea, learning course/enrollment, invoice, asset, request, and approval while retaining source IDs and field-level ownership.
- **Change outbox:** publishes only committed, validated changes for downstream sync, avoiding partial writes and enabling retry/idempotency.
- **Reporting layer:** calculates approved, versioned metrics with source, as-of time, unit, and definition. Unknown or stale values remain visible as such.
- **Knowledge layer:** indexes metadata and permitted document references; access follows source document permissions and classification.
- **Audit and monitoring:** logs reads/writes as appropriate, approvals, integration events, freshness, reconciliation exceptions, and failed or missed runs.

### Authorization policy model

Evaluate access as **subject × resource × action × context**, with a default-deny result:

- **Subject:** authenticated user, assigned role(s), function, BU/project membership, manager relationship, and time-bound delegated authority.
- **Resource:** entity and record ID, owning function/BU/project, sensitivity class, and field-level classification.
- **Action:** discover, read summary, read detail, create, update, submit, approve, export, administer, or execute an external action.
- **Context:** record assignment, approval stage, separation-of-duties rule, source permission, location/tenant policy, and delegated approval limit.
- **Decision:** allow only the minimum action/fields and record the policy result for sensitive reads, writes, exports, approvals, and administrative changes.

Role names and proposed visibility are defined in the [User Manual](user-manual.md); testable access expectations are captured in the [Role-based User Stories](user-stories.md). The UI navigation filter is only a demo convenience and must never be reused as the production authorization mechanism.

## 3. System-of-record and flow boundaries

~~~mermaid
flowchart LR
  CRM[Zoho CRM<br/>Lead · account · opportunity] -->|Won deal · signed scope reference| OS[Company OS<br/>Create · maintain · workflow · audit]
  OS -->|OS-owned project, task, milestone updates<br/>only if approved mapping| PMS[Redmine PMS<br/>Selected synchronized fields]
  PMS -->|External task/status changes<br/>with conflict review| OS
  OS -->|Billing-ready case + evidence| FIN[Finance workspace<br/>Review · reconcile · approve]
  FIN -->|Approved invoice request / reference| BOOKS[Zoho Books<br/>Invoices · receipts · bills · ledger]
  BOOKS -->|Accounting status and balances| FIN
  HR[Company OS HR workspace<br/>Skills · allocation · appraisal cases] <-->|Employee identity and approved fields| HRMS[Keka HRMS<br/>Employee master · leave · payroll]
  M365[Microsoft 365<br/>Files · collaboration · calendar] <-->|Permission-aware links / approved actions| OS
  AWS[AWS<br/>Cloud inventory and cost signals] -->|Read-only signals| OS
  OS -->|Human-approved external communication only| HUMAN[Authorized user]
  HUMAN --> SOCIAL[LinkedIn / email / customer]
~~~

The production design should begin with users authoring OS-owned records plus read-only synchronization from existing systems. Enable outbound field sync only after IVL approves ownership and conflict rules. Any external message, payment, booking, or access change must have a documented owner, permission scope, approval rule, idempotency behavior, and audit record.

### Example: PM creates a project and milestone

1. The PM creates a project in the OS, assigns the BU, customer/account reference, project manager, signed SOW/PO reference, dates, and delivery team.
2. The PM decomposes the project into tasks and milestones, setting owners, dependencies, due dates, acceptance criteria, and (where contractually agreed) billing rules.
3. The OS stores the project plan as an OS-owned record and emits a committed change event. If approved, the connector maps selected fields to Redmine; source IDs are retained and conflicts are routed to a project data owner.
4. On milestone completion, the PM attaches required evidence and requests customer sign-off. The workflow records approver, decision, date, evidence, and project/milestone version.
5. The approved milestone creates a Finance billing-readiness case linked to the project, signed scope, and evidence. Finance checks terms, timesheets, PO, and customer acceptance.
6. Finance approves or returns the case. Invoice creation occurs in Zoho Books (or confirmed accounting system); the OS receives the invoice reference/status and updates the reconciliation view.

### Example: HR maintains people operations data

HR creates and updates OS-owned requisitions, onboarding/exit cases, skills evidence, availability, allocations, appraisal cycles, recognition, and learning assignments under HR-scoped access. Employee identity and payroll/leave fields are read from Keka or another approved master. HR-owned records link to the employee source ID; changes to source-owned fields are submitted through the approved source workflow rather than silently overwritten from the OS.

### Field ownership rules

| Ownership | Meaning | Example |
|---|---|---|
| OS-owned | Created and updated in Company OS; downstream systems receive only approved mapped fields | Project plan, tasks/milestones, resource allocation, skills evidence, approval case |
| Source-owned | External source is authoritative; OS shows a permitted projection/reference | Zoho invoice/receipt, Keka payroll field, Zoho CRM opportunity |
| Synchronized | A field has explicit write direction, owner, conflict rule, and sync status | Selected project status/date fields mirrored with Redmine |

Ownership is defined per field where multiple tools hold the same entity. Never infer authority based solely on which screen last changed.

### End-to-end integration, work, and CXO reporting flow

~~~mermaid
flowchart LR
  subgraph Sources[External sources]
    M365[Microsoft 365]
    ZOHO[Zoho CRM + Books]
    PMS[Redmine PMS]
    HRMS[Keka HRMS]
    AWS[AWS]
  end
  subgraph Entry[Company OS entry points]
    CONN[Connectors · pull / receive]
    FORMS[Role-scoped forms · create / update]
  end
  MAP[Map IDs · apply field ownership · validate]
  EXC[Exceptions · duplicates · stale / failed sync]
  QUEUES[Role queues · Sales · PM / Delivery · HR · IT · Admin · Finance · Design · Product]
  WF[Approval workflows · evidence · audit]
  STORE[(Operational records + source lineage)]
  REPORT[Reconciled reporting model · approved metric definitions]
  ACCESS[Role + BU access filtering]
  CXO[CXO cockpit · KPIs · risks · decisions]
  TRACE[Drill-through · source record · owner · as-of time]

  M365 --> CONN
  ZOHO --> CONN
  PMS --> CONN
  HRMS --> CONN
  AWS --> CONN
  CONN --> MAP
  FORMS --> MAP
  MAP -->|validated records| STORE
  MAP -->|ambiguous, stale, or invalid| EXC
  STORE --> QUEUES
  EXC --> QUEUES
  QUEUES --> WF
  WF --> STORE
  STORE -->|reconciled data| REPORT
  REPORT --> ACCESS
  ACCESS --> CXO
  CXO --> TRACE
  TRACE --> STORE
~~~

The operating principle is **source or OS entry → validated shared entity → role-owned work and approvals → reconciled reporting → access-filtered CXO view**. The CXO cockpit is not a separate manually maintained spreadsheet; it is a governed view over the same linked records employees update and teams process. Exceptions remain visible and owned rather than being silently dropped from rollups.

### CXO metric contract

Each dashboard measure needs an agreed name, definition, formula, period, currency/unit, inclusion and exclusion rules, BU mapping, target, owner, refresh expectation, and source list. The reporting layer stores the definition version and calculation timestamp. KPI drill-through preserves the viewer's permissions and shows source record IDs, reconciliation state, and last-updated/as-of timestamps. A missing, stale, or unreconciled input must be labeled and excluded or included only under an explicitly approved rule.

## 4. Cross-functional process diagrams

### Opportunity to cash

~~~mermaid
flowchart LR
  A[Lead in Zoho CRM] --> B[Qualify: segment, need, authority, timing]
  B --> C[Demo, proposal, scope and estimate]
  C --> D{Commercial / DoA approval}
  D -->|Approved| E[Signed PO + SOW]
  D -->|Needs revision| C
  E --> F[Sales order + project registration]
  F --> G[Assign team, plan milestones and timesheets]
  G --> H[Deliver and collect acceptance evidence]
  H --> I{Billing-ready check}
  I -->|Complete| J[Finance invoice in Zoho Books]
  I -->|Missing evidence| G
  J --> K[Receipt, AR follow-up and reconciliation]
  K --> L[Close project after completion and payment checks]
~~~

### Hire to deploy and exit

~~~mermaid
flowchart LR
  A[BU capacity need] --> B[HR requisition and approval]
  B --> C[Recruit, assess and offer]
  C --> D[Joiner documents and onboarding]
  D --> E[IT asset, identity and access setup]
  E --> F[Skill profile, learning and project allocation]
  F --> G[Goals, appraisal and recognition cycle]
  G --> H[Exit notice and knowledge transfer]
  H --> I[Clearance and asset return]
  I --> J[Access revocation on approved date]
  J --> K[Finance final settlement and closure]
~~~

### Product idea to launch

~~~mermaid
flowchart LR
  A[Idea or customer signal] --> B{Classify request}
  B -->|Statutory update| C[Urgency and compliance review]
  B -->|Core product| D[Product roadmap scoring]
  B -->|Customer change| E[Change request and commercial review]
  B -->|Unclear opportunity| F[Discovery / proof of concept]
  C --> G[Design, estimate and capacity]
  D --> G
  E --> G
  F --> G
  G --> H[Build and test]
  H --> I{Release gate: quality, docs, support readiness}
  I -->|Pass| J[Release and deployment plan]
  I -->|Hold| H
  J --> K[Training, sales enablement and GTM]
  K --> L[Adoption and feedback into next roadmap]
~~~

### Campaign planning to attribution

~~~mermaid
flowchart LR
  DATA[Approved audience data<br/>Zoho CRM · event registrations · customer records] --> SEG[Define segment, consent and exclusions]
  SEG --> PREVIEW[Preview audience + estimate]
  PREVIEW --> BRIEF[Campaign goal, offer, CTA, budget and assets]
  BRIEF --> REVIEW[Product / Design / Marketing review]
  REVIEW --> APPROVE{Authorized approval}
  APPROVE -->|Approved| EXEC[Human-approved channel execution]
  APPROVE -->|Revise| BRIEF
  EXEC --> RESP[Response and campaign events]
  RESP --> CRM[CRM lead source + opportunity attribution]
  CRM --> METRICS[Reconciled campaign metrics]
  METRICS --> CXO[CXO and BU dashboards]
~~~

### Learning assignment to capacity evidence

~~~mermaid
flowchart LR
  ADMIN[Learning admin adds YouTube URL + metadata] --> ASSIGN[Assign course / path to role, BU or employees]
  ASSIGN --> EMP[Employee registers / enrolls]
  EMP --> LEARN[Open video · progress · assessment]
  LEARN --> COMPLETE[Completion and certification evidence]
  COMPLETE --> SKILLS[HR skills matrix]
  SKILLS --> CAP[Capacity and project resource matching]
  CAP --> DASH[Role and CXO views]
~~~

### Purchase to pay

~~~mermaid
flowchart LR
  A[Purchase need] --> B[Budget and authority check]
  B --> C{Approved?}
  C -->|No| D[Return or reject with reason]
  C -->|Yes| E[Purchase order]
  E --> F[Goods or service receipt]
  F --> G[Invoice and PO match]
  G --> H{Exception?}
  H -->|Yes| I[Owner review and correction]
  I --> G
  H -->|No| J[Payment approval]
  J --> K[Payment execution and accounting record]
~~~

## 5. Data ownership starter matrix

This is a starting hypothesis from the reviewed process materials. Confirm entity and field ownership with each system owner before implementing synchronization.

| Entity | Likely source of record | Company OS responsibility |
|---|---|---|
| Leads, accounts, opportunities, sales activities | Zoho CRM | Portfolio view, workflow routing, source-linked summaries |
| Sales orders, invoices, receipts, vendor bills, AR/AP | Zoho Books | Reconciliation queue, milestone linkage, approvals and reporting |
| Project plan, task, milestone, time entry, delivery status | Split ownership to confirm; proposal is OS-owned plan with selected Redmine synchronization | Cross-BU portfolio, allocation, time approvals, handoff, health and billing-readiness view |
| Employee, leave, attendance, payroll inputs | Keka HRMS | Permission-aware people workflow, skills and capacity orchestration |
| Campaign brief, audience definition, approval, attribution | Company OS + Zoho CRM for lead/opportunity outcome | Campaign manager, permissioned preview, approval gates, CRM source attribution |
| Product idea, roadmap decision, stage evidence | Company OS (proposed) | Brainstorm, discovery, prioritization, release and GTM orchestration |
| Course URL, assignment, enrollment and completion | Company OS or approved LMS (to confirm) | Catalog YouTube references, assign learners, record progress and skill evidence |
| Documents and collaboration content | Microsoft 365 | Metadata, approved references, and task context |
| Cloud account and service cost/status signals | AWS | Read-only operational view and escalations |
| Appraisal, HR case, approval evidence | To confirm | Restricted process records only if source, retention, and permissions are approved |

## 6. Risks and design constraints

- Public GitHub Pages is reachable by public visitors and has no private application backend. Bundle no internal records, credentials, API keys, or real integrations.
- The reviewed SOP set includes draft documents and placeholders. Treat thresholds and process details as configurable proposals until owners approve them.
- Existing systems may overlap or have incomplete data. Establish source ownership, reconciliation, and exception handling before claiming a unified record.
- Integrations may have licensing, API, rate-limit, permission, and tenant-consent constraints. Validate these with IVL system owners.
- Employee, financial, customer, and security data require production data minimization, access control, audit, retention, and incident processes.
- Leadership dashboards can mislead if metric definitions, periods, currency units, or source freshness differ. Version metric definitions and show their provenance.
