# Contributing to iQueue

**Welcome! We’re building research infrastructure for 3 billion people.**

-----

## Vision

iQueue democratizes research capability. Anyone with a smartphone should be able to test their ideas rigorously—no credentials, no gatekeeping, just clear thinking and determination.

If you believe in this vision, we want your help.

-----

## How to Contribute

### 1. Code Contributions

**Areas We Need:**

- Backend development (Python/FastAPI)
- Mobile development (React Native)
- DevOps/Infrastructure (Kubernetes, AWS/GCP)
- Domain-specific simulation environments
- AI integration (prompt engineering, LLM orchestration)

**Process:**

1. Check [open issues](https://github.com/justindbilyeu/iQueue/issues)
1. Comment on issue you want to work on
1. Fork the repo
1. Create feature branch (`git checkout -b feature/amazing-feature`)
1. Commit changes (`git commit -m 'Add amazing feature'`)
1. Push to branch (`git push origin feature/amazing-feature`)
1. Open Pull Request

**Code Standards:**

- Python: Black formatting, type hints, docstrings
- JavaScript: ESLint, Prettier
- Tests required for new features
- Documentation updated

-----

### 2. Domain Expertise

**We need scientists to:**

- Design domain-specific test templates
- Validate simulation environments
- Review methodology for your field
- Contribute example hypotheses

**Domains We’re Building:**

- LLM Testing (active)
- Biology (planned)
- Physics (planned)
- Chemistry (planned)
- Climate Science (planned)

**How to Help:**

- Join [Discord](link-tbd) #domain-experts channel
- Review domain specifications
- Propose test methodologies
- Validate results from your field

-----

### 3. Testing & Feedback

**Beta Testers:**

- Use the app with real hypotheses
- Report bugs via GitHub Issues
- Suggest UX improvements
- Share your results

**How to Become a Beta Tester:**

- Join [waitlist](link-tbd)
- Or: Email justin@iqueue.science with:
  - Your background
  - What you want to test
  - Device (iOS/Android)

-----

### 4. Documentation

**We need:**

- User guides for each domain
- Tutorial videos
- Example hypotheses with explanations
- Translation to other languages

**Process:**

- Documentation lives in `/docs`
- Use Markdown
- Include code examples where relevant
- Screenshots for UX documentation

-----

### 5. Community Building

**Help us grow:**

- Share iQueue on social media
- Write blog posts about your results
- Present at conferences
- Connect us with potential partners

**Community Channels:**

- Discord: [link-tbd]
- Twitter: [@iQueueScience](link-tbd)
- Blog: [blog.iqueue.science](link-tbd)

-----

## Development Setup

### Prerequisites:

- Python 3.11+
- Node.js 18+
- Docker
- PostgreSQL 15
- Redis 7

### Backend Setup:

```bash
# Clone repo
git clone https://github.com/justindbilyeu/iQueue.git
cd iQueue

# Create virtual environment
python -m venv venv
source venv/bin/activate  # or `venv\Scripts\activate` on Windows

# Install dependencies
pip install -r requirements.txt
pip install -r requirements-dev.txt

# Set up database
createdb iqueue_dev
alembic upgrade head

# Set environment variables
cp .env.example .env
# Edit .env with your API keys

# Run backend
uvicorn app.main:app --reload
```

### Mobile App Setup:

```bash
# Navigate to mobile directory
cd mobile

# Install dependencies
npm install

# iOS
cd ios && pod install && cd ..
npx react-native run-ios

# Android
npx react-native run-android
```

### Docker Setup (Recommended):

```bash
# Start all services
docker-compose up -d

# View logs
docker-compose logs -f

# Stop services
docker-compose down
```

-----

## Repository Structure

```
iQueue/
├── backend/                 # FastAPI backend
│   ├── app/
│   │   ├── api/            # API endpoints
│   │   ├── core/           # Core logic (quality gates, validation)
│   │   ├── models/         # Database models
│   │   ├── schemas/        # Pydantic schemas
│   │   └── services/       # Business logic
│   ├── tests/              # Backend tests
│   └── alembic/            # Database migrations
│
├── mobile/                  # React Native app
│   ├── src/
│   │   ├── screens/        # App screens
│   │   ├── components/     # Reusable components
│   │   ├── redux/          # State management
│   │   └── services/       # API clients
│   └── __tests__/          # Mobile tests
│
├── simulations/             # Domain-specific containers
│   ├── fold-engine/        # LLM testing
│   ├── bio-sim/            # Biology simulations
│   └── physics-sim/        # Physics simulations
│
├── docs/                    # Documentation
│   ├── user-guides/
│   ├── api-docs/
│   └── domain-specs/
│
└── infrastructure/          # Kubernetes configs, Terraform, etc.
    ├── k8s/
    └── terraform/
```

-----

## Pull Request Guidelines

### Before Submitting:

- [ ] Code follows style guidelines
- [ ] Tests pass (`pytest` for backend, `npm test` for mobile)
- [ ] New tests added for new features
- [ ] Documentation updated
- [ ] Commit messages are clear
- [ ] Branch is up to date with `main`

### PR Template:

```markdown
## Description
Brief description of changes

## Type of Change
- [ ] Bug fix
- [ ] New feature
- [ ] Breaking change
- [ ] Documentation update

## Testing
How did you test this?

## Screenshots (if applicable)

## Checklist
- [ ] Tests pass
- [ ] Documentation updated
- [ ] Code reviewed by self
```

-----

## Code of Conduct

### Our Standards:

**We encourage:**

- Respectful collaboration
- Constructive feedback
- Openness to learning
- Celebrating contributions (big and small)

**We don’t tolerate:**

- Harassment or discrimination
- Disrespectful language
- Personal attacks
- Gatekeeping behavior

**Remember:** iQueue exists to bypass gatekeeping. We practice what we preach.

### Enforcement:

Violations can be reported to: conduct@iqueue.science

We’ll respond within 24 hours and take appropriate action.

-----

## Research Assistant Charter Compliance

**iQueue is built using Research Assistant Charter v3 methodology.**

When contributing, please maintain:

**Quality Gates (G1-G6):**

- G1: Numeric completeness
- G2: Bounded scope
- G3: Operational definitions
- G4: Test rigidity
- G5: Negative controls
- G6: Reproducibility

**Evidence Hierarchy (E1-E5):**

- E5: Fully reproducible
- E4: Methods-grade artifact (our target)
- E3: Reproducible experiment
- E2: Domain knowledge
- E1: Speculation (with test proposal)

**Productive Skepticism:**

- Ask: “How would this break?”
- Explore alternatives
- Identify assumptions
- Test boundary conditions

**See:** <docs/CHARTER.md> for full methodology

-----

## Recognition

**Contributors will be:**

- Listed in CONTRIBUTORS.md
- Mentioned in release notes
- Credited in published papers
- Invited to annual contributor summit (when we have one!)

**Significant contributors may be offered:**

- Equity in iQueue (if we incorporate)
- Employment opportunities
- Research collaboration

-----

## Questions?

**General questions:** Join [Discord](link-tbd)  
**Security issues:** security@iqueue.science  
**Partnership inquiries:** partners@iqueue.science  
**Everything else:** hello@iqueue.science

-----

## License

By contributing, you agree that your contributions will be licensed under the same license as the project.

**Current license:** TBD (likely dual license: open source core, proprietary compute)

-----

## Roadmap Alignment

**Current Phase:** Foundation (Q1 2026)

**Immediate Priorities:**

1. Complete Fold-Engine integration
1. Backend API development
1. Mobile app prototype
1. Quality gate automation

**See:** <ROADMAP.md> for full development plan

-----

## Philosophy

### Why We Build in Public:

**Transparency:** Our methodology demands it
**Collaboration:** Best ideas come from unexpected places
**Accountability:** Public commitments drive execution
**Community:** Building this alone would be impossible

### Our Principles:

1. **Rigor over speed** - But ship anyway
1. **Evidence over narrative** - Show, don’t tell
1. **Access over credentials** - If you can think, you can contribute
1. **Outcomes over activity** - Results matter, not hours logged

-----

## Thank You

**To everyone contributing:** You’re helping democratize research capability for billions of people.

**To beta testers:** Your feedback shapes the platform.

**To domain experts:** Your expertise validates our methodology.

**To believers:** Your support makes this possible.

**Together, we’re building infrastructure that bypasses broken gates.**

**Let’s go.** 🚀

-----

*Last updated: January 2026*
