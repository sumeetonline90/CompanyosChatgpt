# IVL Company OS Demo

A public, static, interactive prototype for Innoval Digital Solutions. The demo uses synthetic operational records and real IVL business-unit names and publicly listed product/service lines. It is not connected to IVL systems and has no authentication or authorization layer.

## Run locally

Open `index.html` in a browser. No build step, package install, or credentials are required.

## Publish with GitHub Pages

The repository includes a GitHub Actions workflow at `.github/workflows/deploy-pages.yml`. In the repository, set **Settings → Pages → Build and deployment → Source** to **GitHub Actions**, then push to `main` or run the workflow manually from the Actions tab. The site is plain HTML, CSS, and JavaScript; `.nojekyll` prevents Jekyll processing. Project-site paths are relative so the app works under `/CompanyosChatgpt/`.

## Demo interactions

- Change the simulated viewer role and business unit.
- Start the guided walkthrough from the Overview tile to move through the CXO view, BUs, PM project planning, timesheets and allocations, Finance, HR, learning, product ideation, campaigns, integrations, and workflows.
- Navigate functional areas and inspect synthetic records.
- Search, filter, open detail drawers, progress workflow steps, create demo actions, and simulate connector states.
- Create a synthetic project with tasks and milestones and inspect its linked Finance setup check; create synthetic HR records for requisitions, skill evidence, allocations, appraisals, recognition, and onboarding/exit cases.
- Open the HR workspace to inspect the skills matrix, appraisal cycle/KRA review stages, hiring requisitions, rewards, joiner/exit cases, and project capacity allocation.
- Preview a synthetic campaign audience and simulate its review, approval, and launch; add a YouTube course, assign learners, enroll, and complete learning; promote product ideas through stage gates; record project allocations and timesheets.
- Local interactions are held in browser memory and reset when the page is reloaded.

## Planning documents

- [Product Requirements Document](docs/PRD.md) — users, product areas, journeys, access and data controls, demo acceptance criteria, phases, and open decisions.
- [Proposed Architecture](docs/architecture.md) — public demo boundary, production system context, source-of-record boundaries, and cross-functional process diagrams.
- [Operating readiness review](docs/operating-readiness-review.md) — function-by-function actions, handoffs to other teams, CXO visibility, current demo gaps, and production prerequisites.
- [User Manual](docs/user-manual.md) — proposed role visibility/responsibilities, approval boundaries, operating conventions, and cross-functional task guides.
- [Role-based User Stories](docs/user-stories.md) — prioritized requirements with acceptance criteria for each key IVL persona.

## Privacy boundary

Never add employee data, compensation, customer records, project financials, access tokens, or exports from IVL systems. All figures, people, customers, opportunities, projects, and dates in this demo are invented. Public company/product references are based on the IVL website and names provided for the prototype.
