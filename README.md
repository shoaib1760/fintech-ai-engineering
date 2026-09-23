# 🚀 FinTech AI Engineering & Quantitative Research
**Track**: Open-Source Quantitative Engineering & Research Series

---

[![Python 3.10+](https://img.shields.io/badge/python-3.10+-blue.svg)](https://www.python.org/downloads/)
[![Environment: uv](https://img.shields.io/badge/environment-uv-purple.svg)](https://github.com/astral-sh/uv)
[![Code Style: Black](https://img.shields.io/badge/code%20style-black-000000.svg)](https://github.com/psf/black)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

Welcome to the **FinTech AI Engineering & Research** curriculum repository. This repository trains undergraduate engineering students and early-career AI practitioners in **production-grade quantitative machine learning, statistical signal processing, and agentic AI systems** applied to financial markets.

---

## 🎯 The Core Philosophy: Why Most AI Fails in Finance

In standard machine learning courses, students are taught:
> *"Load a CSV, drop missing values, call `model.fit(X, y)`, and check `accuracy_score`."*

In the financial industry, **this naive approach leads to catastrophic bankruptcies**:
* **The Anchor Case Study (Zillow's $500M+ Disaster)**: Zillow shut down its automated home-buying division (*Zillow Offers*) after losing over half a billion dollars. Their tabular ML models failed to account for macroeconomic regime shifts (**non-stationarity**) and contained subtle **lookahead bias (future leakage)** in feature engineering.
* **The Lesson**: Dumping raw price series into machine learning algorithms is financial suicide. Financial AI requires **stationarity preservation**, **strict temporal causality**, **asymmetric risk loss functions**, and **calibrated posterior probabilities**.

This course bridges the gap between academic toy problems and Wall Street production standards.

---

## 📅 Month 1: Quantitative Feature Engineering & Tabular ML

| Module | Core AI Logic Concept | Real-World Industry Context | Lab Milestone & Deliverable |
| :--- | :--- | :--- | :--- |
| [**L01: Stationarity & Features**](./month-01-tabular-ml/l01-stationarity-fracdiff/) | **Fractional Differentiation ($0 < d < 1$)** & Causal Rolling Indicators | *How to Lose $500 Million with Algorithms (Zillow Case Study)* | [Interactive Lab 01](./month-01-tabular-ml/l01-stationarity-fracdiff/fractional_differentiation_lab.ipynb): 1-min SPY pipeline, $(1-B)^d$ binomial filter, ADF testing, causal volatility, and zero-leakage unit test suite. |
| [**L02: Cost-Sensitive Loss**](./month-01-tabular-ml/l02-cost-sensitive-loss/) | **Asymmetric Utility Matrices** & Custom Focal Loss | *Kaggle Grandmaster Forums: Why AUC is Useless in Financial Trading* | Train LightGBM & CatBoost models on SPY directional forecasts using custom asymmetric loss penalizing drawdown errors. |
| [**L03: Probability Calibration**](./month-01-tabular-ml/l03-probability-calibration/) | **Platt Scaling**, Isotonic Regression & Dynamic Decision Thresholds | *Scikit-Learn Production Guide: Reliability Diagrams for High-Stakes ML* | Transform gradient-boosted tree logits into true posterior probabilities; evaluate with Brier score and reliability curves. |
| [**L04: Explainability & Baselines**](./month-01-tabular-ml/l04-explainability-shap/) | **TreeSHAP Attributions** & Fuzzy Logic Benchmarking | *Scott Lundberg's SHAP: Why Global Feature Importance Fails Audits* | Extract local and global SHAP attributions for top SPY technical drivers; benchmark against a rule-based Fuzzy Logic system. |

---

## 🔰 Absolute Beginner Setup Guide (Zero-to-Hero)

> **No prior experience setting up Python or terminals?**  
> Follow these 5 foolproof steps. You do not need to install Python manually—our package manager (`uv`) does everything automatically!

---

### Step 1: Install the Free Prerequisites
If you don't already have them, download and install:
1. **VS Code (Code Editor)**: [Download for Windows/Mac](https://code.visualstudio.com/Download)
2. **Git (Version Control)**: [Download Git](https://git-scm.com/downloads)
3. In VS Code, install the **Python** and **Jupyter** extensions from the Extensions tab (`Ctrl + Shift + X`).

---

### Step 2: Install `uv` (The Modern Fast Python Manager)
We use **`uv`**, the world's fastest Python manager. It will automatically download Python, manage virtual environments, and install libraries with zero configuration headache.

* **On Windows (Open PowerShell as normal user and paste)**:
  ```powershell
  powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
  ```
* **On Mac or Linux (Open Terminal and paste)**:
  ```bash
  curl -LsSf https://astral.sh/uv/install.sh | sh
  ```
* *After running the command, close and reopen your PowerShell/Terminal window.*

---

### Step 3: Clone This Repository
Open your Terminal or PowerShell and run:
```bash
git clone https://github.com/shoaib1760/fintech-ai-engineering.git
cd fintech-ai-engineering
```

---

### Step 4: One-Click Environment Synchronization
Run this single command inside the project directory:
```bash
uv sync
```
✨ **What `uv sync` does automatically**:
1. Downloads the correct Python version (CPython 3.10+).
2. Creates an isolated virtual environment (`.venv`).
3. Installs all required quantitative packages (`pandas`, `numpy`, `matplotlib`, `statsmodels`, `scipy`, `lightgbm`, `catboost`, `scikit-learn`, `shap`, `jupyterlab`).
4. **No manual `pip install` or version conflicts!**

---

### Step 5: Open and Run the First Lab in VS Code!
1. Open the repository folder in VS Code:
   ```bash
   code .
   ```
2. In the left file explorer, open:
   👉 `month-01-tabular-ml/l01-stationarity-fracdiff/fractional_differentiation_lab.ipynb`
3. In the **top-right corner** of the notebook:
   - Click **Select Kernel** $\rightarrow$ **Python Environments...**
   - Click the row that has the star: **`⭐ .venv (Python 3.10+) .venv\Scripts\python.exe`**.
4. Press `Shift + Enter` to run each cell one by one! Every cell prints plain-English explanations, outputs, and graphs.

---

### 🌐 Alternative: Running Jupyter in Your Web Browser
If you prefer using Jupyter Lab in your browser instead of VS Code, just run:
```bash
uv run jupyter lab
```
Your browser will open automatically with all notebooks and dependencies pre-loaded!

---

## ❓ Student Troubleshooting FAQ

<details>
<summary><b>Q1: VS Code says <code>ModuleNotFoundError: No module named 'numpy'</code></b></summary>
<p>
This happens if VS Code is running against your computer's default global Python instead of the course's <code>.venv</code> environment.
<br><b>Fix</b>: Look at the top-right corner of the notebook. Click the Python version button, choose <b>Python Environments...</b>, and select the <b><code>.venv</code></b> option. Then click the <b>Restart 🔄</b> button on the notebook toolbar.
</p>
</details>

<details>
<summary><b>Q2: Windows PowerShell says <code>Running scripts is disabled on this system</code></b></summary>
<p>
Windows has a safety restriction for running scripts.
<br><b>Fix</b>: Open PowerShell and run:
<code>Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser</code>
Then press <code>Y</code> and press Enter.
</p>
</details>

<details>
<summary><b>Q3: What does "Zero Future Leakage" mean?</b></summary>
<p>
Future leakage (or lookahead bias) happens when an indicator at minute $t$ accidentally uses data from minute $t+1, t+2, \dots$. In simulation, the AI achieves 99% accuracy because it's peeking at tomorrow's test paper. In real life, it crashes and loses all money. All features in this curriculum are guaranteed to be strictly causal.
</p>
</details>

---

## 🤝 Contributing & Open-Source Community
This repository is developed for educational and quantitative research purposes. Practitioners, students, and engineers are encouraged to fork, submit issues, and build open-source portfolios.

* **Discussions & Issues**: Feel free to open an issue or pull request on GitHub.
* **License**: MIT Open Source.
