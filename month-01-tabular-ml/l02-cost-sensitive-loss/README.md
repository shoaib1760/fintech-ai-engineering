# 📉 L02: Cost-Sensitive Loss & Asymmetric Financial Risk

### Core Concept: Custom Focal Loss & Asymmetric Utility Matrices
In financial prediction, **not all errors are created equal**:
* **Predicting UP when price moves flat (+0.05%)**: Small transaction fee friction.
* **Predicting UP when price crashes (-4.5%)**: Devastating portfolio drawdown, margin call, or fund liquidation!

Standard machine learning objectives (Log-Loss, Cross-Entropy, MSE, AUC) treat all mistakes symmetrically. In this lab, we build **asymmetric loss functions** that map machine learning gradients directly to a financial expected-value utility matrix.

---

## 🏛️ Industry Context
* **Kaggle Grandmaster Forums**: Curated discussions on why optimizing for standard AUC is useless in financial trade execution without mapping predictions to an asymmetric utility matrix.

---

## 🎯 Lab Milestones
1. Formulate the financial utility matrix:
   $$\text{Utility} = P(\text{Up}) \cdot \text{Gain} - P(\text{Down}) \cdot \text{Loss} - \text{Slippage}$$
2. Implement custom first- and second-order gradients (`grad`, `hess`) for LightGBM and CatBoost.
3. Train directional baseline classifiers on engineered 1-minute SPY features from Lab 01.
4. Compare PnL curves: Standard Log-Loss vs Cost-Sensitive Focal Loss.
