# 🛡️ Membership Inference Attack (TML Assignment 1 – Team 16)

This repository contains our implementation of a **Membership Inference Attack (MIA)** against an image classification model, developed as part of the Trustworthy Machine Learning course at Saarland University.

## 📋 Assignment Goal

The objective was to infer whether a given data sample was part of the training set of a victim model, by observing the model's outputs and internal activations, without access to the original training data.

## 🧠 Our Final Approach: Out-of-Fold Stacked Ensemble

After multiple iterations, our best-performing solution combines:

- 📈 **Feature Extraction**: 30+ features derived from model predictions, gradients, and internal activations (conv5).
- 📊 **Top-50 Feature Selection**: Using `SelectKBest` with ANOVA F-test.
- 🔁 **Stacked Ensembling**:
  - Base models: XGBoost, LightGBM, CatBoost (tuned using Optuna).
  - Meta model: Logistic Regression with ElasticNet penalty.
  - Out-of-fold predictions were used to avoid overfitting.

We optimized the classification threshold to improve TPR at FPR = 0.05, which is critical in security-sensitive applications.

---

## ⚙️ Execution

All code was executed using Google Colab (GPU) due to resource constraints. Full pipeline execution takes approximately 20 minutes.

---

## 📊 Performance Summary

| Metric | Local Score | Leaderboard Score |
|--------|-------------|-------------------|
| AUC | **0.7421** | **0.6506** |
| TPR@FPR=0.05 | **0.1904** | **0.1023** |

---

## 👥 Team 16

- Ahrar Bin Aslam  
- Muhammad Mubeen Siddiqui

---

## 📝 Notes

Some of the approaches we explored and discarded were:
- Only confidence/loss-based thresholding (AUC ≈ 0.5)
- Neural networks (prone to overfitting in this setting)

We focused instead on tree-based model which performed more reliably on MIA features.

---

