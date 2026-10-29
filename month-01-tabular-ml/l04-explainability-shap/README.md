# 🔍 Lab 04: Explainability, TreeSHAP & Feature Attribution
### *Fintech AI Course — Hands-On Lab Walkthrough with TreeSHAP*

This hands-on lab introduces students to the most critical compliance and risk requirement in algorithmic trading:
> **"Why did the machine learning model execute this specific trade at this exact minute?"**

In high-stakes financial institutions (FINRA, SEC, Basel III), *"the black-box neural net told me to buy"* is legally unacceptable during an audit after a major loss. We must provide mathematically honest, trade-by-trade feature attribution.

---

## 🚀 Getting Started with `uv`

This repository uses [`uv`](https://github.com/astral-sh/uv) for fast, reproducible environment management.

### 1. Synchronize the Environment
From the **root of the repository**, run:
```bash
uv sync
```
This ensures your `.venv` contains all required libraries:
- `shap`, `catboost`, `pandas`, `numpy`, `matplotlib`, `ipykernel`

### 2. Launch the Lab Notebook

#### Option A: In VS Code (Recommended)
1. Open [`explainability_shap_lab.ipynb`](./explainability_shap_lab.ipynb) in VS Code.
2. In the top-right corner, click **Select Kernel** $\rightarrow$ **Python Environments...**
3. Select **`⭐ .venv (Python 3.10+) .venv\Scripts\python.exe`**.
4. Run each cell sequentially!

#### Option B: In Your Web Browser
Run this command from the repository root:
```bash
uv run jupyter lab month-01-tabular-ml/l04-explainability-shap/explainability_shap_lab.ipynb
```

---

## 🧠 Key Real-Life Student Analogy: The Doctor Analogy

- **🌍 Global Explainability (The Textbook)**:  
  *"Across 10,000 heart disease patients, which factors matter most overall?"*  
  High blood pressure and cholesterol rank at the top.
- **🎯 Local Explainability (Alex Today at 2:00 PM)**:  
  *"Why did you diagnose Alex with heart disease today?"*  
  His blood pressure was completely normal (+0% risk), but his cholesterol spiked dangerously (+40% risk).
- **In Trading**:  
  - **Global**: Across the entire year, which features drove the model's overall decisions?
  - **Local**: On Monday at 14:15 PM, which specific feature made the AI pull the trigger to buy SPY?

---

## 📦 What We Borrow From Previous Labs

To maintain seamless continuity across the curriculum, this lab uses the exact same data pipeline:
1. **1-Minute SPY Market Data**: 780 bars representing 2 realistic trading days (`seed=42`).
2. **The 4 Stationary Causal Features**:
   - `FracDiff_04`: Fractional differenced price with memory ($d=0.40$).
   - `Causal_Vol_30m`: Rolling 30-minute standard deviation of past returns.
   - `Causal_EMA_30m`: 30-minute causal exponential moving average.
   - `Causal_ZScore_30m`: Standardized distance from rolling mean (mean-reversion indicator).
3. **Forward 5-Minute Directional Target ($y$)**: Predicting whether price will be higher 5 minutes into the future ($1 = \text{UP}, 0 = \text{DOWN}$).
4. **Strict Chronological Train/Test Split**: Day 1 for training (60%), Day 2 for testing (40%). Zero lookahead shuffling.

---

## 📂 Notebook Structure

The notebook ([`explainability_shap_lab.ipynb`](./explainability_shap_lab.ipynb)) contains:
1. **Welcome & Intuition**: The Doctor analogy for Global vs. Local explainability.
2. **Import Tools**: Loading `shap`, `catboost`, `pandas`, `numpy`, and `matplotlib`.
3. **Ingest SPY Data & Features**: Fast 20-line causal pipeline from previous labs.
4. **Define Directional Target ($y$)**: Forward 5-minute directional classification & chronological split.
5. **Train Model & Compute TreeSHAP**: Extracting game-theoretic Shapley values with `shap.TreeExplainer`.
6. *(Next step)*: **Global Attribution**: The SHAP Beeswarm Plot and feature importance rankings.
7. *(Next step)*: **Local Attribution**: Trade-by-trade Waterfall Plot explaining a single buy signal.
8. *(Next step)*: **Feature Interactions**: Volatility vs. Z-Score dependency.
9. *(Next step)*: **Fuzzy Logic Baseline**: Benchmarking the AI decision boundary against transparent human rules.
