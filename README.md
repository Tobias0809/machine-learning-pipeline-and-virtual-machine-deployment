# Machine-Learning-Pipeline and Deployment on a virtual machine

This repository contains the solution for **Assignment 2** of the *Big Data Management* course.  
The project focuses on building an end-to-end **machine learning pipeline** for wind power prediction, following the **data analytics lifecycle** and emphasizing **reproducibility, scalability, and proper evaluation**.

**Note**: The problem statement and a report for the assignment can be found in the folder Project Overview

---

## Project Overview

The goal of this assignment is to design, train, evaluate, and deploy a predictive model for wind power production based on historical weather and power generation data.  
The solution combines data preprocessing, feature engineering, model experimentation, and deployment using modern ML best practices.

Key aspects include:
- Time-series aware data preparation
- Physically meaningful feature engineering
- Experiment tracking with MLflow
- Reproducible ML pipelines
- Local and cloud-ready model serving


---

## Data

The project uses three datasets:
- **Historical power production data**
- **Historical weather forecast data**
- **Future weather forecast data**

A major challenge is the mismatch in temporal resolution:
- Power data: **1-minute intervals**
- Weather data: **3-hour intervals**

To address this:
- Power data is aggregated to a 3-hour frequency
- Datasets are merged on aligned timestamps
- Rows with missing target values at the beginning of the series are removed

---

## Feature Engineering

Wind direction is encoded using **u/v vector components** derived from wind speed and direction.

This representation:
- Preserves the physical meaning of wind as a 2D vector
- Avoids artificial discontinuities at 0° / 360°
- Improves model robustness compared to categorical or angle-based encoding

Final numerical features include:
- Wind speed
- Wind vector components (u, v)

---

## Machine Learning Pipeline

The solution is implemented using a **scikit-learn Pipeline**, ensuring consistent preprocessing and preventing data leakage.

Pipeline components:
1. **StandardScaler** for numerical feature scaling
2. **Regression model** (Random Forest or Gradient Boosting)

The dataset is split **chronologically** to respect temporal dependencies:
- 64% training
- 16% validation
- 20% test

---

## Models and Experiments

Two ensemble-based regression models are evaluated:
- **Random Forest Regressor**
- **Gradient Boosting Regressor**

These models are chosen due to:
- Their ability to capture non-linear relationships
- Robust performance on structured tabular data

Hyperparameter tuning is performed using **RandomizedSearchCV**.

---

## Evaluation

Models are evaluated using standard regression metrics:
- **MSE** (Mean Squared Error)
- **RMSE** (Root Mean Squared Error)
- **MAE** (Mean Absolute Error)

RMSE is used as the primary comparison metric due to its interpretability in the target unit (MW).

---

## Experiment Tracking

All experiments are tracked using **MLflow**, including:
- Model parameters
- Evaluation metrics
- Trained models and artifacts

This ensures:
- Full reproducibility
- Transparent model comparison
- Easy rollback and deployment

---

## Model Serving and Deployment

The best-performing model is:
1. Logged to MLflow
2. Served locally via a REST API
3. Prepared for deployment on a cloud-based virtual machine

This demonstrates the full ML lifecycle from data to production-ready model.

---

## Key Takeaways

- Time-aware data handling is critical for predictive modeling
- Feature representations grounded in domain knowledge improve performance
- Pipelines and experiment tracking are essential for reproducible ML
- MLflow simplifies model management and deployment

