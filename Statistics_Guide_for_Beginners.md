# Basketball Analysis - Beginner's Statistics Reference

## 📚 Essential Concepts Explained Simply

---

## 1. Correlation

### What is it?
A number showing if two things move together.

### The Scale
```
-1.0 ════════════ 0.0 ════════════ +1.0
  ↓              ↓                ↓
Perfect        No              Perfect
Negative      Connection       Positive
```

### Examples

**Positive Correlation (+)**
- Offensive Rating vs Win Percentage
- More offense → More wins (makes sense!)

**Negative Correlation (-)**
- Turnovers vs Win Percentage  
- More turnovers → Fewer wins (makes sense!)

**No Correlation (0)**
- Jersey number vs Win Percentage
- One doesn't affect the other

### How to Interpret
- **0.7 to 1.0** = Very Strong relationship
- **0.4 to 0.7** = Strong relationship
- **0.2 to 0.4** = Weak relationship
- **0.0 to 0.2** = Very Weak relationship
- Negative numbers follow same scale

---

## 2. P-value (The "Is this Real?" Test)

### What is it?
Probability that your result happened by pure random chance.

### The Rule
- **P < 0.05** → Result is "statistically significant" ✓ TRUST IT
- **P ≥ 0.05** → Result could be random ✗ DON'T TRUST IT

### Example
```
Hypothesis: Tall teams win more games
Correlation found: 0.09
P-value: 0.850

Translation: There's 85% chance this correlation 
is just random luck. This hypothesis is probably FALSE.
```

### Why 0.05?
- It's a traditional threshold
- Means 95% confidence the result is real
- Industry standard in statistics

---

## 3. Linear Regression

### What is it?
A way to predict one value based on others using a line.

### The Equation
```
PREDICTION = Constant + (Coefficient × Feature1) + (Coefficient × Feature2)...

Win% = 0.50 + (0.003 × Offensive Rating) + (-0.001 × Defensive Rating)
```

### How to Read Coefficients
- **Positive coefficient** = More of that feature → Higher prediction
- **Negative coefficient** = More of that feature → Lower prediction
- **Larger absolute value** = Bigger impact

### Example
```
Feature          Coefficient     Interpretation
─────────────────────────────────────────────────
Offensive Rating    +0.002      Every 1 point → +0.002 win%
Defensive Rating    -0.001      Every 1 point → -0.001 win%

In English:
- Improving offense by 1 point = 0.2% more wins
- Improving defense by 1 point = 0.1% more wins
```

---

## 4. R² Score (How Good is the Model?)

### What is it?
Percentage of variation your model explains.

### The Scale
```
0.0            0.5            1.0
└──────────────┴──────────────┘
Very Bad       Decent         Perfect
```

### Interpretation
| R² Score | What It Means |
|----------|--------------|
| 0.90+ | Excellent - Model explains 90%+ of variation |
| 0.70-0.90 | Good - Explains most of the pattern |
| 0.50-0.70 | Fair - Explains about half |
| 0.30-0.50 | Poor - Explanatory value is limited |
| <0.30 | Very Poor - Model not useful |

### Example
```
R² = 0.75 means:
- Model explains 75% of win percentage variation
- Other 25% is from things not in the data
- (Coaching quality, injuries, luck, etc.)
```

---

## 5. MAE (Mean Absolute Error)

### What is it?
Average mistake size in predictions.

### How to Calculate
```
1. Make predictions for all teams
2. Calculate error = |Actual - Predicted|
3. Average all the errors

Example:
Team A: Predicted 60%, Actual 62% → Error = 2%
Team B: Predicted 50%, Actual 48% → Error = 2%
MAE = (2% + 2%) / 2 = 2%
```

### Interpretation
- Good MAE depends on your data
- Lower is always better
- In our case: MAE = 0.155 = 15.5% average error

---

## 6. Hypothesis Testing

### Structure of a Hypothesis
```
Null Hypothesis (H₀):     Teams with high defensive rating win more
Alternative (H₁):         No relationship between defense and wins

Statistical Test:         Correlation + P-value

Decision Tree:
    ↓
Is p < 0.05?
    ├─ YES → Reject null hypothesis ✓
    │        "The relationship is real!"
    │
    └─ NO  → Fail to reject null hypothesis ✗
             "Could just be random luck"
```

### Our Basketball Hypotheses

**Hypothesis 1**: Offensive rating → Wins
- Correlation: +0.023
- P-value: 0.025
- Result: ✓ PROVEN (p < 0.05)

**Hypothesis 2**: 3-point % → Wins
- Correlation: -0.011
- P-value: 0.296
- Result: ✗ NOT PROVEN (p > 0.05)

---

## 7. Feature Engineering

### Why do it?
Raw data isn't always the best for modeling.

### Examples

**Before**: 
- Free throws made: 15
- Free throw attempts: 20
- Interpretation: Hard to compare across teams

**After** (Feature Engineering):
- Free throw percentage: 0.75 (15/20)
- Interpretation: Easy to see this team shoots 75% from line

### Another Example

**Before**:
- Offensive rating: 105
- Defensive rating: 98
- Interpretation: Need to calculate difference mentally

**After**:
- Net rating: 7 (105 - 98)
- Interpretation: Team outscores opponents by 7 per 100 possessions

---

## 8. Data Split: Train vs Test

### Why Split Data?
Prevent "cheating" - model seeing answers before test.

### The Process
```
All Data (100%)
    ↓
    ├─ Training Set (80%)
    │  └─ Use to train/build the model
    │
    └─ Testing Set (20%)
       └─ Use to test how good model is
          (Model hasn't seen this data yet!)
```

### Why This Matters
```
Without splitting:
- Model trains on data
- Tests on same data
- Result: Artificially high accuracy (lying to ourselves!)

With splitting:
- Model trains on training set
- Tests on NEW data (testing set)
- Result: Honest accuracy measure
```

---

## 9. Multicollinearity

### What is it?
When two features are highly correlated with EACH OTHER.

### Why It's a Problem
```
Feature A: Offensive Rating (points/possession)
Feature B: Points per Game

These are basically the same thing!
Adding both to model is redundant.
```

### How to Spot It
Look at correlation heatmap:
- Red squares between features = High correlation
- Blue squares between features = Negative correlation
- Either is potentially a problem

### What to Do
Remove one of the correlated features.

---

## 10. Statistical Significance vs Practical Significance

### Key Difference

**Statistical Significance** (P < 0.05)
- Result is likely real, not random
- But might be tiny effect

**Practical Significance**
- Does the effect size matter in real world?

### Example
```
Test: Does wearing blue jersey affect wins?
Result: Correlation = 0.001, p = 0.04
Interpretation: 
- ✓ Statistically significant (p < 0.05)
- ✗ NOT practically significant (effect is tiny: 0.001)
- Conclusion: Ignore, effect too small to matter
```

---

## Quick Reference Table

| Concept | Range | Good Value | Interpretation |
|---------|-------|-----------|-----------------|
| Correlation | -1 to +1 | 0.5+ | Medium to strong |
| P-value | 0 to 1 | <0.05 | Statistically significant |
| R² Score | 0 to 1 | 0.7+ | Model explains most variation |
| MAE | 0 to ∞ | Lower | Smaller average error |

---

## Common Questions

**Q: What if correlation is 0.5 but p-value is 0.06?**
A: Result is NOT statistically significant (p > 0.05). Could be random. Don't trust it.

**Q: What if R² is 0.4?**
A: Model explains 40% of variation. Other 60% from unmeasured factors.

**Q: Can two independent features both be important?**
A: Yes! Different aspects can both matter. That's why multicollinearity (same feature twice) is bad.

**Q: Why not use 0.01 instead of 0.05 for p-value?**
A: Could, but makes it harder to find real results. 0.05 is the standard balance.

---

## The Big Picture

### Analysis Flow
```
📊 Data
  ↓
🔧 Feature Engineering (make better variables)
  ↓
📈 EDA (see patterns)
  ↓
✅ Hypothesis Testing (prove assumptions)
  ↓
🤖 Building Models (make predictions)
  ↓
📋 Evaluation (check if it works)
  ↓
💡 Insights & Action
```

### Key Principle
**More data + Better features + Good models = Better predictions**

But no model is perfect. Statistics helps us understand:
- What relationships are real
- How much can we trust our predictions
- Where to focus improvement efforts

---

## 🎯 When to Use Each Concept

| Question | Use This | Why |
|----------|----------|-----|
| Do X and Y move together? | Correlation | See relationship |
| Is the relationship real? | P-value | Distinguish luck from signal |
| How good is my predictor? | R² | Measure explanatory power |
| How accurate are predictions? | MAE | Measure prediction error |
| Which features matter most? | Regression coefficients | See impact of each variable |

---

## Practice Problems

**Problem 1** (Correlation)
Your analysis shows: Wins vs 3-point shooters, correlation = 0.65, p = 0.02
- Is it significant? YES (p < 0.05)
- Is it strong? YES (0.65 is strong)
- Conclusion: Higher 3-point shooting → More wins

**Problem 2** (P-value)
Your hypothesis: Tall players win more
Result: correlation = 0.08, p = 0.51
- Is this real? NO (p > 0.05)
- Recommendation: Reject hypothesis

**Problem 3** (R²)
Your model R² = 0.82
- Good or bad? GOOD (explains 82%)
- What's missing? 18% variation from other factors

---

**Master these concepts → You can understand any data analysis! 🚀**
