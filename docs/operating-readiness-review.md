# Company OS operating-readiness review

**Review date:** 20 October 2026  
**Scope:** Current GitHub Pages prototype, its available actions, cross-module handoffs, and the CXO overview.  
**Verdict:** Useful as an interactive concept demo. It is not yet an operating system people can use for company work: browser state is temporary, permissions are simulated, most source connections are examples, and several function screens are still read-only mock queues.

## What the review means

- **Usable in demo:** A user can perform the described action in the browser and see its local result.
- **Partial:** Some records or stages are interactive, but the complete function workflow is not implemented.
- **Illustrative:** The screen communicates a planned capability; its records, metrics, or controls do not implement the business process.
- **Production prerequisite:** Work needed before real employee, customer, finance, or system data can be used.

All actions listed as usable are synthetic and held in browser memory. Refreshing the page clears them. The static site makes no API calls and writes to no IVL system.

## Function-by-function review

| Function | What a role can do in the demo | Inter-module handoff and CXO visibility | Readiness |
|---|---|---|---|
| CXO overview | Review illustrative revenue, pipeline, delivery, and capacity KPIs; filter the portfolio; open exceptions; see session-local counts and recent activity. | Newly created projects, Finance handoffs, HR records, learning completions, and campaign launches appear in the session rollup/activity. Created review items can enter the exception list. Seed KPIs and chart remain fixed sample figures, and seed exceptions are sample records. | Partial |
| Business units | Compare nine IVL BUs and select a unit to filter work. | BU is carried on created project, HR, and other demo records. The scorecards themselves are fixed illustrative data and do not calculate from the records. | Illustrative |
| Sales pipeline | Inspect synthetic opportunities/tasks and create a generic local item. | Campaign manager is now directly reachable from navigation. Campaign launch is visible to CXO, but does not create a CRM lead/opportunity or attribution result. Sales records do not have a dedicated opportunity capture, qualification, proposal, or order workflow. | Illustrative |
| Campaign manager | Preview a synthetic audience; submit for simulated review; approve; simulate launch. | A launch is saved as a Marketing record and appears in CXO activity. The source count is fixed synthetic data; consent checks are explanatory; no email or LinkedIn action is sent; CRM attribution is pending and not calculated. | Partial |
| Finance | Inspect a synthetic milestone-to-invoice queue and add a generic demo item. Creating a project generates a linked Finance setup check. Submitting project time creates a Finance review item. | Project ID and timesheet handoff are carried into Finance records and CXO review/activity. No actual AR/AP reconciliation, invoice/receipt/bill matching, payment action, milestone approval, or financial rollup is implemented. Existing Finance rows are seed data. | Partial |
| Projects & delivery | Create a project with customer/account, BU, PM, scope reference, and initial tasks/milestones; add resource allocations; submit timesheets. | Project creation queues a Finance setup check. Timesheets link to a project/task and create a Finance review handoff. The project and finance items are visible in their queues and CXO activity/exception rollup. Task and milestone text are captured in project detail, but are not separate editable or approvable records. | Partial |
| HR & people | Inspect skills, appraisal/KRA, requisition, recognition, joiner/exit, and capacity tables. Create HR workflow records; skill evidence appears in the skills matrix; allocation data is shared with Projects. Learning completion creates skill evidence marked for HR review. | HR-created items appear in HR queue and CXO session activity. Hiring, appraisal, recognition, and lifecycle records created through the generic HR form do not yet populate or advance their corresponding detail tables. Workforce and appraisal KPIs are fixed. | Partial |
| Learning hub | Add a YouTube course, select an audience/assignees, register, open the URL, and mark completion. | Completion creates HR skill evidence pending manager validation and is visible in CXO activity/rollup. Enrollment is only a small local demo state: it does not track multiple employees independently per course correctly, validate attendance, or calculate actual completion rates. | Partial |
| Product management | Capture an idea with source, product, problem/evidence, and owner; advance the idea through named stages. | Stage changes appear in CXO activity. The product delivery board is still seeded; advancing an idea does not create a project, allocate a team, trigger release approval, or launch a GTM campaign. | Partial |
| IT assets & services | Inspect synthetic hardware, subscription, cloud, and service rows; create a generic local item. | Seed renewal and cloud items appear as CXO exceptions. No asset assignment/return, access provisioning, subscription approval/renewal, service desk lifecycle, or AWS account action is executable. | Illustrative |
| Admin & travel | Inspect synthetic travel, facilities, and room records; create a generic local item. | Admin records do not yet route for manager approval, book travel/rooms, capture expense handoff, or update CXO from completed work. | Illustrative |
| Design | Inspect creative requests and create a generic local item. | Product and campaign seed rows mention design as a dependency, but no request intake, asset review/approval, versioning, or release handoff is implemented. | Illustrative |
| Workflows & approvals | Open seven sample templates and advance each template’s displayed step. | The step counter is independent of the underlying project, HR, campaign, Finance, or travel record. It does not assign a person, enforce a decision, store evidence, or update CXO queues. | Illustrative |
| Integrations | Inspect the proposed connector inventory and simulated statuses for Microsoft 365, OneDrive, SharePoint, Teams, Outlook, Zoho CRM/Books, Redmine PMS, AWS, LinkedIn, and Keka. | Connector cards explain intended source coverage, but the page has zero credentials, OAuth, API calls, sync jobs, mapping, freshness measurements, retry handling, or conflict resolution. | Illustrative |

## Cross-functional paths that work in this prototype

1. **Project setup → Finance:** Create a project, then open Finance and inspect its generated setup check. It carries the project ID and asks Finance to confirm PO/SOW, billing terms, and milestone schedule.
2. **Timesheet → Finance:** Submit project time. A Finance review record is generated with the project, task, hours, and week.
3. **Learning → HR:** Complete a course. The HR skills matrix receives evidence with a pending manager-validation level.
4. **Campaign → CXO:** Simulate an approved launch. The launch appears in the Marketing queue and the CXO activity/launch count.
5. **Product idea → CXO:** Advance an idea. The new stage appears in recent activity.
6. **Created records → CXO:** Session activity, counts, and some pending review records surface in Overview. The main financial/delivery KPIs do not recalculate.

These are local front-end demonstrations of the intended links. They do not provide durable records, authoritative approvals, or system integration.

## Gaps to close before calling the demo “operable”

### Demo-level gaps

1. Give Sales, Finance, HR, IT, Admin, Design, and workflow queues purpose-built forms and actions. Generic “create item” currently records too little for a real handoff.
2. Turn tasks and milestones into separate project records with owners, dates, completion evidence, approval status, and Finance billing gates.
3. Add Finance reconciliation actions for AR, AP, PO/SOW, invoices, receipts, timesheets, and project milestones, with explicit matched/unmatched states and exception ownership.
4. Make HR create/update actions feed the corresponding skill, appraisal, hiring, recognition, and lifecycle tables, with role-appropriate stages and review decisions.
5. Track each employee’s enrollment separately per course; make assignment, due date, progress, completion, and skill validation visible to the learner and HR.
6. Link product stage gates to delivery project creation, capacity allocation, release readiness, and campaign/GTM work.
7. Bind approval steps to records and decisions. A template progress control must not stand in for record approval.
8. Calculate CXO metrics from governed operational records, with definitions, period/BU filters, permissions, freshness, and drill-downs to the source records. Keep the existing sample company figures visibly labelled as seed data until that exists.
9. Add a demo reset and local persistence choice. Current session data disappears on refresh.

### Production prerequisites

- Authenticated identity and server-enforced role, BU, and sensitive-field authorization. The current role picker is a visual simulation and offers no security.
- Backend APIs, durable database, audit log, record versioning, validation, and retention/deletion rules.
- Approved source-of-record ownership for each field; API scopes, licensing, data mapping, sync direction/frequency, conflict handling, retries, and monitoring for each external connector.
- HR privacy boundaries for appraisal/performance data; Finance maker-checker and accounting controls; marketing consent/purpose controls; IT least-privilege and credential handling.
- Metric definitions and reconciliation controls so the CXO dashboard only reports approved, fresh, permission-filtered values.
- Operational workflows and authority thresholds confirmed by IVL policy owners.

## Suggested build order

1. Define identity, role/BU access, core records, audit history, and system-of-record boundaries.
2. Complete one end-to-end value path: opportunity/order → project/tasks/milestones → time and sign-off → Finance reconciliation → CXO drill-down.
3. Complete HR capacity: skill evidence → demand/requisition → allocation → learning → appraisal/lifecycle permissions.
4. Complete product and campaign paths with human approval and traceable outcomes.
5. Add IT/Admin/Design workflows and approved integrations in priority order.
6. Replace sample CXO KPIs with governed data products and test each drill-down against source records.

## Verification performed

- Reviewed the module navigation, screens, state mutations, form submit handlers, table/detail lookups, inter-module references, walkthrough, connector inventory, and CXO render path in `app.js`.
- Checked JavaScript parsing with `node --check app.js` and whitespace with `git diff --check` after the local interaction changes.
- Attempted to open a local HTTP preview in the in-app browser; its browser environment timed out connecting to the local server, so visual/browser interaction QA remains outstanding.

