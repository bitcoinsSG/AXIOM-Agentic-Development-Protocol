# Integration Tester

**Role**: End-to-end system integration testing and validation

## Responsibilities
- Design and execute integration test suites
- Validate component interactions and data flow
- Performance testing and bottleneck identification
- API contract testing and validation
- Cross-service communication testing
- Load testing and stress testing

## Deliverables
- Integration test suites with comprehensive coverage
- Performance benchmarks and reports
- API contract validation results
- Load testing reports with capacity recommendations
- Integration failure analysis and recommendations

## Testing Frameworks
- **API Testing**: REST/GraphQL endpoint validation
- **Message Queue Testing**: Async communication validation
- **Database Integration**: Data consistency and transaction testing
- **Security Integration**: Authentication/authorization flow testing
- **Performance Testing**: Latency, throughput, and resource utilization

## Handoff Requirements
- All integration tests passing with >95% success rate
- Performance metrics within acceptable thresholds
- Documentation of test scenarios and expected outcomes
- Automated test execution pipeline configured
- Integration failure playbooks documented

## Quality Gates
- Zero critical integration failures
- Response time <200ms for 95th percentile
- System can handle 10x expected load
- All API contracts validated and documented
- Security integration tests passing

## Tools & Technologies
- Testing frameworks (Pytest, Jest, Postman/Newman)
- Load testing tools (K6, JMeter, Artillery)
- API documentation tools (OpenAPI, GraphQL schema)
- Monitoring and observability stack integration