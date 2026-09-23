# 📊 Lab 01: Fractional Differentiation & Causal Rolling Indicators
### *Fintech AI Course — Hands-On Lab Walkthrough*

This hands-on lab introduces students to two foundational concepts in Financial Machine Learning:
1. **Fractional Differentiation ($0 < d < 1$)**: Overcoming the dilemma between raw non-stationary prices (hoarding all memory) and stationary returns (total amnesia).
2. **Causal Rolling Indicators & Lookahead Bias Prevention**: Engineering rolling indicators (EMA, Volatility, Z-Scores) without future leakage.

---

## 🚀 Getting Started with `uv`

This repository uses [`uv`](https://github.com/astral-sh/uv) for lightning-fast, reproducible Python environment management.

### 1. Synchronize the Environment
From the **root of the repository**, run:
```bash
uv sync
```
This automatically sets up the isolated virtual environment (`.venv`) with all required quantitative libraries:
- `pandas`, `numpy`, `matplotlib`, `statsmodels`, `scipy`, `ipykernel`

### 2. Launch the Lab Notebook

#### Option A: In VS Code (Recommended)
1. Open [`fractional_differentiation_lab.ipynb`](./fractional_differentiation_lab.ipynb) in VS Code.
2. In the top-right corner, click **Select Kernel** $\rightarrow$ **Python Environments...**
3. Select **`⭐ .venv (Python 3.10+) .venv\Scripts\python.exe`**.
4. Run each cell sequentially!

#### Option B: In Your Web Browser
Run this command from the repository root:
```bash
uv run jupyter lab month-01-tabular-ml/l01-stationarity-fracdiff/fractional_differentiation_lab.ipynb
```
*(Or if you are already inside this directory, run: `uv run jupyter lab fractional_differentiation_lab.ipynb`)*

---

## 🧠 Key Real-Life Analogies Used in this Lab

- **Raw Price ($d=0$) — "Hoarding Every Memory"**:
  Like remembering every single sandwich you ate since 1st grade. Your brain is overwhelmed with accumulated trivia, making it impossible to identify real trends. In AI, this causes non-stationarity and spurious overfitting.
- **Returns / First Difference ($d=1$) — "Severe Amnesia"**:
  Like waking up with total amnesia, only knowing if you feel slightly warmer than 60 seconds ago. You don't remember if you are a freshman or a senior. In AI, this wipes out long-term memory and trend information.
- **Fractional Difference ($0 < d < 1$) — "Smart Student Memory"**:
  A human-like memory decay: remembering today's lecture vividly (100%), yesterday's homework well (40%), last week's chapter somewhat (10%), and letting old noise fade away. This achieves **stationarity** while preserving **predictive memory**.
- **Lookahead Bias / Future Leakage — "Peeking at Tomorrow's Exam Paper"**:
  Scoring 100% on homework by looking at tomorrow's test questions. The model looks genius in testing, but blows up catastrophically in real-world trading.

---

## 📂 Notebook Structure

The notebook (`fractional_differentiation_lab.ipynb`) contains:
1. **Welcome & Student Life Intuition**: Relatable conceptual breakdowns.
2. **Automated 1-Minute SPY Pipeline**: Continuous realistic market feed with intraday volatility.
3. **The Non-Stationarity Trap ($d=0$)**: Price plots and Augmented Dickey-Fuller (ADF) test.
4. **The Amnesia Trap ($d=1$)**: First difference and loss of memory.
5. **Fractional Differentiation Mechanics**: Binomial series expansion weights and decay curves.
6. **The Optimal $d^*$ Trade-Off Curve**: Scanning $d \in [0, 1]$ to balance ADF stationarity vs memory correlation.
7. **Spotting Future Leakage**: Cheating vs Honest indicators visualization.
8. **Engineering 3 Causal Features**: Causal Rolling Volatility, EMA, and Rolling Z-Score.
9. **Automated Causality Verification**: "Shock the Future" unit test proving zero lookahead bias.
