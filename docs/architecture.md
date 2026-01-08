# iQueue Architecture

**Technical architecture for democratized research infrastructure**

-----

## System Overview

iQueue is a multi-layered platform connecting:

- **Users** (mobile app) → hypothesis submission
- **AI Layer** (Claude/GPT APIs) → methodology guidance
- **Compute Layer** (cloud infrastructure) → simulation execution
- **Validation Layer** (automated quality control) → results verification
- **Publishing Layer** (GitHub-style repos) → distribution

```
┌─────────────────────────────────────────────────────────┐
│                     MOBILE APP                          │
│              (React Native - iOS/Android)               │
└─────────────────────────────────────────────────────────┘
                          ↓↑
┌─────────────────────────────────────────────────────────┐
│                    API GATEWAY                          │
│              (REST API + WebSocket)                     │
└─────────────────────────────────────────────────────────┘
                          ↓↑
        ┌─────────────────┼─────────────────┐
        ↓                 ↓                 ↓
┌──────────────┐  ┌──────────────┐  ┌──────────────┐
│  AI GUIDANCE │  │   SIMULATION │  │  VALIDATION  │
│    LAYER     │  │     LAYER    │  │    LAYER     │
└──────────────┘  └──────────────┘  └──────────────┘
        ↓                 ↓                 ↓
┌─────────────────────────────────────────────────────────┐
│                  DATA PERSISTENCE                       │
│         (PostgreSQL + S3 + Git Backend)                │
└─────────────────────────────────────────────────────────┘
```

-----

## Layer 1: Mobile Application

### Technology Stack

- **Framework:** React Native
- **State Management:** Redux Toolkit
- **Offline Support:** Redux Persist + Local SQLite
- **Real-time Updates:** WebSocket connection
- **Authentication:** OAuth 2.0 (Google, Apple, GitHub)

### Core Screens

**1. Hypothesis Submission**

- Natural language input
- AI-assisted refinement
- Voice input option
- Markdown support for equations

**2. Methodology Wizard**

- Step-by-step quality gate progression
- Visual progress indicator
- AI suggestions for each gate
- Can’t skip steps (enforced progression)

**3. Simulation Queue**

- List of queued/running/completed simulations
- Real-time progress updates
- Estimated completion times
- Cancel/modify before execution

**4. Results Dashboard**

- Pass/fail visualization
- Interactive charts/graphs
- Provenance inspection
- Share/export options

**5. Community**

- Discover public hypotheses
- Follow researchers
- Comment/discuss results
- Leaderboards (optional gamification)

### Offline Capabilities

- Draft hypotheses offline
- Queue simulations when online
- Cached results viewing
- Sync when connection restored

-----

## Layer 2: API Gateway

### Technology Stack

- **Framework:** Node.js + Express
- **API Style:** REST + GraphQL
- **Real-time:** Socket.io for WebSockets
- **Rate Limiting:** Redis-based
- **Caching:** Redis
- **Authentication:** JWT tokens

### Core Endpoints

**Hypothesis Management:**

```
POST   /api/v1/hypotheses          # Create hypothesis
GET    /api/v1/hypotheses/:id      # Get hypothesis
PUT    /api/v1/hypotheses/:id      # Update (draft only)
DELETE /api/v1/hypotheses/:id      # Delete (draft only)
```

**Methodology:**

```
POST   /api/v1/hypotheses/:id/validate   # Run quality gates
POST   /api/v1/hypotheses/:id/preregister # Lock methodology
GET    /api/v1/hypotheses/:id/gates       # Get gate status
```

**Simulation:**

```
POST   /api/v1/simulations         # Queue simulation
GET    /api/v1/simulations/:id     # Get status
GET    /api/v1/simulations/:id/logs # Stream logs (SSE)
DELETE /api/v1/simulations/:id     # Cancel simulation
```

**Results:**

```
GET    /api/v1/results/:id         # Get results
GET    /api/v1/results/:id/provenance # Get full provenance
POST   /api/v1/results/:id/publish # Publish to repo
```

**AI Assistance:**

```
POST   /api/v1/ai/refine           # Refine hypothesis
POST   /api/v1/ai/suggest          # Suggest methodology
POST   /api/v1/ai/critique         # Productive skepticism
```

### WebSocket Events

```javascript
// Client → Server
{
  type: 'SUBSCRIBE_SIMULATION',
  simulationId: 'sim_123'
}

// Server → Client
{
  type: 'SIMULATION_PROGRESS',
  simulationId: 'sim_123',
  progress: 0.45,
  status: 'running',
  estimatedCompletion: '2026-01-08T14:30:00Z'
}
```

-----

## Layer 3: AI Guidance Layer

### Technology Stack

- **Primary:** Anthropic Claude API
- **Secondary:** OpenAI GPT-4 API
- **Orchestration:** LangChain
- **Prompt Management:** Custom template system

### AI Agents

**1. Hypothesis Refinement Agent**

```
Role: Help user formulate testable hypothesis
Tasks:
- Convert natural language → structured claim
- Identify assumptions
- Suggest operational definitions
- Propose metrics
```

**2. Methodology Agent**

```
Role: Guide through quality gates (G1-G6)
Tasks:
- Check numeric completeness
- Verify bounded scope
- Validate operational definitions
- Ensure reproducibility parameters
```

**3. Skepticism Agent**

```
Role: Productive criticism (failure mode probing)
Tasks:
- "How would this break?"
- "What's the simplest alternative explanation?"
- "What assumptions are we treating as facts?"
- "Where does this claim stop being valid?"
```

**4. Domain Expert Agent**

```
Role: Domain-specific guidance
Tasks:
- Suggest appropriate simulation type
- Recommend parameter ranges
- Identify relevant prior work
- Flag domain-specific pitfalls
```

### Prompt Engineering

**Charter-Based System Prompts:**

```
You are a research methodology assistant operating under 
the Research Assistant Charter v3.

Your role is to help users formulate rigorous, testable 
hypotheses that satisfy quality gates G1-G6:

G1: Numeric completeness (≥2 numeric thresholds)
G2: Bounded scope (one testable claim)
G3: Operational definitions (all terms measurable)
G4: Test rigidity (no post-hoc adjustment)
G5: Controls (negative controls specified)
G6: Reproducibility (full parameter specification)

Never let enthusiasm override rigor.
Always ask: "How would this fail?"
```

-----

## Layer 4: Simulation Layer

### Technology Stack

- **Orchestration:** Kubernetes
- **Container Runtime:** Docker
- **Job Queue:** RabbitMQ
- **Compute:** AWS EC2 (auto-scaling) or GCP Compute
- **GPU Compute:** AWS P3/P4 instances or GCP A100 VMs

### Domain-Specific Containers

**LLM Testing (Fold-Engine)**

```dockerfile
FROM python:3.11-slim
RUN pip install anthropic litellm sentence-transformers
COPY fold_engine/ /app/
ENTRYPOINT ["python", "/app/run_test.py"]
```

**Biology (Protein Folding)**

```dockerfile
FROM nvidia/cuda:12.0-base
RUN pip install alphafold openmm biopython
COPY protein_sim/ /app/
ENTRYPOINT ["python", "/app/run_simulation.py"]
```

**Physics (Particle Dynamics)**

```dockerfile
FROM python:3.11-slim
RUN pip install numpy scipy matplotlib
COPY physics_sim/ /app/
ENTRYPOINT ["python", "/app/run_physics.py"]
```

### Simulation Execution Flow

```
1. User queues simulation
   ↓
2. Job added to RabbitMQ queue
   ↓
3. Kubernetes pulls job
   ↓
4. Allocates appropriate resources (CPU/GPU)
   ↓
5. Spins up domain container
   ↓
6. Mounts input parameters (from S3)
   ↓
7. Executes simulation
   ↓
8. Streams logs via WebSocket
   ↓
9. Saves results to S3
   ↓
10. Triggers validation layer
```

### Resource Allocation

**Free Tier:**

- CPU: 2 cores, 4GB RAM
- Time limit: 10 minutes per simulation
- Queue priority: Low

**Pro Tier:**

- CPU: 8 cores, 16GB RAM
- GPU: 1x T4 (optional)
- Time limit: 1 hour per simulation
- Queue priority: Medium

**Institution Tier:**

- CPU: 32+ cores, 64GB+ RAM
- GPU: Multiple A100s available
- Time limit: 24 hours per simulation
- Queue priority: High

-----

## Layer 5: Validation Layer

### Technology Stack

- **Language:** Python 3.11+
- **Framework:** FastAPI
- **Schema Validation:** Pydantic + JSON Schema
- **Cryptography:** hashlib (SHA-256)
- **Version Control:** pygit2

### Validation Pipeline

**Step 1: Quality Gate Verification**

```python
def validate_gates(hypothesis: Hypothesis) -> GateResults:
    """
    Verify all G1-G6 gates are satisfied.
    Returns: Pass/Fail for each gate + overall status
    """
    return {
        'G1_numeric': check_numeric_thresholds(hypothesis),
        'G2_bounded': check_bounded_scope(hypothesis),
        'G3_operational': check_operational_defs(hypothesis),
        'G4_rigid': check_test_rigidity(hypothesis),
        'G5_controls': check_negative_controls(hypothesis),
        'G6_reproducible': check_reproducibility(hypothesis),
        'overall': all_gates_pass()
    }
```

**Step 2: Results Validation**

```python
def validate_results(
    preregistration: PreReg,
    results: SimulationResults
) -> ValidationReport:
    """
    Check if results meet preregistered criteria.
    No post-hoc threshold adjustment allowed.
    """
    return {
        'criteria_met': results.metric >= preregistration.threshold,
        'controls_valid': validate_negative_controls(results),
        'reproducibility': check_provenance_complete(results),
        'verdict': 'PASS' | 'FAIL' | 'INCONCLUSIVE'
    }
```

**Step 3: Provenance Generation**

```python
def generate_provenance(
    hypothesis: Hypothesis,
    simulation: Simulation,
    results: Results
) -> ProvenanceManifest:
    """
    Generate complete provenance package.
    """
    return {
        'hypothesis_hash': sha256(hypothesis.to_json()),
        'methodology_hash': sha256(simulation.config),
        'results_hash': sha256(results.data),
        'git_commit': get_git_commit(),
        'container_version': get_container_version(),
        'environment': capture_environment(),
        'timestamps': get_all_timestamps(),
        'signatures': generate_cryptographic_signatures()
    }
```

### Schema Validation

**Hypothesis Schema:**

```json
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "type": "object",
  "required": ["claim", "metrics", "thresholds", "controls"],
  "properties": {
    "claim": {
      "type": "string",
      "description": "Falsifiable hypothesis"
    },
    "metrics": {
      "type": "array",
      "items": {"type": "string"},
      "minItems": 1
    },
    "thresholds": {
      "type": "object",
      "description": "Numeric success/failure criteria",
      "minProperties": 2
    },
    "controls": {
      "type": "array",
      "description": "Negative controls",
      "minItems": 1
    }
  }
}
```

-----

## Layer 6: Publishing Layer

### Technology Stack

- **Version Control:** Git (pygit2)
- **Storage:** GitHub API + S3
- **DOI Service:** DataCite API
- **Citation Format:** BibTeX generation

### Repository Structure

**Each validated result generates:**

```
username/hypothesis-id/
├── README.md              # Human-readable summary
├── HYPOTHESIS.md          # Full hypothesis specification
├── METHODOLOGY.md         # Preregistered methodology
├── RESULTS.md            # Results summary
├── data/
│   ├── inputs.json       # Input parameters
│   ├── outputs.json      # Simulation results
│   └── raw_data/         # Raw output files
├── provenance/
│   ├── manifest.json     # Full provenance
│   ├── hashes.txt        # Cryptographic hashes
│   └── environment.yml   # Exact environment spec
└── citation.bib          # BibTeX citation
```

### DOI Assignment

**Workflow:**

```
1. Results validated → PASS
   ↓
2. Generate repository
   ↓
3. Publish to GitHub (or internal Git)
   ↓
4. Submit to DataCite for DOI
   ↓
5. DOI assigned: 10.XXXXX/iqueue.2026.hypothesis_id
   ↓
6. Update repository with DOI badge
   ↓
7. Result is now citable
```

-----

## Data Persistence

### Database Schema (PostgreSQL)

**Users:**

```sql
CREATE TABLE users (
    id UUID PRIMARY KEY,
    email VARCHAR(255) UNIQUE NOT NULL,
    username VARCHAR(50) UNIQUE NOT NULL,
    tier VARCHAR(20) DEFAULT 'free',
    created_at TIMESTAMP DEFAULT NOW(),
    updated_at TIMESTAMP DEFAULT NOW()
);
```

**Hypotheses:**

```sql
CREATE TABLE hypotheses (
    id UUID PRIMARY KEY,
    user_id UUID REFERENCES users(id),
    title VARCHAR(255) NOT NULL,
    claim TEXT NOT NULL,
    domain VARCHAR(50) NOT NULL,
    state VARCHAR(20) DEFAULT 'draft', -- draft, locked, testing, validated
    methodology_hash VARCHAR(64),
    created_at TIMESTAMP DEFAULT NOW(),
    locked_at TIMESTAMP,
    published_at TIMESTAMP
);
```

**Simulations:**

```sql
CREATE TABLE simulations (
    id UUID PRIMARY KEY,
    hypothesis_id UUID REFERENCES hypotheses(id),
    status VARCHAR(20) DEFAULT 'queued', -- queued, running, completed, failed
    progress FLOAT DEFAULT 0.0,
    started_at TIMESTAMP,
    completed_at TIMESTAMP,
    compute_minutes INT,
    results_s3_key VARCHAR(255)
);
```

**Results:**

```sql
CREATE TABLE results (
    id UUID PRIMARY KEY,
    simulation_id UUID REFERENCES simulations(id),
    verdict VARCHAR(20), -- PASS, FAIL, INCONCLUSIVE
    metric_value FLOAT,
    threshold FLOAT,
    provenance_hash VARCHAR(64),
    doi VARCHAR(100),
    published_repo_url VARCHAR(255)
);
```

### Object Storage (S3)

**Bucket Structure:**

```
iqueue-data/
├── inputs/
│   └── {hypothesis_id}/
│       └── parameters.json
├── outputs/
│   └── {simulation_id}/
│       ├── results.json
│       └── raw_data/
├── provenance/
│   └── {result_id}/
│       └── manifest.json
└── repos/
    └── {username}/
        └── {hypothesis_id}/
```

-----

## Security & Privacy

### Authentication

- OAuth 2.0 (Google, Apple, GitHub)
- JWT tokens (short-lived, 1 hour)
- Refresh tokens (7 days)
- API keys for programmatic access

### Authorization

- Role-based access control (RBAC)
- Hypothesis ownership enforced
- Private hypotheses accessible only to owner
- Team workspaces for institution tier

### Data Protection

- Encryption at rest (S3, RDS)
- Encryption in transit (TLS 1.3)
- Private hypotheses never exposed
- Results can be embargoed (institution tier)

### Abuse Prevention

- Rate limiting (per user, per IP)
- Compute quotas enforced
- Job runtime limits
- Spam detection for hypotheses

-----

## Scalability

### Horizontal Scaling

**API Gateway:**

- Load balanced across multiple instances
- Auto-scaling based on request volume
- Stateless design (session in Redis)

**Simulation Layer:**

- Kubernetes auto-scaling
- Job queue prevents overload
- Priority-based resource allocation

**Database:**

- Read replicas for queries
- Connection pooling
- Caching layer (Redis)

### Performance Targets

**Response Times:**

- API: <200ms (p95)
- Hypothesis validation: <2s
- Simulation queueing: <1s

**Throughput:**

- 10,000 concurrent users
- 1,000 simulations/hour
- 100 results published/hour

-----

## Monitoring & Observability

### Metrics

- **Application:** Request rates, error rates, latency
- **Compute:** CPU, memory, GPU utilization
- **Queue:** Job backlog, processing time, failures
- **Cost:** Compute spend per tier, per domain

### Logging

- Structured JSON logs
- Centralized aggregation (CloudWatch / StackDriver)
- Log levels: DEBUG, INFO, WARN, ERROR

### Alerting

- High error rates
- Queue backlog exceeds threshold
- Compute spend anomalies
- Security events

### Tools

- **Monitoring:** Prometheus + Grafana
- **Logging:** ELK Stack or CloudWatch
- **Tracing:** OpenTelemetry
- **Alerts:** PagerDuty

-----

## Disaster Recovery

### Backup Strategy

- Database: Daily backups, 30-day retention
- S3: Versioning enabled, lifecycle policies
- Git repos: Mirrored to backup locations

### Recovery Plan

- RPO (Recovery Point Objective): 24 hours
- RTO (Recovery Time Objective): 4 hours
- Automated failover for critical services

-----

## Development Workflow

### Environments

- **Local:** Docker Compose for local development
- **Staging:** Full cloud stack, test data
- **Production:** Production cloud stack

### CI/CD Pipeline

```
1. Code push to GitHub
   ↓
2. Automated tests (pytest, jest)
   ↓
3. Linting (black, eslint)
   ↓
4. Build Docker containers
   ↓
5. Deploy to staging
   ↓
6. Integration tests
   ↓
7. Manual approval
   ↓
8. Deploy to production
```

### Testing Strategy

- Unit tests (80%+ coverage)
- Integration tests (critical paths)
- End-to-end tests (user journeys)
- Load testing (before major releases)

-----

## Technology Decisions

### Why React Native?

- Single codebase for iOS + Android
- Fast development iteration
- Large ecosystem
- Proven at scale (Facebook, Instagram, Discord)

### Why Node.js for API?

- JavaScript everywhere (mobile → backend)
- Excellent async performance
- Large ecosystem
- WebSocket support built-in

### Why Kubernetes?

- Auto-scaling for compute
- Container orchestration
- Cloud-agnostic
- Industry standard

### Why PostgreSQL?

- ACID compliance
- JSON support (flexible schema evolution)
- Excellent performance
- Open source

-----

## Open Questions

*To be resolved during MVP development:*

1. **Compute Cost Model:**
- How to price compute fairly?
- Free tier limits sustainable?
- GPU pricing strategy?
1. **Domain Prioritization:**
- Start with LLM only, or multi-domain MVP?
- Which domains have highest demand?
1. **Community Features:**
- How much collaboration vs. individual research?
- Peer review system needed?
- Gamification elements?
1. **Monetization:**
- Freemium conversion rate assumptions?
- Institution tier pricing?
- Grant funding strategy?

-----

## Next Steps

1. **Prototype API** (FastAPI)
1. **Build hypothesis validation** (charter gates)
1. **Integrate Fold-Engine** (LLM testing domain)
1. **Mobile app mockups** (Figma)
1. **Cloud infrastructure setup** (AWS or GCP)

**Target:** Working end-to-end prototype by Q2 2026

-----

*Architecture is living document. Will evolve as we build and learn.*
