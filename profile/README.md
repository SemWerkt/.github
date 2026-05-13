# Semwerkt | Data

Welcome to the central GitHub organization of **Semwerkt Data Team**. As a full-service online marketing agency based in Hoorn, we deliver scalable data and e-commerce solutions where technical excellence and data-driven results are at the core of everything we do.

## About Semwerkt
Semwerkt supports organizations in translating commercial ambitions into measurable online growth. With a team of specialists in SEO, SEA, Data, and E-commerce, we build sustainable partnerships. This GitHub organization serves as the central repository for our data pipelines, Airflow DAGs, machine learning projects, and supporting custom-built solutions.

## Development Workflow & Standards
To ensure the continuity and quality of our pipelines and applications, we maintain a strict version control protocol.

### 1. Branching Strategy
* **`main`**: Contains the stable production code. For Airflow repositories this branch is the source of truth for the DAGs running on the production scheduler; for application and pipeline repositories it represents the deployed version. **Direct pushes to `main` are strictly prohibited.**
* **`feature/*`**: Branches dedicated to individual functional developments, refactors, and bug fixes. Branched from the most recent version of `main` (or `staging`, where applicable).

### 2. Repository Strategy
* Put source code in /src folder. For possible web development project via Next.js: frontend related code in /web folder, backend if not within Next.js in /src folder.
* Always write fitting README.md files in root folder to explain exactly to your collegae how your codebase operates.

### 3. Quality Assurance
* **Pull Requests**: Every code change is subject to a peer review before being merged. Reviews focus on correctness, readability, observability (logging / alerting), and impact on downstream consumers.
* **Continuous Integration**: Every pull request is monitored by Github runner, installed on the server:
  * **Unit tests** (`pytest`) for business logic and helper modules.
  * **Airflow DAG validation** for Airflow repositories — DAGs are imported in an isolated environment to catch parse errors, missing dependencies, and cyclic references before they reach the scheduler.
* **Continuous Deployment**: On a successful merge to `main`, a self-hosted GitHub Actions runner deployed on our internal server pulls the latest code, so the production environment stays in sync with the repository without manual intervention. This pattern is described in detail in the `ssh_connection_semwerkt` documentation.
* **Local Development**: Development takes place in isolated Python environments (`venv` / `uv`) and, for Airflow, against a local Airflow instance or Docker Compose setup, so changes never touch the production scheduler before review.
* **Secrets Management**: Credentials, API keys, and service-account files are **never** committed to the repository. They live in Airflow Connections / Variables, GitHub Actions Secrets, or a secrets manager — pull requests that introduce secrets are blocked at review.

## Collaboration & Roles
Within this organization, we work closely in multi-disciplinary teams:
* **Data Engineers**: Responsible for the technical architecture of our data platform — Airflow DAGs, BigQuery models, ETL/ELT pipelines, infrastructure, and CI/CD. Own the operational reliability of the pipelines.
* **Data Scientists**: Responsible for machine-learning models, statistical analyses, and turning business questions into reproducible analytical workflows. Own the methodological correctness of the models and the interpretation of results.
* **Developers**: Responsible for custom applications and integrations that complement the data platform — APIs, internal tools, automation scripts.
* **Strategists & Stakeholders**: Responsible for translating commercial questions into requirements, validating outcomes against business expectations, and functional acceptance of dashboards, reports, and model outputs.

## Contribution Guidelines
1. Create a new branch originating from the most recent version of `main` (or `staging`, where applicable).
2. Implement changes and verify them locally — run the linters, tests, and (for Airflow) a local DAG parse.
3. Open a Pull Request including a clear description of the modifications, the motivation, and any impact on downstream consumers or scheduled jobs.
4. Following technical review and successful CI checks, the change is merged. Production deployment follows automatically via the self-hosted runner.

---

## Contact & Information
**Semwerkt B.V.** Willemsweg 73, 1623 JB Hoorn  
[www.semwerkt.nl](https://www.semwerkt.nl)  
info@semwerkt.nl  

*Semwerkt – Together, we translate ambitions into measurable online growth.*
