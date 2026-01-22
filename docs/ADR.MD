# ADR-XXX: <Decision Title>

## Status
Proposed | Accepted | Deprecated | Superseded

---

## Context
Describe the business and technical context that led to this decision.

Include:
- Problem statement
- Constraints (performance, security, compliance, cost, timelines)
- Stakeholders involved
- Current state and pain points

Example:
> The system processes high-volume financial transactions and currently uses synchronous APIs, leading to latency and scalability concerns during peak hours.

---

## Decision
Clearly state the decision that has been made.

Include:
- What is being decided
- Scope of the decision
- What is explicitly included and excluded

Example:
> We will adopt an asynchronous processing model using message queues for non-critical transaction flows.

---

## Alternatives Considered
List all realistic alternatives that were evaluated.

For each alternative, briefly describe:
- Approach
- Pros
- Cons
- Why it was not chosen

Example:
1. **Fully synchronous REST APIs**
   - Pros: Simple, real-time responses
   - Cons: Poor scalability, tight coupling

2. **Hybrid sync + async**
   - Pros: Balanced approach
   - Cons: Increased complexity

---

## Rationale
Explain **why this decision was chosen** over others.

Include:
- Architectural principles applied
- Trade-offs accepted
- Alignment with non-functional requirements (NFRs)

Example:
> The asynchronous model improves scalability and resilience while aligning with the bank’s throughput and fault-tolerance requirements.

---

## Consequences
Describe the impact of this decision.

### Positive
- Improved scalability
- Better fault tolerance
- Reduced API latency during peak loads

### Negative
- Increased system complexity
- Need for monitoring and retry mechanisms
- Eventual consistency challenges

---

## Implementation Notes
(Optional but recommended)

Include:
- High-level implementation approach
- Key technologies or patterns
- Migration considerations

Example:
- Use Kafka for event streaming
- Implement idempotent consumers
- Introduce DLQ for failed messages

---

## Risks & Mitigations
List key risks and how they are addressed.

Example:
- **Risk:** Message loss  
  **Mitigation:** Persistent queues and retries

---

## References
(Optional)

Include:
- Architecture diagrams
- Design documents
- External references
- Jira / Confluence links (if applicable)

---
