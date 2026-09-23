# ⚖️ L03: Probability Calibration & Dynamic Decision Thresholds

### Core Concept: Platt Scaling, Isotonic Regression & Brier Scores
When a Gradient Boosted Decision Tree (LightGBM/XGBoost) outputs a prediction score of `0.85`, does it mean there is actually an 85% chance the market will rise?
**Almost certainly NOT!**

Tree algorithms push leaf predictions toward the extremes (0 and 1) due to aggressive loss minimization. They output **uncalibrated ranking scores**, not **true posterior probabilities**.

In quantitative finance, sizing positions with the **Kelly Criterion** or managing risk budgets requires **calibrated, mathematically honest probabilities**.

---

## 🏛️ Industry Context
* **Scikit-Learn Production Guide**: Official documentation and reliability curves for **Platt Scaling** (logistic sigmoid fitting) and **Isotonic Regression** (non-parametric monotonic regression).

---

## 🎯 Lab Milestones
1. Plot **Reliability Diagrams** (Calibration Curves) for raw LightGBM predictions on SPY.
2. Calculate the **Brier Score** ($BS = \frac{1}{N}\sum (f_t - o_t)^2$) to quantify probability error.
3. Fit Platt Scaling and Isotonic Regression calibrators strictly on validation folds.
4. Establish dynamic decision thresholds ($p^*$) based on transaction fees and volatility regime.
