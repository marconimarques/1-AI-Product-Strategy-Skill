# AI Product Strategy Skill

A Claude Code skill that runs the **8-step Value Stack framework** and produces a complete, executive-ready AI product strategy document grounded in your specific product context - not generic AI strategy advice.

---

## What This Is

This skill works through a structured 8-step framework - Value Stack analysis, primary moat selection, UX paradigm selection, differentiation strategy, domain-specific evals, feedback loop architecture, business model alignment, and trust design - and produces a document where every claim is grounded in what you actually told it, every cited figure is labeled with its basis, and every assumption that requires discovery is explicitly called out as a hypothesis rather than dressed up as insight.

The output is a single document suitable for the team review and alignment.

---

## How to Trigger It

Say things like:

- "Help me build an AI product strategy"
- "Run the Value Stack framework for my product"
- "I want to figure out where AI fits in my product"
- "Build a strategy for my AI idea"
- "Let's think through our AI product direction"

---

## How It Works

The skill runs in three sequential phases.

**Phase 1 - Context gathering**

Before any analysis, the skill asks five targeted questions: what the product does, what stage it is at, what the primary business goal is, what data the product already generates, and who the users are and what their biggest pain point is today. It waits for your answers before proceeding.

**Phase 2 - Framework analysis**

The skill works through all 8 steps applied to your specific product. It does not produce generic examples. Each step reasons from what you described.

**Phase 3 - Strategy document**

A complete, filled-in document. No section placeholders. No generic statements. If a claim requires field discovery to validate, it is written as a hypothesis - not asserted as a market fact.

---

## The 8-Step Framework

| Step | What It Produces |
|---|---|
| 1. Business Value | Value Stack: user pain, business outcome, AI leverage, and the strategic wedge connecting all three |
| 2. Primary Moat | Choice between Data, Distribution, or Trust moat - with the three data layers and a timeline to defensibility |
| 3. AI UX Paradigm | Choice between Assistant, Agent, Autonomous, or Embedded Intelligence - with rationale and an evolution path |
| 4. Differentiation Strategy | The primary lever that makes the product compelling on day one and harder to replicate over time |
| 5. Domain-Specific Evals | What "good" means in your domain by business outcome, not model quality metrics |
| 6. Feedback Loop Architecture | Micro, meso, and macro loops designed from the start to compound AI advantage over time |
| 7. Business Model Alignment | Inference cost estimate, model-mixing plan, pricing structure, and a unit economics check at 10x scale |
| 8. Trust Architecture | Transparency mechanisms, user control mechanisms, and a progressive autonomy path |

The document also includes a **Strategic Priorities** section (discovery always comes first, before any build work) and a **Key Figures and Sources** table that lists every cited number with its basis so you know exactly what to verify before presenting to stakeholders.

---

## Design Principle

**Epistemic discipline on user pain.** The skill only asserts what you told it. Market-size claims, competitor gap statements, and user behavior patterns that require field discovery to confirm are written as hypotheses - using explicit framing like "The hypothesis is that..." - not stated as facts. This matters because the difference between a strategy built on confirmed insight and one built on dressed-up assumptions is the difference between a useful document and a misleading one.

---

## Attribution

The development of this skill was informed by the article **"How to Create an AI Product Strategy: The AI Strategic Lens Framework"** by Miqdad Jaffer, published in [The Product Compass](https://www.productcompass.pm) by Pawel Huryn (August 2, 2025).

The article is a paid publication. This skill is an independent implementation and does not reproduce the article's text or frameworks. The reference is acknowledged here for transparency.

If you find the topic valuable, consider supporting the original work at:
https://www.productcompass.pm/p/how-to-create-an-ai-product-strategy
