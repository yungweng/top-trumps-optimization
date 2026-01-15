# Poster Plan: Top Trumps Game Balancing

## The Story Arc

### 1. Setup: The Problem
**"Can we design a card game that's both fair AND exciting?"**
- Top Trumps: simple game, but deck design matters
- Fairness = skilled player should win more often
- Excitement = games should have dramatic lead changes
- 22 cards × 4 categories = 88 design variables

### 2. Conflict: The Trade-off
**"We discovered you CAN'T have both."**
- Show the Pareto front - the curved boundary
- Moving along the curve = sacrificing one for the other
- This is the core finding

### 3. Resolution: Why?
**"The answer lies in card structure."**
- Fair decks → specialized cards (rock-paper-scissors)
- Exciting decks → generalist cards (strong = strong everywhere)
- Category correlation is the key lever

### 4. Insight: Design Guidelines
**"Now designers can choose deliberately."**
- Want competitive/esports? Use low category correlation.
- Want party game? Use high category correlation.

---

## Poster Layout (A0)

```
+------------------------------------------------------------------+
|                           TITLE                                   |
|   Automatic Game Balancing for Top Trumps Using NSGA-II          |
|                     [Names, University, Date]                     |
+------------------------------------------------------------------+
|                    |                      |                       |
|   1. PROBLEM       |   2. METHOD          |   3. RESULTS          |
|                    |                      |                       |
|   - Game rules     |   - NSGA-II          |   - Pareto front      |
|   - Objectives     |   - Parameters       |     plot              |
|   - Why it's hard  |   - Encoding         |   - Convergence       |
|                    |                      |     plot              |
+------------------------------------------------------------------+
|                    |                      |                       |
|   4. ANALYSIS      |   5. KEY INSIGHT     |   6. CONCLUSION       |
|                    |                      |                       |
|   - Deck heatmaps  |   - Correlation      |   - Design guidelines |
|   - Statistics     |     visualization    |   - Future work       |
|   - Comparison     |   - "Money chart"    |   - References        |
|                    |                      |                       |
+------------------------------------------------------------------+
```

---

## Visualizations

### Already Have ✓
| Visualization | File | Purpose |
|---------------|------|---------|
| Pareto front | `pareto_front_final.png` | Show the trade-off |
| Convergence | `convergence_final.png` | Prove optimization worked |
| Deck heatmaps | `deck_heatmaps_final.png` | Visual contrast of extremes |

### Need to Create
| Visualization | Purpose | Priority |
|---------------|---------|----------|
| Category correlation scatter | Show specialist vs generalist cards | HIGH |
| Correlation → objectives chart | The "aha" moment - why correlation matters | HIGH |
| Game rules diagram | Explain Top Trumps quickly | MEDIUM |
| Card example | Make it tangible | MEDIUM |

---

## Visualization Details

### 1. Category Correlation Scatter (HIGH PRIORITY)
**What**: For each deck, plot values of Category 1 vs Category 2 (or all pairs)
**Fair deck**: Cloud/scattered points (low correlation)
**Exciting deck**: Diagonal line (high correlation)
**Message**: "Card specialization is visible"

### 2. Correlation → Objectives Chart (HIGH PRIORITY)
**What**: X-axis = average category correlation, Y-axis = fairness OR excitement
**Show**: All 26 Pareto solutions as points
**Message**: "One metric explains everything" (r² ≈ 0.97)

### 3. Game Rules Diagram (MEDIUM)
**What**: Simple flowchart or illustration
- Two players, each gets half the deck
- Active player picks category
- Higher value wins the trick
- Most tricks wins

### 4. Card Example (MEDIUM)
**What**: Show 2-3 example cards from fair vs exciting deck
**Message**: Make abstract data concrete

---

## Key Numbers to Highlight

| Metric | Value |
|--------|-------|
| Decision variables | 88 |
| Pareto solutions | 26 |
| Hypervolume | 4.171 |
| Fairness range | 69.6% - 86.6% |
| Excitement range | 3.07 - 4.29 |
| Correlation (fair) | 0.21 |
| Correlation (exciting) | 0.52 |
| Variance explained | ~97% |

---

## Text for Each Section

### Title
"Automatic Game Balancing for Top Trumps: A Multi-Objective Optimization Approach"

### 1. Problem (keep short)
- Top Trumps is a card game where players compare card attributes
- Good game design requires BOTH fairness (skill matters) and excitement (unpredictable)
- 88 continuous variables → too complex for manual tuning

### 2. Method
- NSGA-II: Non-dominated Sorting Genetic Algorithm II
- Population: 100, Generations: 100
- 1000 game simulations per evaluation
- SBX crossover, polynomial mutation

### 3. Results
- 26 Pareto-optimal deck configurations
- Clear trade-off: improving fairness reduces excitement
- Hypervolume = 4.171 (converged)

### 4. Analysis
- Fair decks: specialized cards, low category correlation
- Exciting decks: generalist cards, high category correlation
- Within-card variance differs significantly

### 5. Key Insight
- Category correlation is THE predictor (r² ≈ 0.97)
- Low correlation → strategy matters → fair
- High correlation → luck matters → exciting

### 6. Conclusion
- Fairness and excitement are fundamentally at odds
- Designers can choose their target on the Pareto front
- Single actionable metric: category correlation

---

## Next Steps

1. [ ] Create correlation scatter visualization
2. [ ] Create correlation → objectives chart
3. [ ] Design poster layout in tool (PowerPoint/Figma/LaTeX)
4. [ ] Write concise text for each section
5. [ ] Review with group
6. [ ] Print A0

---

## References to Include

- Deb, K. et al. (2002). A fast and elitist multiobjective genetic algorithm: NSGA-II
- pymoo documentation
- Course lecture notes (ODM WS 2025/26)
