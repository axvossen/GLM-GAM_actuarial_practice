# Modeling Insurance Claims Frequency and Severity (MTPL Belgium 1997)

📌 **Course:** LACTU2150 - Statistical Analysis of Insurance Data  
📌 **Project:** Modeling Insurance Claims Frequency and Severity (GLM & GAM)  
📌 **Dataset:** Belgian MTPL portfolio (1997)  

---

## 📖 Project Overview

This project analyzes a Belgian motor third party liability (MTPL) insurance portfolio from the year **1997**.  
Each observation corresponds to a unique policyholder and includes risk factors recorded at the beginning of the policy period.

The objective is to model:

- **Claim frequency** (number of claims)
- **Claim severity** (average amount per claim)

Two modeling approaches are used:

- **Generalized Linear Models (GLM)**
- **Generalized Additive Models (GAM)** with geographic smoothing

---

## 📊 Dataset

The dataset is: mtpl_be.rda


It contains **163,231** policyholders and the following variables:

| Variable | Description |
|---------|-------------|
| `nclaims` | Number of claims filed |
| `exp` | Exposure fraction during 1997 |
| `amount` | Total claim amount (€) |
| `avg` | Average claim amount (`amount / nclaims`), NA if no claim |
| `coverage` | Coverage type: TPL / PO / FO |
| `fuel` | Fuel type: gasoline / diesel |
| `sex` | Policyholder gender |
| `use` | Vehicle use: private / work |
| `fleet` | Fleet vehicle: yes / no |
| `ageph` | Policyholder age |
| `power` | Vehicle horsepower (kW) |
| `agec` | Vehicle age |
| `bm` | Bonus-malus level (0–22) |
| `long` | Longitude of municipality center |
| `lat` | Latitude of municipality center |

---

## 🎯 Objectives

### 1. Frequency Modeling
Model the number of claims `nclaims` using a **Poisson regression** with a **log-link**, including exposure as an offset:

\[
\log(E[nclaims]) = X\beta + \log(exp)
\]

### 2. Severity Modeling
Model the average claim amount `avg` using a **Gamma regression** with a **log-link**:

\[
\log(E[avg]) = X\beta
\]

---

# 🧪 Part 1 — GLM Analysis

## 1. Data Preparation
- Convert categorical variables into factors:
  - `coverage`, `fuel`, `sex`, `use`, `fleet`
- Bin continuous variables:
  - `ageph`, `agec`, `power`, `bm`

## 2. Exploratory Data Analysis (EDA)
Produce one plot per feature showing relative frequencies for:

- `coverage`
- `fuel`
- `sex`
- `use`
- `fleet`
- `ageph`
- `power`
- `agec`
- `bm`

## 3. Frequency Model (Poisson GLM)
- Fit a Poisson GLM to predict `nclaims`
- Use `exp` as an offset
- Exclude geographic variables (`long`, `lat`)

Feature selection must be based on:
- AIC
- ANOVA (nested model comparison)
- k-fold cross-validation

## 4. Severity Model (Gamma GLM)
- Fit a Gamma GLM to predict `avg`
- Exclude geographic variables (`long`, `lat`)

Feature selection must be based on:
- AIC
- ANOVA (nested model comparison)
- k-fold cross-validation

## 5. Results & Interpretation
The report must include:
- Selected models and significant predictors
- Coefficients and interpretation of effects
- Model comparison using AIC/BIC, ANOVA tests, and cross-validation
- Plot of the resulting insurance premium as a function of:
  - `ageph`
  - `bm`

---

# 🌍 Part 2 — GAM Analysis (Geographic Smoothing)

## 1. Data Preparation
- Use continuous variables directly (no binning required)
- Include geographic variables:
  - `long`, `lat`

## 2. Frequency Model (Poisson GAM)
Fit a Poisson GAM including smoothing terms:

- Smooth effects for continuous variables:
  - `ageph`, `agec`, `power`, `bm`
- Spatial smoothing:
  - `s(long, lat)`

Model evaluation must include:
- AIC comparison with GLM
- ANOVA tests for smooth terms
- k-fold cross-validation

## 3. GLM vs GAM Comparison
Include:
- Discussion of smoothing impact on performance and interpretation
- Plots of smooth functions:
  - `ageph`
  - `agec`
  - `power`
  - `bm`
  - spatial effect (`long`, `lat`)
