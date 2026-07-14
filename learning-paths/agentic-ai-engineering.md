# Agentic AI Engineering Learning Path

This path is for a complete beginner who wants to build AI applications that can reason over context, choose tools, take controlled actions, pause for approval, recover from failure, and provide evidence about what happened.

An agentic AI engineer is primarily a software and systems engineer. Calling a model in a loop is only the beginning. Reliable work also requires data handling, runtime validation, permissions, evaluation, observability, security, cost control, and clear limits on autonomy.

## What is available now

The repository already provides useful shared foundations:

- [Git](../learn-to-git/README.md) teaches safe history, collaboration, automation, investigation, and recovery.
- [Python](../learn-to-python/README.md) teaches programming, packages, types, testing, JSON, databases, asynchronous I/O, logging, configuration, profiling, and secure boundaries.
- [SQL](../learn-to-sql/README.md) teaches durable relational state, transactions, schemas, querying, access control, and performance.
- [TypeScript](../learn-to-typescript/README.md) and the [Web Development path](web-development.md) are optional when you want to build a browser interface for an agent product.
- [Agentic AI Engineering](../learn-to-agentic-ai/README.md) contains 52 ordered modules implementing the complete AI and agent sequence below.

Complete the shared foundations in the beginner order, then enter the Agentic AI course. Domain specializations remain optional later branches.

## Beginner order

Follow this order if you have never programmed:

1. Complete Git Modules 01 through 13 so every experiment has safe history.
2. Complete Python Modules 01 through 32. Python is the primary implementation language for this path.
3. Complete SQL Modules 01 through 23 before reaching Python's database module.
4. Complete Python Modules 33 through 38. You can now connect Python and SQL without meeting unexplained database concepts.
5. Complete SQL Modules 24 through 34 before operating persistent agent state, evaluation stores, or retrieval systems in production.
6. Return to the remaining Git modules while projects become larger and collaborative.
7. Learn TypeScript and the web path only if your role includes building the user-facing application. They are not prerequisites for the Python agent curriculum.

Using an AI coding assistant does not replace these foundations. You need enough programming knowledge to review generated code, recognize unsafe tool access, test failure paths, and debug behavior the model cannot explain reliably.

## Agentic AI course sequence

The stages below are implemented in [Learn Agentic AI Engineering](../learn-to-agentic-ai/README.md).

### Stage 1: Practical Math, Data, and Experiment Skills for AI

Learn vectors, matrices, probability, distributions, sampling, averages, variance, similarity, ranking metrics, uncertainty, train and validation splits, data leakage, baselines, and reproducible experiments. Use NumPy and pandas only after the underlying idea is clear.

The goal is not research-level mathematics. The goal is to understand model inputs, outputs, evaluation results, and tradeoffs without treating metrics as magic.

### Stage 2: Machine Learning Foundations

Learn problem framing, features, labels, regression, classification, loss, gradient descent, overfitting, regularization, embeddings, evaluation metrics, dataset shift, fairness, and production inference boundaries.

You should be able to decide when ordinary rules, search, or a smaller model is better than a large language model.

### Stage 3: Neural Networks, Transformers, and Language Models

Learn tensors, neural network layers, backpropagation, tokenization, embeddings, attention, transformer structure, pretraining, instruction tuning, context windows, decoding, hallucination, model limits, latency, and inference cost.

Training a frontier model is not required. You do need a correct mental model of why outputs are probabilistic and why fluent text is not proof.

### Stage 4: HTTP, APIs, and Service Foundations

Learn clients and servers, URLs, DNS, TLS, HTTP methods, headers, status codes, JSON contracts, authentication, authorization, rate limits, retries, timeouts, idempotency, webhooks, streaming responses, and safe secret handling.

You should be able to build and test a small typed API client and server without a model. Model providers, tool servers, retrieval services, and agent applications all rely on these boundaries.

### Stage 5: LLM Application Engineering

Call a model through a small direct API integration before adding an agent framework. Learn messages, instructions, structured outputs, streaming, retries, rate limits, timeouts, cancellation, model selection, secrets, content handling, caching, and cost measurement.

Every response should cross a runtime validation boundary. A type annotation alone cannot prove that model output follows the requested schema.

### Stage 6: Retrieval and Knowledge Systems

Learn document ingestion, parsing, chunking, metadata, embeddings, vector search, keyword search, hybrid retrieval, reranking, citations, access filtering, freshness, deletion, and retrieval evaluation.

Retrieval-augmented generation is a data system. It needs source ownership, permissions, update behavior, and evaluation, not only a vector database.

### Stage 7: Agent Loops and Tool Contracts

Build a minimal agent loop yourself. Learn termination conditions, maximum turns, tool selection, JSON Schema, argument validation, tool results, retries, idempotency, side effects, error recovery, and deterministic workflow steps.

Tool descriptions are not security controls. Each tool must validate input, authenticate the caller, enforce authorization, limit its capabilities, and return a stable result contract.

### Stage 8: State, Memory, and Context Management

Separate the current model context from durable application state. Learn conversation history, summaries, working state, user preferences, retrieval memory, expiry, versioning, privacy, deletion, tenant isolation, and context-budget decisions.

Do not store every message forever or let model-written memory become trusted fact without validation.

### Stage 9: Orchestration, Delegation, and Human Decisions

Compare deterministic workflows, one agent with tools, manager-style delegation, handoffs, and multiple collaborating agents. Learn when extra agents add value and when they only add latency, cost, and new failure paths.

Sensitive or irreversible actions must support pause, inspection, approval or rejection, durable resumption, and an audit record. Human approval should occur before the side effect, not after it.

### Stage 10: Protocols and Interoperability

Learn HTTP and JSON-RPC boundaries, then study the Model Context Protocol host, client, and server roles. Cover capability negotiation, tools, resources, prompts, transports, authorization, version compatibility, timeouts, and untrusted remote servers.

MCP provides a context exchange protocol. It does not decide how an application should reason, authorize business actions, or manage model context.

### Stage 11: Agent Security and Containment

Study direct and indirect prompt injection, data exfiltration, excessive agency, confused-deputy problems, unsafe output handling, poisoned memory, malicious tools, supply-chain risk, sandbox escape, denial of service, and secret leakage.

Apply least privilege, allowlisted operations, scoped credentials, isolated execution, network restrictions, resource limits, approval gates, output validation, audit logs, and safe failure defaults. Guardrails can add checks, but they do not replace authorization and containment.

### Stage 12: Evaluation, Tracing, and Reliability

Create versioned evaluation datasets and define success before tuning prompts. Test task completion, tool choice, tool arguments, groundedness, citation quality, refusal, safety, latency, cost, recovery, and behavior across model changes.

Record structured traces for model calls, tool calls, handoffs, approvals, failures, and usage while excluding secrets and unnecessary personal data. A demo that worked once is not evaluation evidence.

### Stage 13: Durable Production Agents

Learn queues, workers, checkpoints, resumable state, concurrency, rate limiting, model and prompt versioning, feature flags, deployment, monitoring, incident response, rollback, data retention, and provider failure plans.

Long-running work must survive a process restart without repeating an irreversible action. Production design should allow models, providers, and frameworks to change without rewriting every business rule.

## Choose a later focus

After the shared sequence, choose a domain:

- **Coding agents:** Repository understanding, isolated workspaces, patch review, test execution, and supply-chain controls.
- **Data agents:** Governed SQL tools, semantic models, query limits, result validation, and auditable analysis.
- **Research and knowledge agents:** Source discovery, retrieval, citations, freshness, synthesis, and claim evaluation.
- **Business workflow agents:** Durable approvals, case state, integrations, permissions, and deterministic business rules.
- **Voice and multimodal agents:** Realtime transport, interruption, audio and image inputs, latency, consent, and fallback behavior.
- **Private and local AI systems:** Model serving, hardware limits, quantization, privacy, model evaluation, and update operations.

These are optional branches. Multi-agent architecture is not an automatic advanced level and is not required for every product.

## Project milestones

Progress should come from several increasingly responsible projects:

1. Build a typed command-line model client with structured output, retries, timeouts, logging, and a small evaluation set.
2. Build a retrieval application that cites permitted sources and measures retrieval and answer quality separately.
3. Build one agent with two read-only tools, explicit turn limits, invalid-argument recovery, and traces.
4. Add one side-effecting tool with least privilege, idempotency, human approval, audit history, and a tested rejection path.
5. Expose a limited capability through an authenticated MCP server and test it with an untrusted client input.
6. Deploy a durable agent workflow that can pause, restart, resume, change model versions, and avoid repeating completed side effects.

There is no miscellaneous stage and no final assessment.

## Accuracy anchors for future modules

Future modules should use current primary sources and keep provider-specific APIs inside clearly named implementation lessons:

- [Google Machine Learning Crash Course](https://developers.google.com/machine-learning/crash-course/)
- [PyTorch beginner tutorials](https://docs.pytorch.org/tutorials/beginner/basics/intro)
- [OpenAI Agents SDK documentation](https://openai.github.io/openai-agents-python/)
- [Model Context Protocol architecture](https://modelcontextprotocol.io/docs/learn/architecture)
- [Model Context Protocol security guidance](https://modelcontextprotocol.io/docs/tutorials/security/security_best_practices)
- [NIST AI Risk Management Framework](https://www.nist.gov/itl/ai-risk-management-framework)
- [OWASP Top 10 for LLM and Generative AI applications](https://genai.owasp.org/initiatives/top-10-for-llm-and-genai/)
