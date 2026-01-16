# Project 3: Customer Churn Prediction (End-to-End ML System)

## Overview
This project demonstrates an end-to-end machine learning pipeline for predicting customer churn.  
The focus is not only on model accuracy, but on building a **production-aware ML system** that respects real-world constraints such as data availability, interpretability, and class imbalance.

---

## Problem Statement
Customer churn directly impacts business revenue.  
The objective of this project is to predict whether a customer is likely to churn based on historical customer data, enabling proactive retention strategies.

---

## Machine Learning Framing
- **Problem Type:** Binary Classification  
- **Target Variable:** `Churn` (Yes / No)  
- **Goal:** Predict churn *before* it happens  

---

## Dataset Description
- Tabular dataset where:
  - Each row represents a customer
  - Each column represents a feature
- The dataset contains demographic details, service usage, account information, and billing data.

---

## Feature Groups (High-Level)
Input features are logically grouped to aid understanding:
- **Demographics**
- **Service Usage**
- **Account Information**
- **Billing & Payment Details**

These features represent information available **before churn occurs**.

---

## Key Design Principles

### 1. Training vs Prediction Time
- The model is trained using historical data where churn outcomes are known.
- During prediction, the model uses only information available at the decision moment.

### 2. Data Leakage Prevention
- Features that depend on post-churn information are excluded.
- Only causal, pre-churn data is used for prediction.

### 3. Real-World Constraints
- **Class imbalance** is addressed using appropriate evaluation metrics.
- **Categorical-heavy features** are carefully encoded to avoid feature explosion.
- **Interpretability** is prioritized to ensure business trust and usability.

---

## Evaluation Metrics
Accuracy alone is insufficient due to class imbalance.

Primary metrics:
- **Recall (Churn Class)**
- **F1-score**

These metrics ensure the model effectively identifies customers at risk of churn.

---

## Project Objective
The goal of this project is to build an ML system that:
- Makes honest, deployable predictions
- Respects data availability and causality
- Can be explained and trusted by non-technical stakeholders

---

## Status
🚧 In Progress — Dataset exploration and preprocessing underway.
