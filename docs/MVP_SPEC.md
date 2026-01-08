<!-- docs/MVP_SPEC.md -->
# iQueue MVP Specification

**MVP = Execution Records + Arena (LLM Testing only)**  
**Timeline:** 6 months (Apr–Sep 2026)  
**Goal:** prove credibility can scale *before* adding domains.

---

## MVP Non-Negotiables

### What we must ship
1) **Execution Record pipeline**
   - templates → prereg lock → run → provenance → record
2) **Arena**
   - challenge flows + replication flows + visibility rules
3) **Denial-of-wallet controls**
   - quotas, throttles, anomaly detection, paid credits later
4) **A single coherent backend stack**
   - one API, one job runner, one data model

### What we will NOT ship in MVP
- Multiple scientific domains
- DOIs
- Kubernetes (unless forced by scale; default is managed jobs)
- Social network features (feeds/leaderboards)
- Payments (beta can run on credits + waitlists)

---

## Definitions

### Execution Record (ER)
An immutable package containing:
- Hypothesis (structured)
- Template + parameters
- Preregistered thresholds
- Input dataset/prompt set hash
- Model identifier + snapshot constraints (best effort)
- Logs
- Outputs (raw + summarized)
- Provenance manifest (hashes, environment, timestamps)

**ER claim:** “This ran exactly like this.”

### Arena
Mechanisms that turn ERs into credible evidence:
- **Challenge**: attempt to break method or interpretation
- **Replication**: independent rerun under declared protocol
- **Badge scoring**: credibility tier based on contest/replication history

---

## User Personas (MVP)

1) **Independent tester**
   - wants to test an idea about LLM behavior
2) **Skeptic / challenger**
   - wants to break weak claims and earn reputation
3) **Replicator**
   - reruns records and earns replication credit

We are not targeting “everyone with a hypothesis” yet.
We are targeting people who will actually **run and challenge**.

---

## MVP User Flows

### Flow A — Create an Execution Record (templated)
1) Choose template (e.g., Paraphrase Invariance)
2) Provide claim statement + thresholds (guided)
3) Select model + prompt set size
4) Lock prereg (hash + timestamp)
5) Run job (queued)
6) View outputs + verdict (PASS/FAIL/INCONCLUSIVE)
7) Publish Execution Record (public by default in beta)

**Key:** The user is not designing methodology from scratch. They are selecting and configuring templates.

---

### Flow B — Challenge a Record (Arena)
1) Open an ER
2) Click **Challenge**
3) Choose challenge type:
   - Threshold sanity
   - Prompt set brittleness
   - Baseline comparison
   - Alternative metric
   - Leakage / contamination suspicion
4) Submit challenge run (new ER linked as “challenge”)
5) Original ER becomes **Contested**

---

### Flow C — Replicate a Record
1) Open an ER
2) Click **Replicate**
3) System enforces replication protocol:
   - new prompt set (same distribution)
   - same template + thresholds
   - controlled parameter variance (seed, batch)
4) Run replication job
5) If replication matches declared criteria → ER becomes **Replicated**

---

## Badge Levels (MVP)

Badges are **not truth**. They are credibility signals.

- **ER (Execution Record)**: immutable run + provenance
- **C0 Contested**: has at least one substantive challenge
- **R1 Replicated**: at least one independent replication succeeded
- **R2 Multi-Replicated**: two+ independent replications with variance constraints
- **S1 Stable**: replication holds across 2+ prompt sets (distribution controlled)

Badge rules are explicit and computable.

---

## Metrics (realistic)

### Success looks like:
- 100 beta users
- 200+ Execution Records created
- 50+ Challenges submitted
- 30+ Replications completed
- 10+ records reach R1
- p95 job failure < 10% (MVP reality)
- Average ER creation time < 20 minutes

### What we measure from day 1:
- drop-off points in the wizard
- cost per ER (including AI guidance)
- abuse attempts / throttle triggers
- time-to-first-challenge

---

## MVP Platform Requirements

### Abuse / cost control (must-have)
- Per-user daily run quotas
- Per-user daily AI-token budget
- Global budget circuit breaker
- Job runtime caps
- Anomaly detection (bursting behavior)
- Shadow banning / throttling tiers

### Privacy (MVP)
- Public ERs by default (beta)
- Private ERs reserved for later paid tier

---

## MVP Tech (summary)
- Mobile: React Native
- API: FastAPI (Python)
- DB: Postgres
- Cache/Rate limit: Redis
- Jobs: managed job runner (Batch/Cloud Run Jobs/etc.)
- Storage: object storage (S3/GCS)
- Observability: structured logs + cost meters

See `docs/ARCHITECTURE.md` for details.
