# ⚖️ Lab 03: Probability Calibration & Dynamic Decision Thresholds
### *Fintech AI Course — Hands-On Lab Walkthrough with CatBoost & Scikit-Learn*

This hands-on lab introduces students to one of the most critical questions in quantitative machine learning:
> **"When a Gradient Boosted Tree model predicts `0.85` for a stock rising, is there actually an 85% probability it will go up?"**

**Almost certainly NOT!**  
Tree-based algorithms (CatBoost, LightGBM, XGBoost) aggressively split leaves to minimize loss. As a result, they output **uncalibrated ranking scores**, not **true posterior probabilities**.

In quantitative finance, sizing positions with the **Kelly Criterion** or managing risk budgets requires **calibrated, mathematically honest probabilities**.

---

## 🚀 Getting Started with `uv`

This repository uses [`uv`](https://github.com/astral-sh/uv) for reproducible Python environment management.

### 1. Synchronize the Environment
From the **root of the repository**, run:
```bash
uv sync
```
This automatically ensures your `.venv` contains all required libraries:
- `catboost`, `scikit-learn`, `pandas`, `numpy`, `matplotlib`, `ipykernel`

### 2. Launch the Lab Notebook

#### Option A: In VS Code (Recommended)
1. Open [`probability_calibration_lab.ipynb`](./probability_calibration_lab.ipynb) in VS Code.
2. In the top-right corner, click **Select Kernel** $\rightarrow$ **Python Environments...**
3. Select **`⭐ .venv (Python 3.10+) .venv\Scripts\python.exe`**.
4. Run each cell sequentially!

#### Option B: In Your Web Browser
Run this command from the repository root:
```bash
uv run jupyter lab month-01-tabular-ml/l03-probability-calibration/probability_calibration_lab.ipynb
```

---

## 🧠 Key Real-Life Student Analogy: The "Overconfident Student"

- **The Overconfident Student (Uncalibrated Model)**:  
  A student boasts before every exam: *"I'm 90% sure I'll get an A+!"* But across the whole year, they only get an A+ **55% of the time**. Their claimed confidence is completely distorted.
- **Why This Destroys Hedge Funds**:  
  Position-sizing formulas (like the Kelly Criterion) calculate how much capital to risk based on $p$. If your model claims $p = 0.85$ when the true win rate is only $0.54$, your fund over-leverages and blows up during regular drawdown periods.
- **The Honest Calibrator**:  
  We fit **Platt Scaling** (logistic sigmoid) and **Isotonic Regression** (monotonic non-parametric transformation) to rescale tree predictions into **statistically honest probabilities**.

---

## 📦 What We Borrow From Labs 01 & 02

To maintain seamless continuity, this lab uses the exact same data pipeline:
1. **1-Minute SPY Market Data**: 780 bars representing 2 realistic trading days (`seed=42`).
2. **The 4 Stationary Causal Features**:
   - `FracDiff_04`: Fractional differenced price with memory ($d=0.40$).
   - `Causal_Vol_30m`: Rolling 30-minute standard deviation of past returns.
   - `Causal_EMA_30m`: 30-minute causal exponential moving average.
   - `Causal_ZScore_30m`: Standardized distance from rolling mean (mean-reversion indicator).
3. **Forward 5-Minute Directional Target ($y$)**: Predicting whether price will be higher 5 minutes into the future ($1 = \text{UP}, 0 = \text{DOWN}$).
4. **Three-Way Chronological Split**:
   - **Train Fold (50%)**: Train base tree model.
   - **Calibration Fold (25%)**: Fit Platt & Isotonic calibrators on out-of-sample scores.
   - **Test Fold (25%)**: Final evaluation on unseen market data.

---

## 📂 Notebook Structure

The notebook ([`probability_calibration_lab.ipynb`](./probability_calibration_lab.ipynb)) contains:
1. **Welcome & Intuition**: The "Overconfident Student" analogy.
2. **Import Tools**: Loading `catboost`, `scikit-learn`, `pandas`, `numpy`, and `matplotlib`.
3. **Ingest SPY Data & Features**: Fast 20-line causal pipeline from Labs 01 & 02.
4. **Define Directional Target ($y$)**: Forward 5-minute directional classification.
5. **Three-Way Chronological Split**: Train / Calibration Holdout / Test with zero leakage.
6. **Train Base CatBoost Model**: Generating raw, uncalibrated probability scores.
7. *(Next step)*: **Reliability Curves & Brier Score**: Measuring the calibration gap.
8. *(Next step)*: **Platt Scaling & Isotonic Regression**: Transforming raw scores into true probabilities.
9. *(Next step)*: **Dynamic Decision Thresholds ($p^*$)**: Accounting for trading fees and risk friction.
