## 📢 Click Behavior on Online Ads - Bayesian Data Analysis in R

This project investigates **what influences users to click on online advertisements** using **Bayesian logistic and probit regression models** via **JAGS** in R. The goal is to understand the impact of user demographics and digital behavior on ad-click probability, using probabilistic modeling, diagnostic evaluation, and predictive comparison.

---

### 🎯 Main Objectives

* Preprocess and simplify the online ad interaction dataset
* Fit Bayesian logistic and probit regression models using JAGS
* Evaluate model fit and performance via DIC, WAIC, and Posterior Predictive Checks (PPC)
* Identify variables most associated with click behavior
* Interpret results and compare model robustness

---

### 🧾 Dataset Description

The dataset contains user information and whether or not they clicked on an ad.

**Selected Features:**

| Feature                    | Description                          |
| -------------------------- | ------------------------------------ |
| `Daily Time Spent on Site` | Time spent on the site (minutes)     |
| `Age`                      | Age of the user (years)              |
| `Area Income`              | Avg. income in user’s region         |
| `Daily Internet Usage`     | Time spent online daily (minutes)    |
| `Gender`                   | 1 = Male, 0 = Female                 |
| `Clicked on Ad` (Y)        | Target: 1 = Clicked, 0 = Not clicked |

**Dropped Columns (high cardinality):**

* `Ad Topic Line`, `City`, `Country`, `Timestamp`

---

### 🔍 Bayesian Modeling Approach

Two models were fitted using **JAGS**:

#### 1️⃣ Logistic Regression Model

```r
logit(pi[i]) <- beta[1] + inprod(X[i, ], beta[2:(p + 1)])
```

#### 2️⃣ Probit Regression Model

```r
pi[i] <- phi(beta[1] + inprod(X[i, ], beta[2:(p + 1)]))
```

* Both models assume:

  * **Bernoulli likelihood** for the binary target (`Clicked on Ad`)
  * **Normal priors** for coefficients
* Log-likelihood tracked for model comparison and diagnostics

---

### 📊 Model Evaluation & Diagnostics

#### ✅ Convergence Checks

* Trace plots and R̂ statistics confirm convergence for all parameters.

#### 📉 Model Comparison

| Metric             | Model 1 (Logistic) | Model 2 (Probit) |
| ------------------ | ------------------ | ---------------- |
| Mean Deviance      | 192.4              | 191.5            |
| Complexity Penalty | 5.529              | 6.041            |
| **DIC**            | 197.9              | **197.6**        |
| **WAIC**           | 8.6                | **4.8**          |
| Std. Error         | 8.4                | 5.6              |

* **Model 2 (Probit)** shows **lower DIC and WAIC**, indicating better generalization and fit.

#### 🔄 Posterior Predictive Checks (PPC)

* Both models closely replicate the observed mean.
* **Model 2** aligns more closely, suggesting a marginally better fit.

---

### 📌 Conclusion

* Key Influencers: **Age**, **Internet Usage**, and **Time Spent on Site**
* Bayesian analysis gives rich insights through posterior distributions.
* **Model 2 (Probit)** performs slightly better in terms of predictive accuracy and interpretability.
* This approach demonstrates the power of probabilistic modeling for behavior prediction in digital marketing.

---

### 👥 Group Members

* Natasha Kayla Cahyadi
* Miecel Alicia Angel J
* Sherly Vaneza
