# Plan for the Data Engineering Learning Path

## Goal

Create a beginner-to-advanced path that begins with the repository's real Git, Python, and SQL courses, then defines the missing data engineering curriculum without pretending those specializations already exist.

## Curriculum decisions

- SQL is a core language and must be learned deeply.
- Python is the primary general-purpose implementation language.
- Git begins early, while its advanced recovery and maintenance modules return during larger projects.
- Files, schemas, data contracts, modeling, and rerunnable local pipelines come before distributed tools.
- Batch processing comes before streaming so bounded and unbounded data are not confused.
- Quality, security, lineage, observability, and cost appear throughout the path and later receive dedicated treatment.
- One cloud provider is learned deeply only after portable system concepts.
- Tool names are concrete implementations of durable concepts, not the curriculum structure itself.
- Future module counts will be based on actual concept boundaries. They will not be copied from another course.

## Existing course audit

- [x] Confirm Git teaches beginner command-line use, collaboration, recovery, hooks, tags, and repository maintenance
- [x] Confirm Python teaches files, JSON, CSV, packages, typing, tests, databases, concurrency, async I/O, logging, profiling, and security
- [x] Confirm SQL teaches relational modeling, transactions, advanced queries, migrations, PostgreSQL, access control, and tuning
- [x] Identify missing data engineering specialization boundaries

## Path document

- [x] Define an exact beginner order through existing courses
- [x] Separate available courses from planned courses
- [x] Define nine ordered specialization stages
- [x] Define later career branches without requiring every branch
- [x] Define project milestones instead of a final assessment
- [x] Add current primary documentation anchors
- [x] Add the path to repository navigation

## Completed curriculum roadmap

These curriculum areas are implemented as ordered parts of `learn-to-data-engineer` so learners follow one coherent course instead of nine disconnected folders.

- [x] Implement Data Systems Foundations
- [x] Implement Data Files, Schemas, and Contracts
- [x] Implement Warehouses and Data Modeling
- [x] Implement Ingestion, Transformation, and Analytics Engineering
- [x] Implement Workflow Orchestration
- [x] Implement Distributed Batch Processing
- [x] Implement Event and Streaming Data
- [x] Implement Data Quality, Observability, Lineage, and Governance
- [x] Implement Cloud and Data Platform Operations

Every module keeps the repository's lesson, exercise, quiz, exercise answer, and quiz answer structure. No miscellaneous module or final assessment is included.
