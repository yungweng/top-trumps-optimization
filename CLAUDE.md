# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a university assignment for "Optimization and Decision Making" (Winter 2025/26). The goal is to create an **A0 poster** demonstrating automatic game balancing for Top Trumps using multi-objective optimization.

**Deadline**: February 2nd, 2026, 11:59 PM

## The Optimization Problem

Design Top Trumps card decks that maximize both **fairness** and **excitement**.

### Decision Variables
- x ∈ ℝ^(K×L) where K=22 cards, L=4 categories
- Each value bounded [1, 10]
- Total: 88 real-valued variables

### Objectives (to maximize)
1. **Fairness**: Win rate of skilled player p4 (game should reward skill)
2. **Excitement**: Average number of trick changes per game (lead changes)

### Agents
- **p0** (weak): Picks category with highest normalized value on current card
- **p4** (strong): Calculates exact win probability from remaining cards

### Simulation Parameters
- R = 1000 simulations per deck evaluation
- K/2 = 11 tricks per game (each card played once)

## Commands

```bash
# Install dependencies
pip install numpy pymoo

# Run the notebook
jupyter notebook top-trumps.ipynb

# Or execute directly
jupyter execute top-trumps.ipynb
```

## Architecture

### `top-trumps.ipynb`

**TopTrumpsSimulation** - Game engine
- `set_deck(deck_list)`: Configure deck from flat array of K×L values
- `simulate_game()`: Returns dict with `p4_tricks`, `trick_changes`, `p4_won`
- `get_p0_choice(card)`: Weak agent strategy (max normalized value)
- `get_p4_choice(card, remaining_cards)`: Strong agent strategy (exact win probability)

**TopTrumpsBalancing** - pymoo interface (ElementwiseProblem)
- Wraps simulation for optimization
- Objectives are **negated** for minimization (pymoo convention)
- `_evaluate(x, out)`: Runs n_simulations and returns [-avg_win_rate, -avg_trick_changes]

## Course Context

Relevant algorithms from lectures:
- **NSGA-II**: (μ+μ) strategy with non-dominated sorting + crowding distance
- **SMS-EMOA**: (μ+1) steady-state with hypervolume contribution
- **MOEA/D**: Decomposes into weighted subproblems

Quality indicators:
- **Hypervolume (HV)**: Primary indicator - has soundness property
- **IGD**: Inverted Generational Distance (needs reference set)
- **Crowding Distance**: Measures solution spread

## Required Deliverables

1. Approximate the Pareto front for K=22, L=4, R=1000
2. Evaluate approximation quality using a quality indicator
3. Analyze patterns: What deck characteristics favor fairness vs. excitement?

## Lecture Materials

Text-converted lecture notes are available in:
`../downloads/25_11_ODM_IntroMOO.txt` - Multi-objective optimization concepts
`../downloads/25_12_ODM_MOOAlgos.txt` - MOO algorithms (NSGA-II, SMS-EMOA, MOEA/D)
`../downloads/25_07_ODM_EAs_Intro.txt` - Evolutionary algorithms basics
