<!-- docs/README.md -->
# iQueue

**A credibility commons for people with hypotheses.**

iQueue helps anyone turn a question into a **verifiable execution record**, then earn credibility through **challenge and replication**—not credentials.

This is not “publish anything.”  
This is: **run it, prove it ran, let others try to break it, then earn the badge.**

---

## The Idea (Start Here)

Most “democratized research” projects die for one reason:

> They democratize *publication*, not *credibility*.

Science isn’t a pipeline of steps. It’s a living immune system:
- claims are challenged
- methods are questioned
- results are replicated
- reputations are earned
- knowledge persists as memory

iQueue is infrastructure for that immune system—built for independent researchers.

---

## What iQueue Produces

### The Ladder

Everything in iQueue moves through a credibility ladder:

1) **Execution Record**
   - Preregistered method + locked parameters
   - Deterministic run artifact (inputs/outputs/logs)
   - Provenance hashes + environment capture
   - *This is not “true.” It is “verifiably executed.”*

2) **Contested Record**
   - Other users (or the system) challenge assumptions
   - Alternative baselines attempted
   - Red-team attempts logged

3) **Replicated Record**
   - Independent rerun succeeds under declared replication protocol
   - Same claim, new prompt set / seed / model snapshot constraints

4) **Citable Record**
   - Earns a badge based on replication + contest history + integrity checks
   - DOI is optional and **not** part of MVP

**Rule:** Nothing becomes “citable” until it survives the Arena.

---

## What iQueue Is (and is not)

### iQueue IS:
- A methodology + execution + audit system
- A templated experiment runner (starting with LLM evaluation)
- A public arena for adversarial critique + replication
- A credibility scoring / badging layer

### iQueue IS NOT:
- A guarantee of “research-grade truth”
- A replacement for domain expertise
- A permissionless DOI minting machine
- A general simulation platform in v1

---

## MVP Wedge: LLM Testing (Fold-Engine)

We start with **templated LLM evaluations** because:
- tests can be standardized
- artifacts are reproducible
- abuse cases are easier to model
- credibility can be earned through replication

MVP focus:
- Paraphrase invariance
- Determinism / stochasticity
- Context robustness
- Order invariance
- Self-consistency

---

## The Missing Layer Most Projects Ignore

**The Arena** is the product.

If iQueue skips contest + replication, it becomes:
- a landfill of plausible junk, or
- a private toy with no social trust

So we build the Arena first-class.

---

## Principles

1) **Gates of evidence, not status**
2) **Execution integrity before interpretation**
3) **Replication is the credibility currency**
4) **Abuse is assumed (design accordingly)**
5) **Negative results are first-class records**
6) **Transparency by default; privacy is paid**

---

## Status

**Stage:** Foundation (Jan 2026)  
**Immediate goal:** working end-to-end system that creates Execution Records and runs Arena challenges.

Next: `docs/MVP_SPEC.md` and `docs/ARCHITECTURE.md`
