# Plan for the Agentic AI Engineering Learning Path

## Goal

Create a beginner-to-advanced path that treats agentic AI as software and systems engineering. The path must teach model limits, tool boundaries, evaluation, permissions, human approval, security, durability, and operations before presenting large agent frameworks as shortcuts.

## Curriculum decisions

- Python is the primary implementation language for the shared path.
- SQL is required for durable application state, evaluations, retrieval metadata, and production operations.
- TypeScript and web development are optional for learners responsible for user-facing interfaces.
- Practical math and machine learning foundations come before language-model application work.
- Learners call a model directly and build a minimal agent loop before using a large orchestration framework.
- Retrieval is taught as a governed data system rather than a vector-database trick.
- Model context, durable state, and memory are separate concepts.
- Deterministic workflows are preferred when model-directed orchestration adds no value.
- Tools enforce authentication, authorization, validation, and least privilege outside the model.
- Human approval, evaluation, tracing, and durable resumption are required production boundaries.
- MCP is taught as an interoperability protocol, not as the definition of an agent.
- Provider-specific APIs stay inside named implementation lessons so the core remains portable.
- Future module counts will follow actual learning boundaries and will not be copied from another course.

## Existing course audit

- [x] Confirm Git covers safe history, collaboration, investigation, recovery, automation, and releases
- [x] Confirm Python covers packages, typing, testing, JSON, SQL, concurrency, async I/O, logging, configuration, profiling, and secure boundaries
- [x] Confirm SQL covers transactions, schemas, access control, persistent state, and performance
- [x] Confirm TypeScript and the web path can remain optional interface specializations
- [x] Identify the missing math, ML, LLM, retrieval, agent, evaluation, security, and operations boundaries

## Path document

- [x] Define an exact beginner order through existing courses
- [x] Separate available courses from planned courses
- [x] Define thirteen ordered specialization stages
- [x] Explain why multi-agent systems are optional
- [x] Define domain branches without mixing them into the shared core
- [x] Define project milestones instead of a final assessment
- [x] Add current primary documentation anchors
- [x] Add the path to repository navigation

## Completed curriculum roadmap

These curriculum areas are implemented as ordered parts of `learn-to-agentic-ai` so learners follow one coherent course before choosing an optional domain specialization.

- [x] Implement Practical Math, Data, and Experiment Skills for AI
- [x] Implement Machine Learning Foundations
- [x] Implement Neural Networks, Transformers, and Language Models
- [x] Implement HTTP, APIs, and Service Foundations
- [x] Implement LLM Application Engineering
- [x] Implement Retrieval and Knowledge Systems
- [x] Implement Agent Loops and Tool Contracts
- [x] Implement State, Memory, and Context Management
- [x] Implement Orchestration, Delegation, and Human Decisions
- [x] Implement Protocols and Interoperability
- [x] Implement Agent Security and Containment
- [x] Implement Evaluation, Tracing, and Reliability
- [x] Implement Durable Production Agents

Every module keeps the repository's lesson, exercise, quiz, exercise answer, and quiz answer structure. No miscellaneous module or final assessment is included.
