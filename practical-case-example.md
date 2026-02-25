# AI Product Strategy: Agent Logistics Optimizer

**Stage:** Idea
**Date:** 2026-02-25
**Prepared by:** AI Product Strategy Framework - 7-Step Value Stack

Prompt: Use /ai-product-strategy taking into consideration the idea as following: A MILP Solver focused on route and fleet allocation supported by an AI Agent that orchestrate the user queries and the solver functions. This is an idea of product targeting Brazilian trucking transportation business from 50 up to 500 trucks where there is a lack of Operations Research intelectual capital, decision making tools to maximize profitability or minimize costs.

---

## Executive Summary

Agent Logistics Optimizer is a B2B SaaS platform that brings industrial-grade Mixed Integer Linear Programming
(MILP) route and fleet allocation optimization to mid-size Brazilian trucking companies - without
requiring any Operations Research expertise on the buyer's side. An AI Agent acts as the
interface between logistics managers and the mathematical solver, translating plain business
questions into optimized dispatch plans and measurable cost savings. The target segment - fleets
of 50 to 500 trucks - is systematically underserved by enterprise logistics software and lacks
the technical staff to deploy OR tools independently, creating a durable market gap that Agent Logistics Optimizer
is uniquely positioned to fill.

---

## Step 1: Business Value - The Value Stack

### User Pain

Mid-size Brazilian trucking companies with 50 to 500 trucks make daily routing and fleet
allocation decisions manually or through spreadsheets. The result is chronic operational waste:

- Deadhead (empty return) trips averaging 25 to 35% of total kilometers driven
  [Author estimate - verify against CNT or ILOS Brazilian logistics reports]
- Fleet utilization rates below 70% [Author estimate - verify]
- No systematic process for load consolidation or multi-stop route sequencing

These companies know they are leaving money on the table but have no practical path to fix it.
Hiring an OR specialist costs R$15,000 to R$30,000 per month [Author estimate - verify against
Brazilian salary benchmarks: Glassdoor BR, Catho]. Enterprise TMS platforms such as SAP TM and
Oracle OTM require implementation budgets that exceed their annual IT spend.

### Business Outcome

The primary metric is **cost per kilometer driven** and **revenue per truck per month**.

Secondary metrics:

- Fuel spend - represents 35 to 45% of total operating cost for Brazilian truckers
  [Industry estimate - verify against CNT Pesquisa de Custos and NTC&Logistica]
- Overtime hours
- Deadhead percentage

A 5 to 10% improvement in routing efficiency on a 100-truck fleet running 10,000 km per month
per truck represents R$150,000 to R$400,000 in annual savings [Author estimate - based on
approximately R$0.30 to R$0.60/km fuel cost]. That number anchors the entire pricing
conversation.

### AI Leverage

The solver (MILP) already exists as proven technology. HiGHS, GLPK, and CBC are open-source
and production-grade. The blocker has never been the math - it has been the interface layer.

An OR engineer is needed to:
- (a) translate a business problem into a mathematical formulation
- (b) tune constraints and parameters
- (c) interpret solver outputs into actionable dispatch orders

The AI Agent eliminates all three steps. A dispatcher can ask:

> "What is the best way to cover tomorrow's 47 deliveries using 12 trucks,
> keeping all within 10 driving hours?"

And receive an optimized route plan with plain-language explanations - no OR knowledge required.
This is the unlock that makes enterprise-grade optimization accessible to a segment that has
never had it.

### Strategic Wedge

AI Agent removes the human OR bottleneck -> dispatchers get optimal routing decisions daily ->
fleet cost per km drops 5 to 12% -> customers renew because savings exceed SaaS cost by 5x
to 10x.

---

## Step 2: Data Moat

### Input Data

Raw signals that feed the system from Day 1:

| Data Source | Content | Availability |
|---|---|---|
| Delivery orders | Origin, destination, weight, time windows | Customer ERP or manual upload |
| Route logs | Actual paths driven, km, time per leg | Fleet telematics or manual input |
| Fuel consumption records | Liters per truck per trip | Fleet management system |
| Driver logs | Availability, HOS compliance, certifications | HR system or manual |
| Toll cost tables | Cost by corridor, vehicle type | ANTT data [Source: ANTT - Brazil's National Land Transportation Agency] |
| Customer SLAs | Delivery windows, priority tiers, access restrictions | Manual input at onboarding |
| Fleet specifications | Truck capacity, refrigeration, weight class | Manual input at onboarding |

### Feedback Data

Every time a dispatcher modifies, overrides, or rejects a solver recommendation, that signal is
the product's most valuable asset. It reveals hidden constraints the model does not yet know:

- A driver who cannot operate a specific corridor
- A customer who informally requires early morning delivery
- A road that is practically impassable in the wet season
- A client that always requires a specific truck type regardless of what the system suggests

These overrides, captured and tagged, become a proprietary constraint library for that customer -
one that no competitor or generic LLM can replicate without years of operational data from that
same fleet.

### Context Layer (Proprietary)

The compounding moat is the **per-customer constraint graph**: a structured, machine-readable
map of every soft and hard constraint that governs how that specific fleet actually operates.
This graph is built automatically as users interact with the agent and includes:

- Informal business rules ("Client X always gets priority over others")
- Regional route preferences and known road hazards
- Carrier-specific vehicle restrictions and driver preferences
- Seasonal demand patterns tied to specific cargo types - agribusiness seasonality is a
  major driver in Brazil's freight market

A competitor using the same base MILP solver and the same foundation LLM would still produce
inferior recommendations for that customer on Day 1 of deployment, because the constraint graph
takes months of operational dialogue to build.

### Defensibility Assessment

| Timeframe | Moat Strength | Driver |
|---|---|---|
| Launch (Month 0) | Low | Solver and LLM are commodity components |
| Month 3 | Moderate | Early constraint graph and route history accumulating |
| Month 6 | Strong | Constraint graph makes switching costly |
| Month 12+ | Very Strong | Historical operational data + constraint graph + feedback patterns |

By Month 6 of a customer relationship, switching to a competitor means starting the learning
process over from scratch. This creates genuine switching cost beyond contractual lock-in.

---

## Step 3: AI UX Paradigm

**Chosen Paradigm:** Assistant (with a defined evolution path to Agent)

### Rationale

Logistics dispatchers in Brazilian mid-size trucking companies are not early adopters. They have
operated with spreadsheets and phone calls for years. Autonomy given too early - before
demonstrated accuracy - will cause a single bad recommendation to kill trust and churn the
account.

The Assistant paradigm keeps the dispatcher in control:

- The AI presents the optimized plan
- The AI explains the key decisions in plain language
  (e.g., "Route 3 was consolidated to save 180 km because deliveries D-14 and D-22 share
  the same corridor and can be batched without violating either time window")
- The dispatcher approves before anything is dispatched

This also dramatically reduces the risk of the solver producing an output that violates a
real-world constraint the system does not yet know about.

### Evolution Path

| Stage | Name | Trigger | Description |
|---|---|---|---|
| Stage 1 (Months 0 to 6) | Advisor | Launch | AI presents full route plan. Dispatcher reviews, modifies, approves every run. |
| Stage 2 (Months 6 to 12) | Co-Pilot | Modification rate below 15% for 30 days | For high-confidence scenarios, AI pre-populates dispatch. Dispatcher reviews exceptions only. |
| Stage 3 (Month 12+) | Autonomous Dispatch | Acceptance rate above 85% for 90 days + explicit opt-in | AI dispatches routine runs automatically. Alerts human on anomalies or constraint violations only. |

Progression between stages requires explicit customer opt-in - the system never advances
autonomy unilaterally.

---

## Step 4: Domain-Specific Evals

### Primary Use Case

Daily route and fleet allocation planning: given a set of delivery orders for tomorrow, which
trucks should be assigned to which routes, in what sequence, to minimize cost or maximize
throughput within all operational constraints?

### "Good" Definition

Good is not solver accuracy. Good is not answer completeness. Good is:

1. **Dispatcher acceptance rate:** The dispatcher accepts the recommendation without material
   modification on 80% or more of runs [Author estimate - validate as product benchmark
   during pilots]
2. **Operational outcome:** The customer's measured cost per km drops by at least 5% versus
   the 90-day pre-Agent Logistics Optimizer baseline [Author estimate - verify]

These are the two metrics that define product-market fit. If the dispatcher is constantly
overriding the solver, the constraint graph is incomplete. If cost per km is not moving, the
optimization is not translating to real-world execution.

### Failure Mode

The solver recommends a route that violates a real-world constraint the system does not know
about:

- A truck routed to a client that requires a refrigerated vehicle but the assigned truck
  lacks refrigeration
- A driver assigned more hours than legally permitted under Brazilian CLT and transport
  regulations
- A delivery scheduled during a customer's receiving blackout window
- A heavy vehicle routed through a bridge with a weight restriction below the loaded
  truck's gross weight

These failures are high-visibility because they affect real shipments and real clients. A single
visible failure in the first 30 days can end the pilot relationship. They are the primary churn
risk during onboarding.

### Proxy Signal

**Dispatcher modification rate per recommendation** - captured automatically in-product.

| Modification Rate | Interpretation | Action |
|---|---|---|
| Above 40% | Constraint graph critically incomplete | Trigger onboarding review, structured constraint discovery session |
| 20 to 40% | Graph building - expected in Month 1 to 2 | Monitor, capture override reasons |
| Below 20% | Graph maturing well | Eligible for co-pilot progression discussion |
| Below 15% for 30 days | High confidence | Eligible for Stage 2 promotion |

This metric is instrumentable from Day 1 and requires no external data or integrations.

---

## Step 5: Feedback Loop Architecture

### Micro Loop (Session-Level)

**Trigger:** Every dispatcher action on a solver recommendation.

**What is captured:**
- Accept as-is
- Modify (specific change logged: which truck, which route, which sequence, with a
  free-text reason field)
- Reject (reason required)

**What happens next:**
The AI Agent interprets modifications as soft constraint signals and updates the customer's
constraint graph immediately. Example: if the dispatcher consistently removes Driver A from
long-haul routes, the system learns Driver A has an implicit short-haul constraint and stops
recommending him for those assignments within 3 to 5 override events.

### Meso Loop (Weekly)

**What is measured:**
- Which scenario types are run most often (cost minimization vs. capacity maximization vs.
  deadline priority)
- Which constraints are triggered most frequently per customer
- Which route corridors are consistently modified vs. accepted
- Which dispatchers engage most with the AI explanations vs. skipping them

**What it informs:**
Product development prioritization and customer success conversations. Example: "We noticed
your team is manually adjusting refrigerated routes every day - let us formalize that as a hard
constraint in your profile and stop requiring the manual step."

### Macro Loop (Monthly)

**What is measured:**
Correlation of Agent Logistics Optimizer usage intensity against customer-reported (or telematics-reported)
cost per km and fleet utilization rate.

**The key question:**
Do customers using the solver for 80% or more of daily dispatches show measurably different
operational metrics than customers using it for 30% of dispatches? If yes, this data becomes
the renewal argument, the case study, and the upsell trigger.

### Compounding Advantage

Each customer's constraint graph grows more accurate every week. At the product level,
aggregate anonymized patterns across customers - such as common constraint types in
agribusiness fleets vs. retail distribution vs. industrial cargo - become training signal for
improving the AI Agent's constraint-discovery dialogue. This makes onboarding faster and more
accurate for every new customer over time, creating a network effect that compounds across
the customer base even though the data moat itself is per-customer.

---

## Step 6: Business Model Alignment

### Cost per Inference

| Component | Cost Estimate | Basis |
|---|---|---|
| MILP solve (HiGHS, open source, cloud compute) | USD $0.01 to $0.05 per planning session | Author estimate - verify for 100 to 300 stop problem sizes |
| AI Agent LLM calls per session (query parsing, result interpretation) | USD $0.05 to $0.20 per session | Author estimate - verify against current Anthropic API pricing for Claude Sonnet |
| Total AI cost per customer per day | USD $0.06 to $0.25 | Author estimate |
| Total AI cost per customer per month | USD $1.80 to $7.50 | Author estimate |

At a SaaS price of R$320 per truck per month on a 100-truck fleet (R$32,000/month or
approximately USD $5,800/month [Author estimate - using approximate BRL/USD rate, verify]),
the AI inference cost represents well under 0.2% of revenue. The unit economics are extremely
favorable.

### Model-Mixing Plan

| Phase | Timeframe | LLM Strategy | Expected Cost Impact |
|---|---|---|---|
| Launch | Months 0 to 6 | Frontier model (Claude Sonnet 4.6) for all interactions | Baseline cost - quality and accuracy priority |
| Scale | Months 6 to 18 | Fine-tune smaller model on constraint-discovery dialogue logs; use frontier model only for novel queries | 60 to 75% LLM cost reduction [Author estimate - verify] |
| Maturity | Month 18+ | Cached constraint graphs; frontier model as fallback only | Marginal LLM cost; compute cost dominates |

The model-mixing transition should be triggered by volume, not time. When monthly LLM inference
cost across all customers exceeds R$20,000 [Author estimate - adjust], initiate the fine-tuning
program.

### Pricing Model

**Value-based, priced per truck per month.** Token-based or usage-based pricing is incompatible
with this market. Operational buyers in Brazilian mid-market trucking will not accept pricing
that makes them think twice before running a scenario - that friction would kill the feedback
loops that are the product's core asset.

| Tier | Fleet Size | Price per Truck per Month | Monthly Revenue (mid-point fleet) |
|---|---|---|---|
| Starter | Up to 50 trucks | R$400 | R$16,000 (40 trucks) [Author estimate - verify] |
| Growth | 51 to 200 trucks | R$320 | R$48,000 (150 trucks) [Author estimate - verify] |
| Scale | 201 to 500 trucks | R$250 | R$87,500 (350 trucks) [Author estimate - verify] |

### Unit Economics Check

**Example: Growth tier, 150-truck fleet**

| Metric | Value |
|---|---|
| Monthly SaaS revenue | R$48,000 |
| Monthly AI inference cost | approximately R$250 (USD $45) |
| Gross margin (compute only) | above 99% before team and CAC costs |
| Customer annual savings from optimization (7% efficiency gain) | approximately R$2.5 million [Author estimate - verify] |
| Annual SaaS cost to customer | R$576,000 |
| Customer ROI | approximately 4.3x [Author estimate] |

At 10x current volume - 300 customers averaging 150 trucks each - the compute cost remains
below 1% of revenue. The business model holds at scale. The risk is not AI cost. The risk is
customer acquisition cost in a market with long sales cycles and high skepticism toward
technology.

---

## Step 7: Trust Architecture

### Transparency Mechanisms

Every routing recommendation includes three layers of explanation:

**1. Summary statement (always visible)**
> "This plan covers all 47 deliveries using 11 trucks, saving an estimated 340 km versus
> yesterday's routes by consolidating deliveries D-14 and D-22 on Route 3."

**2. Key decision log (expandable)**
> - "Truck 07 assigned to Campinas corridor: highest payload capacity available and no
>   time window conflicts with that route's 3 stops."
> - "Truck 03 excluded from long-haul: driver HOS log shows 9 hours available, below
>   the 11 hours required for the Ribeiro Preto run."

**3. Confidence flag (shown when relevant)**
> "Limited historical data for refrigerated routes to this client. Please review this
> assignment carefully before confirming."

Confidence flags fire automatically when the constraint graph coverage for a scenario type
falls below a threshold, giving dispatchers explicit signal about when to apply extra scrutiny.

### Control Mechanisms

| Mechanism | Function |
|---|---|
| Full manual override | Dispatcher can change any truck, route, or sequence at any time - the system never blocks an action |
| What-if mode | Modify a constraint and re-run the solver instantly without committing ("What if I only use 10 trucks instead of 12?") |
| Rejection logging | Every rejected recommendation requires a reason (dropdown + optional free text) - this is the primary constraint graph training signal |
| Audit trail | Every dispatched plan is logged with dispatcher ID, timestamp, and a diff of all changes made vs. the original recommendation |
| Plan comparison | Dispatcher can compare the AI plan against an alternative scenario side by side before choosing |

### Progressive Autonomy Roadmap

**Stage 1 - Suggest (Months 0 to 6)**

- AI presents complete route plan in the interface
- Dispatcher reviews the full plan, modifies as needed, and clicks "Approve to Dispatch"
- Zero automation - every dispatch is a human decision
- Goal: demonstrate solver accuracy, build constraint graph, earn dispatcher trust

**Stage 2 - Pre-fill (Months 6 to 12)**

- Trigger: modification rate below 15% sustained for 30 days + customer opt-in
- AI pre-populates the dispatch system with the recommended plan
- Dispatcher reviews a "changes from baseline" diff rather than the full plan
- Dispatcher approves the diff - saves 60 to 80% of daily review time [Author estimate]
- Human approval still required before any truck moves

**Stage 3 - Alert-on-Exception (Month 12+)**

- Trigger: acceptance rate above 85% sustained for 90 days + explicit written opt-in
  from fleet manager (not just dispatcher)
- AI dispatches routine, high-confidence runs automatically
- Dispatcher receives a daily summary report and real-time alerts only for:
  - Constraint violations detected
  - New scenario types outside the trained constraint graph
  - Solver confidence below threshold
  - Manual review flag set by any customer rule

Trust is never assumed. Each stage requires a deliberate opt-in decision from the customer's
operations leadership.

---

## Strategic Priorities: What to Do First

### Now (0 to 3 months) - Validate Before Building

**Priority 1: Discovery interviews with 5 to 10 fleet operators**

Target logistics managers and owners of 50 to 150 truck fleets in Brazil. Confirm:

- Are they losing money on routing inefficiency? Do they quantify it?
- What is their current dispatch process? (spreadsheet, phone, basic TMS)
- Would they pay for an optimization tool requiring no technical staff?
- What would make them switch? What would stop them?
- Who makes the buying decision - the owner, the logistics manager, the CFO?

Do not write a line of product code until these interviews are complete. The answers will reshape
the constraint graph architecture, the pricing model, and the go-to-market motion.

**Priority 2: Build a proof-of-concept demo with real customer data**

With permission from one willing fleet operator, take their historical delivery data and run a
MILP solve using HiGHS or CBC. Quantify the delta versus what they actually did. If the solver
finds 8 to 15% savings on real data, the sales conversation becomes structurally easy - you are
showing them their own money left on the table.

### Next (3 to 6 months) - Build the MVP

**Priority 1: AI Agent constraint-discovery interface**

The hardest UX problem in the product. The agent must be able to interview a dispatcher - in
Portuguese, in plain language - and translate the conversation into a structured constraint
graph. This is more important than the solver interface, because the solver already works. The
constraint graph is where the product lives or dies.

**Priority 2: Sign 3 to 5 pilot customers**

Offer significant pricing discount (50 to 70%) in exchange for:
- Co-development access (weekly feedback sessions)
- Permission to use anonymized data for model improvement
- Reference rights if the pilot succeeds

Instrument the modification rate metric from Day 1 of each pilot. Use pilots to validate the
constraint graph architecture and measure real-world acceptance rates.

### Later (6 to 12 months) - Scale What Works

**Priority 1: Formalize the feedback loop infrastructure**

Build the meso and macro loop dashboards internally before making them customer-facing. The
internal dashboard answers: which customers are getting ROI, which are at risk, and which are
ready for Stage 2 promotion? This data drives customer success, renewals, and upsells.

**Priority 2: Begin model-mixing transition**

Fine-tune a smaller model on constraint-discovery dialogue logs from the pilot phase. Target:
reduce LLM inference cost by 60% without measurable quality degradation on the top 80% of
scenario types by frequency.

**Priority 3: Build the case study playbook**

Each pilot customer who demonstrates a quantified ROI - cost per km reduction, fleet
utilization improvement, deadhead percentage reduction - becomes a replicable sales asset.
Brazilian mid-market buyers trust peer references more than vendor claims. One verified case
study from a 200-truck fleet in the same cargo vertical is worth more than 10 product demos.
Structure every case study around three numbers: baseline cost, Agent Logistics Optimizer cost, and savings.

---

## Key Risks and Open Questions

| Risk | Likelihood | Impact | Mitigation |
|---|---|---|---|
| Dispatcher adoption resistance ("the computer doesn't know our routes") | High | High | Stage 1 paradigm - suggest only, no automation; constraint override UX; 90-day onboarding with dedicated CSM; proof-of-concept demo with their own data |
| Solver produces bad recommendations early due to incomplete constraint graph | High | High | Explicit confidence flags on low-coverage scenarios; dispatcher review required in Stage 1; modification rate monitoring with CSM escalation above 40% |
| Sales cycle too long for early-stage cash flow - Brazilian mid-market buys slowly | Medium | High | Anchor sales conversation on ROI demo with customer's own data; offer monthly contracts with no annual lock-in for first 6 months; pilot pricing to reduce decision barrier |
| Competitor response from incumbent TMS vendors (TOTVS Logix, others adding AI features) | Medium | Medium | Constraint graph moat and customer data lock-in; compete on ease-of-use and time-to-value, not feature breadth; target the segment incumbents underserve |
| MILP solve time exceeds dispatcher patience for large fleets (300+ stops, tight windows) | Medium | Medium | Problem decomposition (cluster-first, route-second heuristics); async solve with push notification rather than synchronous wait; set expectation at onboarding |
| Regulatory complexity - Brazilian driver HOS rules, RNTRC requirements, weight restrictions | Low | High | Embed regulation constraints into the base constraint library from launch; position regulatory compliance as a feature, not a limitation; partner with a Brazilian transport law specialist for constraint definition |
| Key person risk - OR expertise concentrated in founding team | Low | High | Document solver architecture and constraint schema thoroughly; build constraint graph as a data layer separate from solver logic so non-OR engineers can maintain the product layer |

---

## Key Figures and Sources

Every specific figure cited in this document and its basis:

| Figure | Value | Source / Basis |
|---|---|---|
| Deadhead (empty return) km percentage for mid-size Brazilian fleets | 25 to 35% | Author estimate - verify against CNT (Confederacao Nacional do Transporte) or ILOS logistics reports |
| Fleet utilization rate for mid-size trucking companies | Below 70% | Author estimate - verify |
| OR specialist monthly salary in Brazil | R$15,000 to R$30,000 | Author estimate - verify against Glassdoor BR, Catho, LinkedIn Salary for "pesquisador operacional" |
| Fuel as percentage of trucking operating cost | 35 to 45% | Industry estimate - verify against CNT Pesquisa de Custos Operacionais and NTC&Logistica annual report |
| Average km per truck per month | 10,000 km | Author estimate - verify against CNT fleet productivity data |
| Annual savings for 100-truck fleet at 5 to 10% efficiency gain | R$150,000 to R$400,000 | Author estimate - based on R$0.30 to R$0.60/km fuel cost, 10,000 km/truck/month, 100 trucks |
| MILP solve cost per session (cloud compute, open source solver) | USD $0.01 to $0.05 | Author estimate - verify for 100 to 300 stop problem sizes on AWS/GCP standard compute |
| AI Agent LLM inference cost per planning session | USD $0.05 to $0.20 | Author estimate - verify against current Anthropic API pricing for Claude Sonnet 4.6 |
| Suggested SaaS pricing - Growth tier | R$320/truck/month | Author estimate - validate against willingness-to-pay interviews before launch |
| Customer ROI - 150-truck Growth tier | approximately 4.3x | Author estimate - based on 7% efficiency gain on R$2.5M annual optimization opportunity vs. R$576K annual SaaS cost |
| LLM cost reduction from model-mixing | 60 to 75% | Author estimate - validate against fine-tuning results |
| Dispatcher time savings in Stage 2 co-pilot mode | 60 to 80% of daily review time | Author estimate - validate during pilot phase |
| Total addressable market - companies with 50 to 500 trucks in Brazil | 2,000 to 5,000 companies | Author estimate - verify against ANTT RNTRC (Registro Nacional de Transportadores Rodoviarios de Cargas) registry and IBGE company census |
| BRL to USD exchange rate used in calculations | approximately 5.5 BRL per USD | Author estimate - use current rate at time of financial modeling |
| Acceptance rate threshold for Stage 3 autonomous dispatch | 85% for 90 days | Author estimate - validate as operational benchmark during Stage 1 and 2 pilots |

---

## Bottom Line

The single most important strategic bet in this plan is that **the AI Agent interface - not the
MILP solver - is the product.** The math is a commodity. The differentiation is making
enterprise-grade Operations Research accessible to a logistics manager with no quantitative
background, in Portuguese, through a conversational interface that learns the hidden rules of
their specific fleet over time.

Success in 12 months looks like: 5 to 10 reference customers in production, each with documented
cost-per-km reductions above 5%, and a constraint graph architecture that demonstrably improves
recommendation accuracy month over month - generating the case studies that make the next 50
customers easy to close.

The one thing that must be true for this to work: a dispatcher with no technical background must
be able to onboard and run their first optimized route plan within 2 hours of signing the
contract - because if adoption requires training programs, IT involvement, or configuration
projects, the target segment will not sustain the behavioral change needed to build the feedback
loops that make the product defensible.

Time to value is the product's most important engineering constraint.

