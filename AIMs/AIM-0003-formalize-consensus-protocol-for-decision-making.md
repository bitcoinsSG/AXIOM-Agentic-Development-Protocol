# AIM-0003: Formalize Consensus Protocol

**Status:** Draft\
**Date:** 2025-08-03\
**Category:** Addition

**Background:**\
Current two-phase consensus lacks formal structure and metrics.

**Description:**\
Define pre-prepare/prepare/commit phases; instrument metrics (latency, dissent).

**Motivation:**\
Enhance reliability and observability of change approvals.

**Detailed Protocol Specification:**

### Phase 1: Pre-Prepare
- Orchestrator broadcasts proposed change with unique sequence number
- Change includes: modified files, test coverage, security analysis
- Timeout: 30 seconds for agent acknowledgment
- Required metadata: change hash, dependencies, risk assessment

### Phase 2: Prepare
- Each relevant agent validates the change against their expertise
- Agents broadcast PREPARE message with validation results
- Requires 2f+1 PREPARE messages (where f = max Byzantine agents)
- Validation includes: code quality, security, performance, compatibility

### Phase 3: Commit
- If prepare threshold met, agents broadcast COMMIT
- Orchestrator applies change after 2f+1 COMMIT messages
- Failed consensus triggers rollback and analysis
- Commit includes verification of applied changes

**Metrics Collection:**
```rust
struct ConsensusMetrics {
    proposal_id: u64,
    phase_latencies: [Duration; 3],
    agent_responses: HashMap<AgentId, ConsensusVote>,
    success: bool,
    dissent_reasons: Vec<String>,
    change_complexity: u32,
    rollback_required: bool,
}

enum ConsensusVote {
    Approve { confidence: f32, notes: String },
    Reject { reason: String, severity: RejectionSeverity },
    Abstain { reason: String },
}
```

**Impact Analysis:**

- **Dependencies:** Orchestrator messaging layer, agent communication protocols.
- **Risks & Mitigations:** Added complexity; pilot on low-risk modules first.
- **Metrics for Success:** Agreement success rate >95%, average commit latency <60s.

**Implementation Plan:**

1. Design protocol specification with formal verification
2. Implement consensus module in Orchestrator
3. Update agent communication interfaces
4. Add metrics collection and monitoring
5. Run controlled experiment on test environment
6. Gradual rollout with rollback capability

**Security Considerations:**
- Message authentication and integrity verification
- Protection against replay attacks
- Byzantine fault tolerance for up to f malicious agents
- Audit trail for all consensus decisions

**Review & Approval:**\
Security and performance agents, system architect validation required.

**Testing Requirements:**
- Unit tests for all consensus phases
- Integration tests with simulated Byzantine agents
- Performance tests under various load conditions
- Chaos engineering to test failure scenarios