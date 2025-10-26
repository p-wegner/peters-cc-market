---
name: execute-prd-plan
description: Execute PRD implementation plan using parallel subagents for each development stream. Orchestrates multiple agents to work on different streams simultaneously while respecting dependencies.
arguments:
  - name: prd-file
    description: Path to the PRD file to implement
    required: true
  - name: project-name
    description: Name for the project (optional, defaults to PRD filename)
    required: false
---

# Execute PRD Implementation Plan (Parallel Subagents)

You are responsible for orchestrating the execution of a PRD implementation plan using parallel subagents. Your role is to:

1. **First**: Use the PRD-to-Implementation-Plan skill to generate the implementation plan from the PRD
2. **Then**: Launch parallel subagents for each development stream according to the plan
3. **Finally**: Coordinate execution order and dependencies

## Execution Process

### Step 1: Generate Implementation Plan
Use the PRD-to-Implementation-Plan skill on the provided PRD file to create the detailed implementation plan with all streams and dependencies.

### Step 2: Phase 1 Parallel Execution (Day 1-2)
Launch subagents IN PARALLEL using Task tool with subagent_type=parallel-subagent:parallel-worker:

## Example
#### Stream A: API Contract Design
**Agent Instructions:**
```
You are the API Contract Design specialist. Your ONLY responsibility is:
- Create OpenAPI 3.0 specification based on the PRD requirements
- Set up API mocking service (Prism, MSW, or custom solution)
- Define authentication/authorization flows
- Set up contract testing framework

IMPORTANT:
- Work ONLY on API contracts and mocking
- DO NOT implement actual API endpoints
- DO NOT work on frontend or database setup
- STOP when these tasks are complete and report back
- Focus on creating the contract specification that other teams will use
```

#### Stream B: Development Environment
**Agent Instructions:**
```
You are the Development Environment specialist. Your ONLY responsibility is:
- Create docker-compose.yml with all required services (database, auth, messaging, cache)
- Configure database schema and migrations based on PRD requirements
- Set up authentication service configuration
- Create development scripts and automation
- Set up monitoring and logging infrastructure

IMPORTANT:
- Work ONLY on environment and infrastructure setup
- DO NOT implement application logic or APIs
- DO NOT work on frontend components
- STOP when these tasks are complete and report back
- Focus on creating the foundation environment
```

#### Stream C: Project Scaffolding
**Agent Instructions:**
```
You are the Project Scaffolding specialist. Your ONLY responsibility is:
- Initialize frontend and backend project structures
- Set up package management and dependencies
- Configure CI/CD pipeline
- Set up code quality and security tools
- Create project documentation structure

IMPORTANT:
- Work ONLY on project structure and tooling
- DO NOT implement business logic or features
- DO NOT work on API implementations
- STOP when these tasks are complete and report back
- Focus on creating the project foundation
```

### Step 3: Wait for Phase 1 Completion
Wait for all three Phase 1 agents to report completion before proceeding to Phase 2. Validate that:
- API contracts are ready and mock service is working
- Development environment is fully configured
- Project scaffolding is complete

### Step 4: Phase 2 Parallel Execution (Day 2-5)
After Phase 1 is complete, launch these three subagents IN PARALLEL:

#### Stream D: Backend Implementation
**Agent Instructions:**
```
You are the Backend Implementation specialist. Your ONLY responsibility is:
- Implement REST APIs exactly matching the OpenAPI specification created in Phase 1
- Add authentication middleware based on the auth flows defined in Phase 1
- Implement business logic based on PRD requirements
- Create database repositories and models using the schema from Phase 1

IMPORTANT:
- Follow the API contract EXACTLY as specified in the OpenAPI doc
- Work ONLY on backend implementation
- DO NOT work on frontend components
- DO NOT modify the API contracts - implement them as-is
- STOP when these tasks are complete and report back
```

#### Stream E: Frontend Implementation
**Agent Instructions:**
```
You are the Frontend Implementation specialist. Your ONLY responsibility is:
- Build UI components for all API endpoints defined in the OpenAPI specification
- Implement authentication UI and state management based on auth flows
- Connect frontend to the mock API service from Phase 1
- Add form validation and error handling

IMPORTANT:
- Use the mock API service during development
- Work ONLY on frontend implementation
- DO NOT modify backend APIs
- DO NOT work on testing framework setup
- STOP when these tasks are complete and report back
```

#### Stream F: Testing Framework
**Agent Instructions:**
```
You are the Testing Framework specialist. Your ONLY responsibility is:
- Create E2E test framework setup
- Write E2E tests for all PRD requirements
- Set up API contract testing against the OpenAPI specification
- Configure performance and security testing
- Set up visual regression testing if applicable

IMPORTANT:
- Work ONLY on testing infrastructure and test cases
- DO NOT implement application features
- DO NOT modify APIs or frontend components
- STOP when these tasks are complete and report back
- Focus on comprehensive test coverage
```


## Key Requirements

### For Each Subagent:
- **Scoped Responsibility**: Each agent works ONLY on their assigned stream
- **Clear Boundaries**: No overlap between agent responsibilities
- **Stop When Done**: Agents stop when their specific tasks are complete
- **Report Completion**: Each agent reports back when finished

### For Orchestration:
- **Respect Dependencies**: Phase 2 cannot start until Phase 1 is complete
- **Parallel Execution**: Run agents in parallel within each phase
- **Integration Points**: Coordinate handoffs between phases
