# Findings: What Makes Top Trumps Decks Fair vs Exciting

## The Fundamental Trade-off

Our NSGA-II optimization discovered a clear inverse relationship between **fairness** and **excitement**:

- **Fairness** (p4 win rate): 69.6% – 86.6%
- **Excitement** (trick changes): 3.07 – 4.29

You cannot maximize both simultaneously. Designing for skill-based outcomes reduces unpredictability, and vice versa.

---

## Key Discriminating Metrics

| Metric | Correlation with Fairness | Correlation with Excitement |
|--------|---------------------------|----------------------------|
| Dominance Pairs | r = -0.968 | r = +0.982 |
| Rank Difference Between Categories | r = +0.971 | r = -0.984 |
| Category Correlation (avg) | r = -0.948 | r = +0.983 |
| Within-Card Std Deviation | r = +0.918 | r = -0.939 |

**The average inter-category correlation explains ~97% of variance in both objectives.**

---

## Fair Decks (High p4 Win Rate ~87%)

Fair decks reward the skilled player (p4) by making strategy matter.

### Characteristics
- **Specialized cards**: Each card excels in 1-2 categories but is weak in others
- **Low category correlation** (r ≈ 0.21): Being strong in Category 1 doesn't predict strength in Category 2
- **Few dominance pairs** (~52): More "rock-paper-scissors" relationships between cards
- **High within-card variance** (std ≈ 1.72): Large spread of values within each card

### Why This Helps p4
- p4 calculates exact win probability for each category choice
- Specialized cards have clear "best use cases" that p4 can identify
- p0's simple heuristic (pick highest normalized value) fails when categories are uncorrelated
- Skill translates directly to wins because optimal play is distinguishable from naive play

---

## Exciting Decks (High Trick Changes ~4.3)

Exciting decks create unpredictability and frequent lead changes.

### Characteristics
- **Generalist cards**: Strong cards are strong in ALL categories; weak cards are weak everywhere
- **High category correlation** (r ≈ 0.52): Categories are somewhat redundant
- **Many dominance pairs** (~120): Clearer card hierarchies
- **Low within-card variance** (std ≈ 1.46): Cards have similar values across categories

### Why This Creates Excitement
- When categories are correlated, category choice matters less
- Card quality (random draw) dominates over strategic choice
- More balanced matchups lead to unpredictable outcomes
- Upsets happen more frequently → more lead changes per game

---

## Summary Comparison

| Property | Fair Decks | Exciting Decks |
|----------|------------|----------------|
| Category correlation | Low (0.21) | High (0.52) |
| Dominance pairs | Few (~52) | Many (~120) |
| Within-card std | High (1.72) | Low (1.46) |
| Card archetype | Specialists | Generalists |
| What determines outcome | Strategy | Card draw luck |

---

## Causal Mechanism

```
Low Category Correlation
        ↓
Cards have diverse strength profiles
        ↓
Optimal category choice varies per card
        ↓
p4's probability calculation gives advantage
        ↓
Skill → Wins (FAIR)
```

```
High Category Correlation
        ↓
Strong cards dominate in all categories
        ↓
Category choice matters less
        ↓
Random card distribution determines outcomes
        ↓
Luck → Upsets → Lead changes (EXCITING)
```

---

## Design Recommendations

- **For competitive/skill-based games**: Design decks with LOW category correlation (specialized cards)
- **For party/casual games**: Design decks with HIGH category correlation (generalist cards)
- **Key actionable metric**: Average inter-category correlation is the single most predictive factor

---

## Optimization Results

- **Algorithm**: NSGA-II
- **Population**: 100, Generations: 100
- **Evaluations**: 10,000 (R=1000 simulations each)
- **Pareto front**: 26 non-dominated solutions
- **Hypervolume**: 4.171
