# Customer Conversion Prediction – Machine Learning Pipeline

This repository contains a full end-to-end machine learning pipeline developed as part of a university Machine Learning course project. The goal of the project was to predict whether a customer would convert (make a purchase) based on demographic information, marketing campaign attributes, and observed engagement behavior.

The project emphasizes **data understanding, feature selection, model comparison, and performance-driven model choice**, rather than treating model selection as a purely theoretical exercise.

---

## Problem Statement

Digital marketing teams need to identify which customers are most likely to convert so they can:
- Allocate advertising budgets more effectively
- Optimize campaign strategies
- Improve return on spend

This project frames conversion prediction as a **binary classification problem**, where the objective is to accurately predict whether a customer converts (`1`) or does not convert (`0`) after exposure to a marketing campaign.

---

## Dataset Overview

- **Source:** Synthetic digital marketing campaign dataset
- **Rows:** ~8,000 customer observations
- **Target Variable:** `Conversion` (binary)
- **Feature Types:**
  - Customer demographics (age, income, gender)
  - Campaign context (channel, campaign type, spend)
  - Behavioral engagement (site usage, email activity, prior purchases)

A detailed schema of both the raw and cleaned datasets is documented in:

- `sample_schema.md`

---

## Data Preparation & Cleaning

Key characteristics of the dataset:
- No duplicate rows
- No missing values
- Consistent data types

Primary preprocessing steps focused on **feature relevance rather than heavy cleaning**:
- Removed operational metadata not predictive of conversion:
  - `AdvertisingPlatform`
  - `AdvertisingTool`
- Retained all behavioral and demographic features
- Encoded categorical variables using one-hot encoding to ensure model compatibility
- Produced a modeling-ready dataset used consistently across all experiments

All preprocessing and validation steps are implemented in:

- `1_EDA_and_Cleaning.ipynb`

---

## Modeling Approach

We treated model selection as an empirical process rather than assuming a single “best” algorithm.

The pipeline includes:
1. Initial exploratory data analysis and baseline expectations
2. Performance comparison across multiple supervised learning models
3. Selection of the final model based on generalization performance

The following models were evaluated:
- Logistic Regression
- K-Nearest Neighbors
- Decision Tree
- Random Forest
- Support Vector Machine
- **XGBoost (Extreme Gradient Boosting)**

Each model was trained and evaluated using consistent train/test splits and comparable metrics.

---

## Final Model Selection: XGBoost

**XGBoost was selected as the final model** due to its superior performance across key metrics, including:
- Overall accuracy
- Precision-recall balance
- Ability to model non-linear feature interactions
- Robustness to correlated input features

### My Primary Contribution

My main contribution to this project was the **development, tuning, and evaluation of the XGBoost model**, including:
- Feature compatibility validation
- Hyperparameter configuration
- Performance benchmarking against alternative models
- Final result visualization and interpretation

This work is implemented in:
- `XGBoost_Model.ipynb` (model training and evaluation)
- `Final_Results_Visualization.ipynb` (performance comparison and insights)

The decision to deploy XGBoost was based strictly on observed performance rather than model complexity or popularity.

---

## Key Takeaways

- Careful feature selection can be more impactful than aggressive data cleansing
- Model performance must drive model choice — not theoretical appeal
- Tree-based ensemble methods (XGBoost) excelled in capturing complex interactions within customer behavior data
- A structured, repeatable pipeline leads to clearer modeling decisions and better interpretability

---

## Notes

This repository is intended as a **project showcase**, not a production-ready ML system.  
The dataset is synthetic and used solely for academic and portfolio purposes.


