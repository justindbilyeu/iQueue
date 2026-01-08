# iQueue MVP Specification

**Detailed specifications for Minimum Viable Product (Phase 1)**

**Target:** Working mobile app with LLM testing domain  
**Timeline:** 6 months (April - September 2026)  
**Success Metric:** 100 beta users, 50+ validated results published

-----

## MVP Scope

### What’s IN Scope:

✅ Mobile app (iOS + Android)  
✅ User authentication  
✅ Hypothesis submission with AI guidance  
✅ Quality gate validation (G1-G6)  
✅ LLM testing domain (Fold-Engine integration)  
✅ Preregistration & methodology lock  
✅ Simulation execution on cloud  
✅ Results validation  
✅ Publishing to Git repos with DOI

### What’s OUT of Scope:

❌ Multiple scientific domains (just LLM testing)  
❌ VR environments  
❌ Advanced community features  
❌ Team workspaces  
❌ API access  
❌ Payment processing (all users free during beta)

-----

## User Flows

### Flow 1: First-Time User Onboarding

```
1. Download app from App Store / Play Store
2. Open app → Splash screen → Onboarding slides:
   - Slide 1: "Got a hypothesis? Test it rigorously."
   - Slide 2: "No credentials required. Just curiosity."
   - Slide 3: "From idea to validated result in hours."
3. "Sign In" (OAuth: Google, Apple, GitHub)
4. Profile setup:
   - Username
   - Optional: Bio, interests, website
5. Tutorial (interactive):
   - "Let's submit your first hypothesis"
   - Guided tour of key features
6. Dashboard (empty state):
   - "Submit Your First Hypothesis" CTA
```

**Success Criteria:** User completes onboarding in <3 minutes

-----

### Flow 2: Hypothesis Submission

**Step 1: Idea Capture**

```
Screen: "What's Your Hypothesis?"

Input: Natural language text area
- Placeholder: "Describe your idea in plain language..."
- Voice input button (speech-to-text)
- Markdown support for equations
- Character limit: 2000

AI Assistance (real-time):
- "Make this more specific"
- "This seems like multiple claims - can you separate them?"
- "What would prove this wrong?"

Example hypotheses shown below input
```

**Step 2: Domain Selection**

```
Screen: "What Domain?"

Options:
- LLM Testing (only option in MVP)
  - Description: "Test intrinsic properties of language models"
  - Examples: "Paraphrase invariance, determinism, context robustness"

Future domains shown but grayed out:
- Biology (Coming Soon)
- Physics (Coming Soon)
- Chemistry (Coming Soon)
```

**Step 3: Hypothesis Refinement**

```
Screen: "Refine Your Claim"

AI Chat Interface:
User: "I think LLMs should give same answer to paraphrased questions"

AI: "Good start! Let's make this testable:
     1. Define 'same answer' - exact text match or semantic similarity?
     2. Define 'paraphrased questions' - how different can they be?
     3. What threshold would prove your hypothesis?"

User iterates with AI until claim is clear

Output: Structured hypothesis
- Claim: "LLMs should produce semantically similar answers (cosine similarity >0.85) to paraphrased questions"
- Domain: LLM Testing
- Test Type: Paraphrase Invariance
```

**Step 4: Methodology Wizard**

```
Screen: "Quality Gates"

Progress bar: Gate 1/6

Gate G1: Numeric Completeness
Question: "What numeric threshold defines success?"
Input: 
- Metric: [Dropdown: Cosine Similarity, Exact Match, etc.]
- Success threshold: [Number input: 0.85]
- Failure threshold: [Number input: 0.70]

AI Help: "Why these numbers? What's your reasoning?"

[Next] button disabled until valid input

Repeat for all gates:
- G1: Numeric thresholds ✓
- G2: Bounded scope (single claim) ✓
- G3: Operational definitions ✓
- G4: Test rigidity (confirm no post-hoc adjustment) ✓
- G5: Negative controls ✓
- G6: Reproducibility parameters ✓
```

**Step 5: Simulation Parameters**

```
Screen: "Test Parameters"

Based on test type (Paraphrase Invariance):
- Number of base prompts: [Slider: 5-50, default 20]
- Paraphrases per prompt: [Slider: 1-5, default 2]
- Model to test: [Dropdown: Claude Sonnet, GPT-4, etc.]
- Temperature: [Slider: 0.0-1.0, default 0.0]

Estimated compute time: ~15 minutes
Estimated cost: Free (beta)

[Review & Lock Methodology]
```

**Step 6: Preregistration Review**

```
Screen: "Lock Methodology"

Complete specification shown:
- Hypothesis
- All quality gates
- Test parameters
- Success/failure criteria
- Negative controls

Warning: "Once locked, methodology cannot be changed"

Cryptographic hash displayed: sha256:abc123...

[Lock & Queue Simulation]
```

**Success Criteria:**

- User completes submission in <15 minutes
- 90% of users pass quality gates on first try (with AI help)

-----

### Flow 3: Simulation Monitoring

```
Screen: "Your Simulations"

List of simulations:
┌──────────────────────────────────────────┐
│ Paraphrase Invariance Test              │
│ Status: Running (45% complete)           │
│ Started: 2 min ago                       │
│ Est. completion: 13 min                  │
│ [View Live Logs]                         │
└──────────────────────────────────────────┘

Tapping simulation shows:
- Real-time progress bar
- Live log stream (WebSocket)
- Current stage (e.g., "Testing prompt 8/20")
- Option to cancel (before completion)
```

**Success Criteria:**

- Real-time updates work reliably
- Users understand what’s happening

-----

### Flow 4: Results Review

```
Screen: "Results"

Header:
✅ PASSED | ❌ FAILED | ⚠️ INCONCLUSIVE

Primary Metric:
Cosine Similarity: 0.89 (threshold: 0.85)

Visual: Chart showing similarity scores for all prompt pairs

Negative Control:
Semantic Alteration: 0.42 (expected <0.85) ✅

Details:
- Total queries: 40
- Excluded: 2 (extraction failures)
- Execution time: 14.2 minutes

Provenance:
- Methodology hash: sha256:abc123...
- Model ID: claude-sonnet-4-20250514
- Timestamp: 2026-04-15T14:23:17Z

[Publish Results] [Download Data] [Share]
```

**Success Criteria:**

- Users understand verdict immediately
- Provenance is transparent
- Can export all data

-----

### Flow 5: Publishing

```
Screen: "Publish Results"

Repository preview:
┌──────────────────────────────────────────┐
│ justinbilyeu/paraphrase-test-20260415    │
│                                          │
│ README.md                                │
│ HYPOTHESIS.md                            │
│ METHODOLOGY.md                           │
│ RESULTS.md                               │
│ data/                                    │
│ provenance/                              │
└──────────────────────────────────────────┘

Options:
- [ ] Publish publicly (visible to all)
- [x] Publish privately (just me)
- [ ] Request DOI (for citation)

[Publish]

Success screen:
"Results Published! 🎉"
Repository URL: https://iqueue.science/justinbilyeu/paraphrase-test-20260415
DOI: 10.5281/iqueue.2026.04.15.001

[Share on Twitter] [Copy Link] [Done]
```

**Success Criteria:**

- Publishing takes <30 seconds
- Generated repos are well-formatted
- DOI works for citations

-----

## Technical Specifications

### Mobile App

**Tech Stack:**

- Framework: React Native 0.73+
- State: Redux Toolkit
- Navigation: React Navigation
- UI Library: React Native Paper (Material Design)
- Charts: Victory Native
- Real-time: Socket.io client
- Auth: React Native App Auth (OAuth 2.0)

**Key Libraries:**

```json
{
  "react-native": "0.73.0",
  "react-redux": "9.0.0",
  "@reduxjs/toolkit": "2.0.0",
  "react-navigation": "6.0.0",
  "react-native-paper": "5.11.0",
  "victory-native": "37.0.0",
  "socket.io-client": "4.6.0",
  "react-native-app-auth": "7.0.0"
}
```

**Screens:**

1. Splash
1. Onboarding (3 slides)
1. Auth (sign in)
1. Dashboard
1. Hypothesis Submission (multi-step wizard)
1. Simulation Queue
1. Results Viewer
1. Profile
1. Settings

**Offline Support:**

- Hypothesis drafts saved locally
- Queue when online
- Cached results available offline

-----

### Backend API

**Tech Stack:**

- Framework: FastAPI (Python 3.11)
- Database: PostgreSQL 15
- Cache: Redis 7
- Queue: RabbitMQ
- Storage: AWS S3
- AI: Anthropic Claude API

**Endpoints:**

**Authentication:**

```python
POST   /api/v1/auth/google      # OAuth callback
POST   /api/v1/auth/apple       # OAuth callback
POST   /api/v1/auth/github      # OAuth callback
POST   /api/v1/auth/refresh     # Refresh JWT token
```

**Hypotheses:**

```python
POST   /api/v1/hypotheses                  # Create
GET    /api/v1/hypotheses                  # List user's hypotheses
GET    /api/v1/hypotheses/{id}             # Get details
PUT    /api/v1/hypotheses/{id}             # Update (draft only)
DELETE /api/v1/hypotheses/{id}             # Delete (draft only)
POST   /api/v1/hypotheses/{id}/validate    # Run quality gates
POST   /api/v1/hypotheses/{id}/lock        # Preregister & lock
```

**AI Assistance:**

```python
POST   /api/v1/ai/refine       # Refine hypothesis text
POST   /api/v1/ai/suggest      # Suggest parameters
POST   /api/v1/ai/critique     # Productive skepticism
```

**Simulations:**

```python
POST   /api/v1/simulations              # Queue simulation
GET    /api/v1/simulations              # List user's simulations
GET    /api/v1/simulations/{id}         # Get status
GET    /api/v1/simulations/{id}/logs    # Stream logs (SSE)
DELETE /api/v1/simulations/{id}         # Cancel
```

**Results:**

```python
GET    /api/v1/results/{id}                 # Get results
GET    /api/v1/results/{id}/provenance      # Get provenance
POST   /api/v1/results/{id}/publish         # Publish to repo
GET    /api/v1/results/{id}/download        # Download ZIP
```

**WebSocket Events:**

```python
# Client subscribes to simulation updates
ws://api.iqueue.science/ws?token={jwt}

# Server sends progress updates
{
  "type": "SIMULATION_PROGRESS",
  "simulationId": "sim_abc123",
  "progress": 0.45,
  "currentStage": "Testing prompt 8/20",
  "estimatedCompletion": "2026-04-15T14:30:00Z"
}
```

-----

### Database Schema

**Users:**

```sql
CREATE TABLE users (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    email VARCHAR(255) UNIQUE NOT NULL,
    username VARCHAR(50) UNIQUE NOT NULL,
    oauth_provider VARCHAR(20) NOT NULL, -- google, apple, github
    oauth_id VARCHAR(255) NOT NULL,
    bio TEXT,
    avatar_url VARCHAR(500),
    created_at TIMESTAMP DEFAULT NOW(),
    updated_at TIMESTAMP DEFAULT NOW()
);

CREATE INDEX idx_users_email ON users(email);
CREATE INDEX idx_users_username ON users(username);
```

**Hypotheses:**

```sql
CREATE TABLE hypotheses (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    user_id UUID REFERENCES users(id) ON DELETE CASCADE,
    title VARCHAR(255) NOT NULL,
    claim TEXT NOT NULL,
    domain VARCHAR(50) NOT NULL, -- 'llm_testing'
    test_type VARCHAR(50) NOT NULL, -- 'paraphrase_invariance'
    state VARCHAR(20) DEFAULT 'draft', -- draft, locked, testing, completed
    
    -- Methodology (JSON)
    parameters JSONB NOT NULL,
    quality_gates JSONB NOT NULL,
    
    -- Hashing
    methodology_hash VARCHAR(64),
    
    -- Timestamps
    created_at TIMESTAMP DEFAULT NOW(),
    locked_at TIMESTAMP,
    completed_at TIMESTAMP
);

CREATE INDEX idx_hypotheses_user ON hypotheses(user_id);
CREATE INDEX idx_hypotheses_state ON hypotheses(state);
```

**Simulations:**

```sql
CREATE TABLE simulations (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    hypothesis_id UUID REFERENCES hypotheses(id) ON DELETE CASCADE,
    
    status VARCHAR(20) DEFAULT 'queued', -- queued, running, completed, failed, cancelled
    progress FLOAT DEFAULT 0.0,
    current_stage VARCHAR(255),
    
    -- Compute
    container_image VARCHAR(255) NOT NULL,
    compute_minutes INT,
    
    -- Storage
    input_s3_key VARCHAR(500),
    output_s3_key VARCHAR(500),
    logs_s3_key VARCHAR(500),
    
    -- Timestamps
    queued_at TIMESTAMP DEFAULT NOW(),
    started_at TIMESTAMP,
    completed_at TIMESTAMP
);

CREATE INDEX idx_simulations_hypothesis ON simulations(hypothesis_id);
CREATE INDEX idx_simulations_status ON simulations(status);
```

**Results:**

```sql
CREATE TABLE results (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    simulation_id UUID REFERENCES simulations(id) ON DELETE CASCADE,
    
    verdict VARCHAR(20) NOT NULL, -- PASS, FAIL, INCONCLUSIVE
    
    -- Metrics
    primary_metric VARCHAR(100) NOT NULL,
    metric_value FLOAT NOT NULL,
    threshold FLOAT NOT NULL,
    
    -- Negative controls
    control_metrics JSONB,
    
    -- Provenance
    provenance_hash VARCHAR(64),
    provenance_s3_key VARCHAR(500),
    
    -- Publishing
    published BOOLEAN DEFAULT FALSE,
    repo_url VARCHAR(500),
    doi VARCHAR(100),
    
    created_at TIMESTAMP DEFAULT NOW()
);

CREATE INDEX idx_results_simulation ON results(simulation_id);
CREATE INDEX idx_results_published ON results(published);
```

-----

### Compute Infrastructure

**Kubernetes Setup:**

**Namespace:**

```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: iqueue-simulations
```

**Job Template (Fold-Engine):**

```yaml
apiVersion: batch/v1
kind: Job
metadata:
  name: sim-{simulation_id}
  namespace: iqueue-simulations
spec:
  template:
    spec:
      containers:
      - name: fold-engine
        image: iqueue/fold-engine:v0.1.0
        env:
        - name: HYPOTHESIS_ID
          value: "{hypothesis_id}"
        - name: ANTHROPIC_API_KEY
          valueFrom:
            secretKeyRef:
              name: api-keys
              key: anthropic
        resources:
          requests:
            memory: "4Gi"
            cpu: "2"
          limits:
            memory: "8Gi"
            cpu: "4"
      restartPolicy: Never
  backoffLimit: 3
```

**Resource Quotas (MVP - Free Tier):**

```yaml
apiVersion: v1
kind: ResourceQuota
metadata:
  name: free-tier-quota
  namespace: iqueue-simulations
spec:
  hard:
    requests.cpu: "100"      # Max 50 concurrent jobs (2 CPU each)
    requests.memory: "400Gi" # Max 50 concurrent jobs (8GB each)
    count/jobs.batch: "200"  # Max 200 queued jobs
```

-----

### Fold-Engine Integration

**Container:** `iqueue/fold-engine:v0.1.0`

**Input (from S3):**

```json
{
  "hypothesis_id": "hyp_abc123",
  "test_type": "paraphrase_invariance",
  "parameters": {
    "n_prompts": 20,
    "model_id": "claude-sonnet-4-20250514",
    "temperature": 0.0,
    "threshold": 0.85,
    "negative_control": {
      "type": "semantic_alteration",
      "mechanism": "negation"
    }
  },
  "prompts_file": "s3://iqueue-data/prompts/base_prompts.jsonl"
}
```

**Execution:**

```bash
# Container runs:
python /app/fold_engine/run_test.py \
  --config /input/config.json \
  --output /output/results.json

# Progress updates sent via webhook:
POST https://api.iqueue.science/api/v1/simulations/{id}/progress
{
  "progress": 0.45,
  "current_stage": "Testing prompt 8/20"
}
```

**Output (to S3):**

```json
{
  "test_id": "test1_paraphrase_invariance",
  "verdict": "PASS",
  "metric_value": 0.89,
  "threshold": 0.85,
  "negative_control": {
    "metric_value": 0.42,
    "passed": true
  },
  "n_queries": 40,
  "n_excluded": 2,
  "execution_time_seconds": 852.3,
  "provenance": {
    "model_id": "claude-sonnet-4-20250514",
    "methodology_hash": "sha256:abc123...",
    "timestamp": "2026-04-15T14:23:17Z"
  }
}
```

-----

### Validation Pipeline

**Automated Checks:**

```python
def validate_result(
    hypothesis: Hypothesis,
    simulation: Simulation,
    result: Result
) -> ValidationReport:
    """
    Validate result against preregistration.
    """
    checks = {
        'methodology_unchanged': (
            hypothesis.methodology_hash == 
            result.provenance['methodology_hash']
        ),
        'threshold_met': (
            result.metric_value >= hypothesis.threshold
        ),
        'control_valid': validate_negative_control(result),
        'provenance_complete': check_provenance(result),
        'schema_valid': validate_schema(result)
    }
    
    return ValidationReport(
        verdict=result.verdict,
        checks=checks,
        passed=all(checks.values())
    )
```

-----

### Publishing Pipeline

**Repository Generation:**

```python
def generate_repo(result: Result) -> RepoStructure:
    """
    Generate Git repository for validated result.
    """
    repo = {
        'README.md': generate_readme(result),
        'HYPOTHESIS.md': generate_hypothesis_doc(result),
        'METHODOLOGY.md': generate_methodology_doc(result),
        'RESULTS.md': generate_results_doc(result),
        'data/inputs.json': result.simulation.input_data,
        'data/outputs.json': result.output_data,
        'provenance/manifest.json': result.provenance,
        'provenance/hashes.txt': generate_hashes(result),
        'citation.bib': generate_bibtex(result)
    }
    
    return repo
```

**DOI Assignment:**

```python
async def assign_doi(result: Result) -> str:
    """
    Assign DOI via DataCite API.
    """
    metadata = {
        'titles': [{'title': result.hypothesis.title}],
        'creators': [{'name': result.hypothesis.user.username}],
        'publicationYear': datetime.now().year,
        'resourceType': 'Dataset',
        'url': result.repo_url
    }
    
    doi = await datacite_api.mint_doi(metadata)
    return doi  # e.g., "10.5281/iqueue.2026.04.15.001"
```

-----

## MVP Feature List

### Must-Have (P0):

- [x] Mobile app (iOS + Android)
- [x] User authentication (OAuth)
- [x] Hypothesis submission wizard
- [x] Quality gate validation (G1-G6)
- [x] AI-guided refinement (Claude API)
- [x] LLM testing domain (Fold-Engine)
- [x] Preregistration & lock
- [x] Cloud simulation execution
- [x] Real-time progress updates
- [x] Results validation
- [x] Publishing to Git repo
- [x] DOI assignment

### Nice-to-Have (P1):

- [ ] Hypothesis templates
- [ ] Example gallery
- [ ] Share to social media
- [ ] Email notifications
- [ ] Push notifications (simulation complete)
- [ ] Dark mode

### Future (P2):

- [ ] Community features (browse, comment)
- [ ] Advanced analytics
- [ ] Export formats (PDF, LaTeX)
- [ ] Integration with ORCID
- [ ] Citation tracking

-----

## Success Metrics

**Quantitative:**

- 100 beta users signed up
- 70%+ completion rate (submission → result)
- 50+ validated hypotheses published
- <5% simulation failure rate
- <3 minute app load time (p95)
- 4.0+ App Store rating

**Qualitative:**

- Positive user feedback (surveys)
- Users understand quality gates
- AI assistance is helpful
- Results are trusted
- Willing to recommend to others

-----

## Testing Strategy

### Unit Tests:

- API endpoints (FastAPI test client)
- Quality gate validation logic
- Provenance generation
- DOI integration

### Integration Tests:

- End-to-end flow (submission → result)
- Fold-Engine containerization
- WebSocket reliability
- S3 storage/retrieval

### User Acceptance Testing:

- 10 internal beta testers
- Real hypotheses submitted
- Feedback collected
- Bugs fixed before public beta

-----

## Deployment Plan

### Staging:

- AWS/GCP test environment
- Seeded with test data
- Internal team testing
- Performance benchmarking

### Beta Launch:

- Gradual rollout (10 → 50 → 100 users)
- Monitoring for issues
- Daily check-ins with early users
- Bug fixes within 24 hours

### Production:

- Full deployment after beta success
- 99.9% uptime SLA
- Automated backups
- Incident response plan

-----

## Budget (MVP)

**Development (6 months):**

- Developers (3 FTE × 6 months × $10K/month): $180K
- Designer (0.5 FTE × 6 months × $8K/month): $24K
- Total: **$204K**

**Infrastructure (6 months):**

- AWS/GCP compute: $2K/month × 6 = $12K
- Database: $500/month × 6 = $3K
- Storage: $200/month × 6 = $1.2K
- API costs (Claude): $1K/month × 6 = $6K
- Total: **$22.2K**

**Other:**

- Legal/incorporation: $5K
- Design tools: $1K
- Misc: $3K
- Total: **$9K**

**Grand Total:** **$235.2K** for MVP

-----

## Open Questions

1. **AI Provider:** Claude only, or also support GPT-4?
1. **Pricing:** Free beta indefinitely, or switch to freemium?
1. **Domain Expansion:** Which domain after LLM testing?
1. **Open Source:** Core methodology open, or proprietary?
1. **Partnerships:** Early academic partnerships?

-----

**Next Step:** Start building! 🚀

**First Sprint:** Backend API + Database setup (2 weeks)
