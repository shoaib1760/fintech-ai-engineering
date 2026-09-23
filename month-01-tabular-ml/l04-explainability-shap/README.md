# 🔍 L04: Explainability, TreeSHAP & Fuzzy Logic Benchmarking

### Core Concept: Local/Global Feature Attribution & Rule-Based Benchmarking
Financial algorithms operating in institutional markets must comply with risk compliance (FINRA, SEC, Basel III). "The neural network told me to buy" is legally unacceptable during an audit after a major loss.

We need **individualized, trade-by-trade explainability**:
* Which specific feature (e.g., Fractional Diff $d=0.4$ vs 30-min Volatility) drove this specific long trade?
* How does our ML model's decision surface compare against a classical rule-based **Fuzzy Logic control system**?

---

## 🏛️ Industry Context
* **Scott Lundberg's SHAP**: The original author's paper and blog explaining why global feature importance (e.g., Gini impurity or split count) fails regulatory scrutiny compared to game-theoretic Shapley values.

---

## 🎯 Lab Milestones
1. Compute exact Shapley values using **TreeSHAP** on the calibrated SPY directional classifier.
2. Generate summary plots (global feature importance) and force plots (local trade attribution).
3. Build a baseline **Fuzzy Logic inference engine** using simple triangular membership functions for trend, volatility, and volume.
4. Benchmark the decision boundaries of Tabular ML vs Fuzzy Logic.
