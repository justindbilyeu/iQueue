# iQueue Roadmap

**From concept to platform that serves 3 billion people**

-----

## Overview

iQueue development follows a **phased approach**:

1. **Foundation** (Q1 2026) - Methodology validation, architecture design
1. **MVP** (Q2-Q3 2026) - Working prototype with LLM testing
1. **Scale** (Q4 2026-Q2 2027) - Multi-domain expansion, user growth
1. **VR Labs** (Q3 2027+) - Immersive research environments

**Philosophy:** Ship fast, validate early, iterate based on real usage.

-----

## Phase 0: Foundation (January - March 2026)

**Goal:** Validate methodology, design architecture, build team

### Milestones

**M0.1: Vision & Documentation** ✅

- [x] README.md (vision document)
- [x] ARCHITECTURE.md (technical design)
- [x] ROADMAP.md (this document)
- [ ] MVP_SPEC.md (detailed specifications)
- [ ] CONTRIBUTING.md (collaboration guidelines)

**M0.2: Fold-Engine Completion**

- [ ] Complete Fold-Engine test suite
- [ ] Validate preregistration methodology works
- [ ] Document charter-based workflow
- [ ] Generate first research-grade results
- **Success Criteria:** Fold-Engine produces validated, reproducible LLM test results

**M0.3: Prototype Hypothesis Flow**

- [ ] Build CLI prototype (Python)
- [ ] Implement quality gates (G1-G6) validation
- [ ] Test preregistration → lock → execute → validate flow
- [ ] Prove methodology can be automated
- **Success Criteria:** Can take hypothesis from submission → validated result via command line

**M0.4: AI Integration Proof-of-Concept**

- [ ] Claude API integration for hypothesis refinement
- [ ] Test AI-guided gate satisfaction
- [ ] Measure quality improvement (AI-assisted vs. not)
- **Success Criteria:** AI demonstrably helps users satisfy quality gates

**M0.5: Team Formation**

- [ ] Identify collaborators (developers, domain experts)
- [ ] Define roles and responsibilities
- [ ] Set up collaboration infrastructure (Discord, GitHub Projects)
- **Success Criteria:** Core team of 3-5 people committed

**Deliverables:**

- Complete foundational documentation
- Working Fold-Engine
- CLI prototype demonstrating full flow
- AI integration proof-of-concept
- Core team assembled

**Timeline:** 3 months (January - March 2026)

-----

## Phase 1: MVP - Minimum Viable Product (April - September 2026)

**Goal:** Ship working mobile app with LLM testing domain

### M1.1: Backend Infrastructure (April 2026)

**API Development:**

- [ ] FastAPI backend setup
- [ ] User authentication (OAuth 2.0)
- [ ] Hypothesis CRUD operations
- [ ] Quality gate validation endpoints
- [ ] AI guidance integration (Claude API)

**Database:**

- [ ] PostgreSQL schema implementation
- [ ] User management
- [ ] Hypothesis storage
- [ ] Simulation tracking

**Compute Infrastructure:**

- [ ] Kubernetes cluster setup (AWS/GCP)
- [ ] Docker container for Fold-Engine
- [ ] Job queue (RabbitMQ)
- [ ] S3 bucket structure

**Deliverable:** Working backend API with authentication, hypothesis management, and compute orchestration

**Timeline:** 6 weeks

-----

### M1.2: Mobile App (May - June 2026)

**Core Screens:**

- [ ] Onboarding / authentication
- [ ] Hypothesis submission wizard
- [ ] Methodology wizard (quality gates)
- [ ] Simulation queue dashboard
- [ ] Results viewer

**Features:**

- [ ] Offline hypothesis drafting
- [ ] Real-time progress updates (WebSocket)
- [ ] AI assistance integration
- [ ] Share/export results

**Platforms:**

- [ ] iOS (React Native)
- [ ] Android (React Native)

**Deliverable:** Functional mobile app for iOS and Android

**Timeline:** 8 weeks

-----

### M1.3: LLM Testing Domain Integration (July 2026)

**Fold-Engine Integration:**

- [ ] Containerize Fold-Engine
- [ ] API wrapper for simulation execution
- [ ] Parameter schema definition
- [ ] Results schema definition

**Templates:**

- [ ] Paraphrase invariance test template
- [ ] Determinism test template
- [ ] Context robustness test template
- [ ] Self-consistency test template
- [ ] Order invariance test template

**Documentation:**

- [ ] Domain-specific user guide
- [ ] Example hypotheses
- [ ] Interpretation guide for results

**Deliverable:** LLM testing domain fully integrated and documented

**Timeline:** 4 weeks

-----

### M1.4: Validation & Publishing (August 2026)

**Validation Pipeline:**

- [ ] Automated quality gate checking
- [ ] Results validation against preregistration
- [ ] Provenance generation
- [ ] Schema validation

**Publishing:**

- [ ] Git repository generation
- [ ] DOI integration (DataCite)
- [ ] README/documentation generation
- [ ] Citation format (BibTeX)

**Deliverable:** End-to-end validation and publishing workflow

**Timeline:** 4 weeks

-----

### M1.5: Beta Launch (September 2026)

**Pre-Launch:**

- [ ] Internal dogfooding (team uses app for 2 weeks)
- [ ] Bug fixes from dogfooding
- [ ] Performance testing
- [ ] Security audit

**Beta Launch:**

- [ ] Invite 100 beta users
- [ ] Onboarding flow testing
- [ ] Collect feedback (surveys, interviews)
- [ ] Monitor usage patterns

**Success Criteria:**

- 70%+ completion rate (submission → validated result)
- <5% error rate
- Positive NPS score (>40)
- At least 50 validated results published

**Deliverable:** MVP app with 100 active beta users

**Timeline:** 4 weeks

-----

**Phase 1 Summary:**

- **Duration:** 6 months (April - September 2026)
- **Output:** Working mobile app with LLM testing
- **Validation:** 100 users, 50+ published results
- **Decision Point:** Proceed to scale or pivot based on feedback

-----

## Phase 2: Scale (October 2026 - June 2027)

**Goal:** Expand domains, grow user base, validate business model

### M2.1: Biology Domain (October - November 2026)

**Protein Folding:**

- [ ] AlphaFold integration
- [ ] Molecular dynamics simulations
- [ ] Parameter templates
- [ ] Results visualization

**Cell Dynamics:**

- [ ] Basic cell simulation environments
- [ ] Pathway modeling
- [ ] Gene expression modeling

**Success Criteria:** 10+ validated biology hypotheses

**Timeline:** 8 weeks

-----

### M2.2: Physics Domain (December 2026 - January 2027)

**Particle Dynamics:**

- [ ] N-body simulations
- [ ] Field theory calculations
- [ ] Collision modeling

**Cosmology:**

- [ ] Universe expansion models
- [ ] Dark matter simulations
- [ ] CMB predictions

**Success Criteria:** 10+ validated physics hypotheses

**Timeline:** 8 weeks

-----

### M2.3: Chemistry Domain (February - March 2027)

**Molecular Dynamics:**

- [ ] LAMMPS integration
- [ ] Reaction pathway analysis
- [ ] Materials property prediction

**Drug Binding:**

- [ ] Docking simulations
- [ ] Binding affinity predictions
- [ ] ADMET property prediction

**Success Criteria:** 10+ validated chemistry hypotheses

**Timeline:** 8 weeks

-----

### M2.4: Community Features (April 2027)

**Discovery:**

- [ ] Browse public hypotheses
- [ ] Filter by domain, status, verdict
- [ ] Search functionality

**Social:**

- [ ] Follow researchers
- [ ] Comment on results
- [ ] Share hypotheses

**Collaboration:**

- [ ] Team workspaces (institution tier)
- [ ] Shared hypotheses
- [ ] Collaborative editing

**Success Criteria:** 30% of users engage with community features

**Timeline:** 6 weeks

-----

### M2.5: Business Model Validation (May - June 2027)

**Freemium Launch:**

- [ ] Free tier: Basic simulations
- [ ] Pro tier ($10/month): Advanced compute
- [ ] Institution tier ($500-5000/month): Teams + unlimited

**Metrics:**

- [ ] Free → Pro conversion rate
- [ ] Institution tier acquisition
- [ ] Compute cost per tier
- [ ] Customer acquisition cost (CAC)
- [ ] Lifetime value (LTV)

**Success Criteria:**

- 5% free → pro conversion
- 3+ institution customers
- LTV:CAC ratio > 3:1

**Timeline:** 8 weeks

-----

**Phase 2 Summary:**

- **Duration:** 9 months (October 2026 - June 2027)
- **Output:** 4 domains (LLM, Bio, Physics, Chem)
- **Users:** 10,000+ total, 500+ paying
- **Results:** 500+ validated hypotheses published
- **Decision Point:** Proceed to VR or focus on domain expansion

-----

## Phase 3: VR Research Labs (July 2027 - December 2027)

**Goal:** Build immersive research environments

### M3.1: VR Prototype (July - August 2027)

**Platform:**

- [ ] Meta Quest 3 / Quest Pro
- [ ] Unity or Unreal Engine
- [ ] Hand tracking
- [ ] Voice commands

**Core Experience:**

- [ ] Virtual lab space
- [ ] 3D visualization of results
- [ ] Spatial hypothesis mapping
- [ ] Gesture-based interaction

**Success Criteria:** Working prototype, positive user feedback

**Timeline:** 8 weeks

-----

### M3.2: Domain-Specific VR Environments (September - October 2027)

**Biology Lab:**

- [ ] Protein structure visualization (3D)
- [ ] Interactive molecular manipulation
- [ ] Cell dynamics observation

**Physics Lab:**

- [ ] Particle track visualization
- [ ] Field line rendering
- [ ] Spacetime curvature visualization

**Success Criteria:** Domain experts validate utility

**Timeline:** 8 weeks

-----

### M3.3: Collaborative VR Spaces (November - December 2027)

**Multi-User:**

- [ ] Shared virtual labs
- [ ] Avatar presence
- [ ] Voice chat
- [ ] Collaborative hypothesis building

**Whiteboarding:**

- [ ] Virtual whiteboards
- [ ] Equation editor
- [ ] Diagram drawing

**Success Criteria:** Teams use VR for collaborative research

**Timeline:** 8 weeks

-----

**Phase 3 Summary:**

- **Duration:** 6 months (July - December 2027)
- **Output:** VR research lab environments
- **Users:** 1,000+ VR users
- **Decision Point:** VR as core product or supplementary feature?

-----

## Phase 4: Global Scale (2028+)

**Goals:**

- 100,000+ active users
- 10+ scientific domains
- 10,000+ validated results published
- Institutional adoption (universities, research labs)
- Grant funding secured
- Open source core components

**Potential Expansions:**

- Climate science domain
- Materials science domain
- Economics/social systems modeling
- Educational partnerships (high schools, universities)
- API access for institutional research
- White-label deployments

-----

## Key Metrics

### Product Metrics

- **Hypothesis Submission Rate:** Hypotheses created per week
- **Completion Rate:** % of hypotheses that reach validation
- **Quality Gate Pass Rate:** % passing all gates first try
- **Simulation Success Rate:** % of simulations that complete successfully
- **Publishing Rate:** Results published per week

### User Metrics

- **MAU (Monthly Active Users):** Total active users per month
- **Retention:** % of users active after 1 month, 3 months, 6 months
- **Engagement:** Avg hypotheses per user
- **NPS (Net Promoter Score):** User satisfaction

### Business Metrics

- **Conversion Rate:** Free → Pro tier
- **MRR (Monthly Recurring Revenue):** Total subscription revenue
- **CAC (Customer Acquisition Cost):** Cost to acquire one user
- **LTV (Lifetime Value):** Revenue per user over lifetime
- **Compute Cost:** Infrastructure cost per user/simulation

### Impact Metrics

- **Published Results:** Total validated hypotheses
- **Citations:** Times iQueue results are cited
- **Breakthroughs:** Novel findings from the platform
- **Democratization:** % of results from non-institutional researchers

-----

## Risk Mitigation

### Technical Risks

**Risk:** Compute costs spiral out of control
**Mitigation:**

- Strict quotas per tier
- Auto-scaling limits
- Cost monitoring and alerts
- Optimize simulation efficiency

**Risk:** Simulation quality varies across domains
**Mitigation:**

- Domain expert review before launch
- Extensive validation testing
- User feedback loops
- Continuous improvement

**Risk:** Mobile app performance issues
**Mitigation:**

- Performance testing from day 1
- Progressive web app fallback
- Optimize for low-end devices

### Business Risks

**Risk:** Low free → pro conversion
**Mitigation:**

- A/B test pricing
- Value demonstration (show compute savings)
- Institution tier focus (higher margins)

**Risk:** Insufficient institutional adoption
**Mitigation:**

- Early partnerships with universities
- Grant funding applications
- White-label options
- API access for integration

**Risk:** Abuse / spam hypotheses
**Mitigation:**

- Rate limiting
- Quality gate enforcement
- Manual review flagging system
- Community moderation

### Community Risks

**Risk:** Low-quality hypotheses flood platform
**Mitigation:**

- Quality gates are strict
- AI guidance improves quality
- Failed hypotheses still valuable (negative results)
- Community can filter by quality

**Risk:** Toxic community behavior
**Mitigation:**

- Code of conduct
- Moderation tools
- Report/block functionality
- Emphasize collaborative, not competitive culture

-----

## Decision Points

**After Phase 1 (MVP):**

- ✅ **Proceed** if: >70% completion rate, positive NPS, clear path to scale
- ⚠️ **Pivot** if: Low completion rate, negative feedback, fundamental UX issues
- ❌ **Pause** if: Technical infeasibility, unsustainable costs

**After Phase 2 (Scale):**

- ✅ **Proceed to VR** if: Strong user growth, business model validated, demand for VR
- ✅ **Focus on domains** if: More domains requested, VR demand unclear
- ⚠️ **Restructure** if: Growth stalled, unit economics broken

**After Phase 3 (VR):**

- ✅ **VR as core** if: High engagement, clear value-add, competitive moat
- ✅ **VR as feature** if: Useful but not essential, mobile remains primary
- ⚠️ **Sunset VR** if: Low adoption, high cost, limited value

-----

## Success Criteria (Overall)

**By End of 2026:**

- [ ] 10,000+ users
- [ ] 500+ validated results published
- [ ] 4 scientific domains operational
- [ ] Positive unit economics
- [ ] Institutional partnerships (3+)

**By End of 2027:**

- [ ] 100,000+ users
- [ ] 5,000+ validated results
- [ ] 8+ scientific domains
- [ ] Profitable or path to profitability clear
- [ ] Academic recognition (papers citing iQueue)

**Long-Term Vision (2030):**

- [ ] 1,000,000+ users
- [ ] 100,000+ validated results
- [ ] Research infrastructure for independent scientists globally
- [ ] Proven model for democratized science
- [ ] Breakthrough discoveries attributed to platform

-----

## Open Questions

*To be resolved during development:*

1. **Domain Priority:** Which domains have highest demand/impact?
1. **Pricing:** Optimal free/pro/institution tier limits?
1. **VR Timing:** When is VR mature enough for research use?
1. **Partnerships:** Which universities/institutions to target first?
1. **Funding:** Venture capital, grants, or bootstrap?
1. **Open Source:** Which components should be open vs. proprietary?

-----

## Team Growth

### Phase 1 (MVP):

- 1 Founder/Product (Justin)
- 1 Full-Stack Developer
- 1 Mobile Developer
- 1 DevOps/Infrastructure
- 1 Domain Expert (LLM testing)

### Phase 2 (Scale):

- Add: 2 Backend Developers
- Add: 1 Frontend Developer
- Add: 3 Domain Experts (Bio, Physics, Chem)
- Add: 1 Designer (UX/UI)
- Add: 1 Community Manager

### Phase 3 (VR):

- Add: 2 VR Developers (Unity/Unreal)
- Add: 1 3D Artist
- Add: 1 VR Experience Designer

**Total Team by End of 2027:** ~15 people

-----

## Funding Strategy

### Bootstrap (Phase 0-1):

- Founder resources
- Small angel investments (<$100K)
- Grants (NSF, foundations)

### Seed Round (Phase 2):

- Target: $2-5M
- Use: Team expansion, infrastructure scaling
- Timing: After MVP validation

### Series A (Phase 3+):

- Target: $10-20M
- Use: VR development, global expansion
- Timing: After product-market fit proven

**Alternative:** Stay lean, bootstrap via revenue, avoid VC if possible

-----

## Communication Plan

### Quarterly Updates:

- Public blog posts
- GitHub milestones
- Community Discord announcements
- Metrics dashboard (public transparency)

### Annual Review:

- State of iQueue report
- User stories / impact highlights
- Roadmap adjustments
- Open goals for next year

-----

*This roadmap is a living document. We’ll adapt based on what we learn.*

**Next step:** Build Phase 0 MVP prototype.

**Let’s go.** 🚀
