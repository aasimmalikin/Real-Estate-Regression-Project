# Real Estate Price Prediction – Machine Learning Project

## Overview

This project focuses on building an end-to-end machine learning solution to predict residential property prices using structured real estate data. The objective is to develop a statistically sound, business-relevant regression model and prepare it for production deployment via an API (Flask/FastAPI).

The current implementation achieves:

* **R² score ~ 0.87 on test data**
* **RMSE ~ 28% (relative to average property price)**

These metrics indicate strong explanatory power and reasonable prediction error for a real-world real estate pricing use case, where noise and location-driven variance are inherently high.

---

## Problem Statement

Accurately estimating house prices is critical for:

* Buyers and sellers making informed decisions
* Real estate platforms providing price recommendations
* Financial institutions performing risk assessment

The goal is to predict the **market price of a house** based on a combination of structural, geographical, and categorical features.

---

## Dataset & Features

The dataset consists of residential property records with both numerical and categorical attributes.

### Key Features

* **Bedrooms**
* **Bathrooms**
* **House size / built-up area**
* **City**
* **State** (highly influential geographical feature)
* Additional engineered features derived during preprocessing

### Target Variable

* **Price of the property**

---

## Data Preprocessing & Feature Engineering

Significant effort was invested in preparing the data to meet linear regression assumptions and improve model stability.

### Steps Performed

* Handling missing values
* Outlier detection and treatment using **IQR-based methods**
* Log transformation of skewed target values (price)
* Encoding categorical variables (city, state)
* Feature scaling using **StandardScaler** (fit on training data only)
* Train-test split to ensure unbiased evaluation

> Note: Feature engineering and EDA were intentionally separated from model serialization to maintain clean production artifacts.

---

## Model Selection

### Baseline Model

* **Linear Regression** was selected as the primary model due to:

  * Interpretability
  * Business explainability
  * Strong baseline performance

### Regularization Considerations

* Multicollinearity was analyzed using **Variance Inflation Factor (VIF)**
* Regularized models (e.g., **Lasso**) were evaluated conceptually to address:

  * Feature selection
  * Overfitting risk

---

## Model Evaluation

### Performance Metrics

| Metric     | Value  | Interpretation                                 |
| ---------- | ------ | ---------------------------------------------- |
| R² (Train) | ~0.876 | Good learning of underlying patterns           |
| R² (Test)  | ~0.87  | Strong generalization, minimal overfitting     |
| RMSE       | ~28%   | Acceptable error range for real estate pricing |

### Model Fit Assessment

* **No significant overfitting** (train and test R² closely aligned)
* **Low bias, controlled variance**
* Performance is consistent across major geographies

---

## Model Persistence

The trained model and preprocessing objects (scaler, encoders) are serialized using **pickle** to ensure:

* Reproducibility
* Consistency between training and inference
* Seamless deployment

Artifacts saved:

* Trained regression model
* Feature scaler
* Encoders / feature mappings

---

## Deployment Architecture (Planned / In Progress)

### API Layer

* **FastAPI / Flask** for serving predictions
* REST endpoint accepting JSON input features
* Input validation and preprocessing pipeline

### Inference Flow

1. Client sends property features
2. API applies same preprocessing steps
3. Pickle-loaded model generates prediction
4. Price prediction returned as JSON response

### Deployment Targets

* Local development server
* Cloud deployment (Docker-ready)

```

---

## Business Interpretation

* Location (state and city) plays a dominant role in pricing
* Structural features (size, bedrooms, bathrooms) drive incremental value
* The model provides **explainable predictions**, suitable for stakeholder-facing applications

---


---

## Conclusion

This project demonstrates a complete machine learning lifecycle—from raw data to deployable model—applied to a realistic real estate pricing problem. With an R² of ~0.87 and controlled error levels, the model is production-viable and provides meaningful business value while maintaining interpretability.

---

## Author

**Aasim**
Machine Learning & Data Science Practitioner
