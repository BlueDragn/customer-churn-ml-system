# 📘 Project 3 — Conceptual Study Notes  
## Customer Churn Prediction (End-to-End ML System)

---

## 1. Project Overview

**Project 3** focuses on building an **end-to-end, production-aware machine learning system**, not just training a model in a notebook.

The objective is to understand:
- How ML problems are framed in real life
- How data is used responsibly
- How constraints shape ML system design

This project emphasizes **thinking like an ML engineer**.

---

## 2. Problem Statement

The problem addressed is **Customer Churn Prediction**.

- **Churn**: When a customer leaves the service
- **Goal**: Predict churn *before it happens*
- **Business Value**: Enables proactive retention actions

This is a **binary classification problem**.

---

## 3. Dataset Structure

- The dataset is **tabular**
- **Rows** represent customers
- **Columns** represent features and the target
- **Target column**: `Churn` (Yes / No)

---

## 4. Input Features (High-Level View)

Input features are grouped by **meaning**, not listed column-by-column initially.

### Feature Categories

- **Demographics**  
  Who the customer is (e.g., personal attributes)

- **Service Usage**  
  What services the customer uses

- **Account Information**  
  Relationship with the company (tenure, contract)

- **Billing & Payment**  
  How much and how the customer pays

This high-level grouping helps understand the problem before implementation.

---

## 5. High-Level vs Low-Level Thinking

- **High-Level**: Feature categories and problem framing (Step 1)
- **Low-Level**: Column-wise analysis, data types, cleaning (Step 2)

Details are intentionally delayed to avoid premature design mistakes.

---

## 6. Training Time vs Prediction Time (Critical Concept)

### Training Time
- Historical data
- Churn outcome is known
- Used to learn patterns

### Prediction Time
- Only active customers
- Churn has not happened yet
- Model must rely only on data available *before churn*

---

## 7. Core Rule (Non-Negotiable)

> **The model must use only data that exists before churn happens.**

- Churned customers → included in training
- Churn status → used as label
- Post-churn information → excluded from features

---

## 8. Data Leakage

**Data leakage** occurs when future or outcome-dependent information is used during training.

### Why it is dangerous
- Artificially high accuracy
- Model learns shortcuts
- Fails in production

**Key principle:**

> Causes → Allowed  
> Consequences → Forbidden

---

## 9. Why Using Post-Churn Data Is Cheating

Even if post-churn data exists only for churned customers:

- The *existence or absence* of such data reveals the label
- The model learns “who already churned”
- Predictions fail for real, active customers

---

## 10. Key Constraints of the Problem

These constraints define the **real-world boundaries** of the system.

---

### Constraint 1: Class Imbalance

- Majority of customers do not churn
- Accuracy becomes misleading

**Implications:**
- Focus on Recall (churn class)
- Use F1-score
- Evaluate missed churners, not just correct predictions

---

### Constraint 2: Categorical-Heavy Dataset

- Many features are non-numeric
- Encoding is required

**Risks:**
- Feature explosion from one-hot encoding
- Increased overfitting and complexity

---

### Constraint 3: Interpretability Requirement

- Business users need explanations
- Black-box models reduce trust

**Implications:**
- Prefer simple, explainable models
- Use intuitive and defensible features

---

## 11. Feature Explosion

Occurs when categorical encoding causes:

- 1 column → many columns

This leads to:
- Overfitting
- Slow training
- Poor interpretability

**Rule of thumb:**
- Few categories → safe  
- Many categories → handle carefully

---

## 12. Model Learning Philosophy

The model learns:

> “When customers looked like *this* **before churn**, they later churned.”

It does **not** learn:
> “Customers who already churned have these values.”

---

## 13. Final Mental Model

> The model learns from **past customers**, using only information that existed **before churn**, to predict churn for **current customers**.

---

## 14. Key Takeaway

**Project 3 is about building an ML system that:**
- Makes honest, deployable predictions
- Respects time, causality, and data availability
- Operates under real-world constraints

This is the foundation of production-grade machine learning.

# 📁 Project 3 — Folder Structure

Explain **why each folder and file exists** in the project.  
The goal is to understand the structure, not just memorize it.

---

## Root Directory: `customer-churn-ml-system/`

This is the **project boundary**.  
Everything inside this folder belongs to **one machine learning system**.

---

## 📊 `data/` — Dataset Managementdata/
```
data/
├── raw/
└── processed/
```

### `data/raw/`
- Contains the original, untouched dataset
- Acts as the **source of truth**
- Never modified directly

### `data/processed/`
- Stores cleaned and transformed data
- Output of preprocessing and feature engineering

⚠️ Both `raw/` and `processed/` are ignored by Git.  
The dataset source is documented in the README instead.

---

## 📓 `notebooks/` — Exploration & Analysis
```
notebooks/
└── eda.ipynb
```


Purpose:
- Exploratory Data Analysis (EDA)
- Visualizing patterns
- Testing ideas and assumptions

Rules:
- No production code
- No final pipelines
- No model artifacts

Notebooks are a **thinking space**, not part of the final system.

---

## 🧠 `src/` — Core ML Logic
```
src/
├── init.py
├── data_preprocessing.py
├── feature_engineering.py
├── train.py
└── evaluate.py
```


This folder contains **all reusable and production-ready code**.

### `data_preprocessing.py`
- Handles missing values
- Cleans data types
- Converts raw data into usable format

### `feature_engineering.py`
- Encodes categorical variables
- Creates and transforms features
- Prevents data leakage

### `train.py`
- Splits data into train/validation sets
- Trains machine learning models
- Saves trained model artifacts

### `evaluate.py`
- Evaluates model performance
- Computes metrics (Recall, F1-score, etc.)
- Validates model behavior

---

## 🧪 `model/` — Trained Model Artifacts
```
model/
└── model.pkl
```


- Stores trained model files
- Generated by training scripts
- Ignored by Git to keep the repository lightweight

Models can always be regenerated from code.

---

## 🌐 `api/` — Model Serving Layer
```
api/
├── init.py
└── main.py
```

Purpose:
- Serve the trained model via FastAPI
- Accept customer data as input
- Return churn predictions

This folder converts the ML model into a **usable system**.

---

## 🪵 `logs/`

- Stores training logs and debugging information
- Helps track experiments and failures
- Ignored by Git

---

## 🧪 `tests/`

- Placeholder for unit and integration tests
- Demonstrates testing awareness
- Even an empty folder is a positive signal

---

## ⚙️ Configuration & Metadata Files

### `.gitignore`
- Prevents committing:
  - Data files
  - Model artifacts
  - Virtual environments
  - Logs and OS files

Keeps the repository clean and professional.

---

### `requirements.txt`
- Lists Python dependencies
- Enables reproducible environments
- Allows easy project setup using:
  ```bash
  pip install -r requirements.txt
### README.md
- Explains project purpose and scope
- Documents design decisions
- Provides instructions to run the project
