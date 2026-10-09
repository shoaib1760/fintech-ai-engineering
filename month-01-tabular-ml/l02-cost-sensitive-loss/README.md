# 📉 Lab 02: Cost-Sensitive Loss & Asymmetric Financial Risk
### *Fintech AI Course — Hands-On Lab Walkthrough with CatBoost*

This hands-on lab introduces students to one of the most important concepts in algorithmic trading:
> **Why do machine learning models with high accuracy or AUC still lose money in live trading?**

Standard machine learning objectives (Log-Loss, Cross-Entropy, Accuracy) treat all errors symmetrically. In this lab, we use **CatBoost** to build **cost-sensitive models** that penalize catastrophic downside errors (buying before a price crash) much more severely than harmless false alarms.

---

## 🚀 Getting Started with `uv`

This repository uses [`uv`](https://github.com/astral-sh/uv) for reproducible Python environment management.

### 1. Synchronize the Environment
From the **root of the repository**, run:
```bash
uv sync
```
This automatically ensures your `.venv` contains all required libraries:
- `catboost`, `pandas`, `numpy`, `matplotlib`, `ipykernel`

### 2. Launch the Lab Notebook

#### Option A: In VS Code (Recommended)
1. Open [`cost_sensitive_loss_lab.ipynb`](./cost_sensitive_loss_lab.ipynb) in VS Code.
2. In the top-right corner, click **Select Kernel** $\rightarrow$ **Python Environments...**
3. Select **`⭐ .venv (Python 3.10+) .venv\Scripts\python.exe`**.
4. Run each cell sequentially!

#### Option B: In Your Web Browser
Run this command from the repository root:
```bash
uv run jupyter lab month-01-tabular-ml/l02-cost-sensitive-loss/cost_sensitive_loss_lab.ipynb
```

---

## 🧠 Key Real-Life Student Analogy

- **The False Alarm (Minor Friction)**:  
  You packed an umbrella because you predicted rain, but it stayed cloudy.  
  *Cost*: Minor annoyance carrying an umbrella (like paying a $1 brokerage fee on a flat trade).
- **The Catastrophic Error (Fund Liquidation)**:  
  You predicted clear skies, left your laptop out in the yard, and a flash thunderstorm destroyed your entire thesis project.  
  *Cost*: Complete wipeout (like buying stock right before a -4% crash, triggering margin call/liquidation).
- **Cost-Sensitive Learning (CatBoost)**:  
  We configure CatBoost's penalty weights (`class_weights=[1.8, 1.0]`) so that buying before a price crash is penalized significantly harder than missing a flat trade, avoiding both reckless overtrading and "risk paralysis".

---

## 📦 What We Borrow From Lab 01

To keep this lab focused and beginner-friendly, we bring in three core components from **Lab 01**:
1. **1-Minute SPY Market Data**: 780 bars representing 2 realistic trading days.
2. **The 4 Stationary Causal Features**:
   - `FracDiff_04`: Fractional differenced price with memory ($d=0.40$).
   - `Causal_Vol_30m`: Rolling 30-minute standard deviation of past returns.
   - `Causal_EMA_30m`: 30-minute causal exponential moving average.
   - `Causal_ZScore_30m`: Standardized distance from rolling mean (mean-reversion indicator).
3. **Strict Chronological Train/Test Split**: Day 1 for training (60%), Day 2 for testing (40%). Zero lookahead shuffling.

---

## 📂 Notebook Structure

The notebook ([`cost_sensitive_loss_lab.ipynb`](./cost_sensitive_loss_lab.ipynb)) contains:
1. **Welcome & Intuition**: The umbrella vs. laptop disaster analogy.
2. **Import Tools**: Loading `catboost`, `pandas`, `numpy`, and `matplotlib`.
3. **Causal Feature Pipeline**: Fast 20-line generation of the Lab 01 features.
4. **Target Formulation ($y$)**: Predicting forward 5-minute price direction ($1 = \text{UP}, 0 = \text{DOWN}$).
5. **Chronological Splitting**: Train on Day 1, Test on Day 2 with zero leakage.
6. **Model 1 (Baseline CatBoost)**: Standard symmetrical Log-Loss.
7. **Model 2 (Cost-Sensitive CatBoost)**: Asymmetric penalty on downside errors via `class_weights` (balanced to avoid risk paralysis).
8. **Equity Curve & PnL Backtest**: Visual side-by-side comparison proving how cost-sensitive learning protects against drawdowns.
9. **Summary & Takeaways**: Key lessons preparing students for Lab 03 (Probability Calibration).
