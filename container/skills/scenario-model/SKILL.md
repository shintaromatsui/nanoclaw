---
name: scenario-model
description: Model 2-4 scenarios with triggers, probabilities, and contingency actions. Use when someone says "model scenarios", "what if", "bull case bear case", "scenario planning", "model this out", "best case worst case", "sensitivity analysis", or needs to think through multiple futures for a decision, investment, career move, or strategy.
---

# Scenario Model

Model 2-4 distinct futures to stress-test a decision. Not a forecast — a structured way to think about what could happen and what you'd do.

## Input

Parse the message to extract:
- **Decision or situation** (required): What you're modeling scenarios for
- **Variables** (optional): Key factors that drive different outcomes
- **Timeframe** (optional): Over what period (default: infer from context)
- **Scenarios** (optional): User-defined — if not provided, auto-generate Bull / Base / Bear + optional Wildcard

Examples:
- "scenario model for Vanta equity value over 4 years"
- "what happens if I leave Amplitude — model the scenarios"
- "bull/bear/base for compliance market evolution 2026-2028"
- "model 3 scenarios for our Q2 revenue"

## Process

### Step 1: Identify Key Variables

Name 2-4 variables that most determine which scenario plays out. These should be:
- **Independent** of each other (not correlated)
- **Observable** — you'll be able to tell which scenario is unfolding
- **High-impact** — small changes produce big outcome differences

Example for "Vanta equity value":
- Revenue growth rate (50% vs 80% vs 120% YoY)
- Revenue multiple at liquidity (10x vs 15x vs 25x)
- Time to liquidity event (18 months vs 3 years vs 5+ years)

### Step 2: Define Scenarios

| Scenario | Description | Probability |
|----------|-------------|-------------|
| **Bull** | Everything goes right. Key tailwinds materialize. | X% |
| **Base** | Most likely path. Mix of wins and setbacks. | X% |
| **Bear** | Key risks materialize. Headwinds dominate. | X% |
| **Wildcard** (optional) | Non-obvious scenario that breaks assumptions. | X% |

Probabilities must sum to 100%. Base should usually be 40-50%.

### Step 3: Model Each Scenario

For each scenario:

**Narrative:** What happens, in sequence (3-5 sentences)

**Key metrics / outcomes:** Quantify the result
- Financial: dollar values, returns, multiples
- Career: title, scope, network, skills gained
- Strategic: market position, optionality, risk exposure

**Leading indicators:** How you'd know this scenario is unfolding (within 3-6 months)

**Contingency actions:** What you should do IF this scenario materializes
- Immediate actions (this week)
- Medium-term pivots (this quarter)

### Step 4: Expected Value

```
EV = (P_bull × Outcome_bull) + (P_base × Outcome_base) + (P_bear × Outcome_bear)
```

Compare to alternatives or status quo.

### Step 5: Robustness Check

- **Regret minimization:** In which scenario would you most regret not acting?
- **Asymmetry:** Is the upside/downside asymmetric?
- **Optionality:** Does any choice preserve more options across scenarios?
- **Timing:** Is there value in waiting for leading indicators before committing?

## Output Format

```
# Scenario Model: [Topic]

**Timeframe:** [X]
**Key variables:** [list]

## Scenarios at a Glance

|                    | Bull (X%)     | Base (X%)     | Bear (X%)     |
|--------------------|---------------|---------------|---------------|
| [Variable 1]       | [value]       | [value]       | [value]       |
| [Variable 2]       | [value]       | [value]       | [value]       |
| **Key outcome**    | [value]       | [value]       | [value]       |

## Bull Case: [Name] (X%)
**Story:** [narrative]
**Outcome:** [quantified]
**Watch for:** [leading indicators]
**If this happens:** [contingency actions]

## Base Case: [Name] (X%)
[same structure]

## Bear Case: [Name] (X%)
[same structure]

## Expected Value
[Probability-weighted outcome]

## Decision Implications
- **If optimizing for expected value:** [recommendation]
- **If optimizing for downside protection:** [recommendation]
- **If optimizing for upside capture:** [recommendation]
```

## Design Principles

- **Name your scenarios.** "The IPO Rocket" is more memorable than "Scenario A."
- **Quantify everything possible.** Vague scenarios aren't useful for decisions.
- **Leading indicators are the gold.** The user needs to know WHEN to act, not just what might happen.
- **Expected value ≠ best decision.** Factor in risk tolerance, regret, and optionality.
- **Wildcard scenarios prevent tunnel vision.** Include one non-obvious future.
