# Senior AI and Backend Interview Preparation

This document consolidates the Spanish source note into an adaptable four-day interview-preparation outline for a senior AI and backend engineering role. It is intended to help candidates explain real work, system-design decisions, and technical leadership; it is not a verified job description, an implementation specification for JFXCMS, or evidence that any example system, transaction volume, latency, or availability target has been achieved.

Use it against the actual role description. Treat the technologies below as examples, and describe only experience and measurements you can substantiate.

## Four-day outline

### Day 1 — Production AI systems and MLOps

**Goal:** Explain how an ML model moves from experimentation into a reliable production service.

- Compare synchronous online inference, asynchronous processing, and batch scoring. Explain the choice in terms of user experience, latency budget, throughput, failure handling, and data freshness.
- Discuss service boundaries and model-serving options. The source note names FastAPI, gRPC, Kafka, RabbitMQ, Celery, ONNX Runtime, and TensorRT as examples; these are alternatives to evaluate, not a prescribed stack.
- Cover feature retrieval, caching, load balancing, horizontal scaling, model and data quality monitoring, model versioning, rollback, and operational ownership.
- Explain timeouts, retries, circuit breakers, and degraded behavior. Use a rules-based fallback only when the business and safety policy permits that decision.
- Define the measurement before discussing a performance result: workload, request rate, latency percentile, measurement window, and availability objective.

**Practice scenario:** Add fraud scoring to a payment flow with a hypothetical end-to-end latency budget of 50 ms. Treat the number as an interview constraint from the source note, not a general benchmark or a claim about a real system. Clarify which work must remain synchronous, what can run asynchronously, how the budget is divided, and what happens when a dependency is slow or unavailable.

### Day 2 — Backend, data, platform, and security

**Goal:** Demonstrate sound backend design and explain how it would be operated.

- **Python and APIs:** Review FastAPI, request and response validation with Pydantic, and separation of routing, service, and data-access responsibilities where that structure fits. Be ready to distinguish asynchronous I/O from CPU-bound model work; `async`/`await` does not by itself make CPU-heavy inference parallel.
- **PostgreSQL:** Discuss query plans, connection pooling, and choosing indexes from observed query patterns. B-tree and GIN indexes serve different access patterns; an index can also add write and storage costs.
- **Delivery and operations:** Explain containerization, CI/CD, Kubernetes readiness, liveness, and startup probes. Choose autoscaling signals that the deployed environment can actually provide; latency or accelerator metrics may require additional metric adapters or infrastructure.
- **Application security:** Cover parameterized SQL, authentication and authorization (including OAuth2/JWT where appropriate), least privilege, secret handling, and protection of personal data.
- **LLM security:** Treat prompts and retrieved content as untrusted input. Discuss layered controls, tool permissions, output handling, monitoring, and adversarial testing; input sanitization alone is not a complete prompt-injection defense.

**Practice questions:** How do you handle concurrency versus parallelism in Python? When would you consider a GIN index? How would you scale inference when each worker loads a large NLP model into memory?

### Day 3 — Low-level design and technical leadership

**Goal:** Make a design reviewable and show how you guide implementation.

For a low-level design (LLD), prepare the artifacts that best communicate the proposal:

- sequence or component diagrams;
- domain model or UML where useful;
- API contracts, such as OpenAPI;
- database schema and key indexes;
- error, timeout, retry, and idempotency behavior;
- security, privacy, observability, and test boundaries.

**Whiteboard exercise:** Design an SMS spam-classification service for a telecom operator. State assumptions about message volume, latency, data retention, and human review before choosing components. Compare an asynchronous pipeline (for example, an API, queue, workers, and database) with an online path if the use case requires an immediate decision.

For code reviews and mentoring, discuss how you assess correctness, tests, readability, database behavior, performance, maintainability, and relevant design principles such as SOLID. Give a truthful example of helping a teammate diagnose a production or integration issue, including how you made the reasoning and follow-up work clear.

### Day 4 — Generative AI, telecom examples, and English interviews

**Goal:** Explain optional differentiators clearly and communicate evidence in English.

- Review embeddings, retrieval-augmented generation (RAG), vector-search options such as Qdrant, Pinecone, or pgvector, structured model/API outputs, and evaluation of retrieval quality and unsupported answers. Frameworks named in the source note include Instructor, LangChain, and LlamaIndex; compare them only when relevant to the role.
- Telecom examples from the source note include call-detail-record (CDR) analysis, churn prediction, and customer support. Treat these as design prompts, and address lawful access, privacy, retention, and evaluation before proposing use of customer data.
- Prepare concise English answers using STAR: **Situation, Task, Action, Result**. Focus on your own decisions and verified outcomes.

Sample prompts:

1. “Can you walk us through a time you scaled an AI/ML service into production?”
2. “How do you handle technical debt while keeping up with delivery deadlines?”

The source note mentions millions of monthly transactions and 99.9% availability as interview themes. Use them only as hypothetical requirements unless you have evidence for a specific system and measurement period. Never present a target as an achieved result.

## Preparation checklist

- Prepare two truthful STAR stories: one about an AI/ML project and one about a backend bottleneck, migration, or service design. Keep only metrics you can support with logs, reports, or clear measurement context.
- Rehearse one system-design exercise, such as asynchronous text classification with an API, queue, workers, Redis, PostgreSQL, and Kubernetes. Explain why each component is needed and how the design behaves during failure.
- Review Python concurrency and parallelism, PostgreSQL B-tree versus GIN use cases, and memory-aware scaling for model-serving workers.
- For each design answer, state the requirements and assumptions first; then explain the architecture, trade-offs, failure handling, security and privacy, evaluation, and operational measures.

## Official references

These references support the technical topics above. Check the linked documentation for current behavior and version-specific details when preparing for an interview.

- [FastAPI: Concurrency and async/await](https://fastapi.tiangolo.com/async/)
- [PostgreSQL: Indexes](https://www.postgresql.org/docs/current/indexes.html) and [GIN indexes](https://www.postgresql.org/docs/current/gin.html)
- [Kubernetes: Workload autoscaling](https://kubernetes.io/docs/concepts/workloads/autoscaling/) and [container probes](https://kubernetes.io/docs/concepts/workloads/pods/probes/)
- [OWASP GenAI Security Project: LLM Top 10 (2026)](https://genai.owasp.org/resource/owasp-genai-llm-top-10-2026/)

## Source provenance

Translated and consolidated from [`docs/Este programa de capacitación.txt`](https://github.com/robotics-intelligent-systems/jfxcms/blob/25aaf1b69beb96d833c8feb3cf5b864958c532f5/docs/Este%20programa%20de%20capacitaci%C3%B3n.txt), present in source commit `25aaf1b69beb96d833c8feb3cf5b864958c532f5`.

- Original Git blob SHA-1: `71a7de1f87aaca6b712931dd5e1ea4da24ca72d5`
- Original file SHA-256: `998a2a617611aac994b76d03e9a90aad18f3e823ba64cb65906166a4137dcd60`
- Original language: Spanish
- Replacement path: `docs/senior-ai-backend-interview-preparation.md`
