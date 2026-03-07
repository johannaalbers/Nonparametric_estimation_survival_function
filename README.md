# Survival Analysis of Clinical Trial Data (Kaplan–Meier Estimation)

This repository contains an end-to-end analysis of clinical time-to-event data using **nonparametric survival analysis methods in R**.  
The project demonstrates how to estimate survival functions, handle right-censored observations, and compare treatment effects in a clinical trial setting.

The analysis uses a leukemia clinical trial dataset and focuses on **time to relapse under different treatments**.

---

# Project Objectives

The goal of this project is to demonstrate key techniques used in **health data science and clinical research**, including:

- Survival analysis of time-to-event outcomes
- Handling **right-censored clinical data**
- Estimating survival probabilities using the **Kaplan–Meier estimator**
- Comparing treatment groups using survival curves
- Visualizing survival functions, cumulative hazard functions, and event distributions
- Interpreting clinical outcomes from statistical models

This project illustrates common workflows used in **biostatistics, epidemiology, and real-world health data analysis**.

---

# Dataset

The dataset originates from a clinical trial investigating **leukemia relapse under two treatment arms**.

Variables include:

| Variable | Description |
|--------|-------------|
| `pair` | Patient pair ID |
| `time` | Time until relapse (weeks) |
| `cens` | Relapse indicator (event vs censored) |
| `treat` | Treatment group (Control vs 6-MP) |
| `status` | Disease stage |

The dataset contains **42 observations** and includes **right-censored follow-up times**, a common challenge in clinical research.

---

# Methods

## Survival Object Construction

Time-to-event data is represented using the `Surv()` object from the `survival` package.

```r
library(survival)

srem <- Surv(time, cens)
```

This object encodes both event times and censoring information.

---

## Kaplan–Meier Estimation

The survival function \(S(t)\) is estimated nonparametrically using the Kaplan–Meier estimator.

```r
svf <- survfit(srem ~ 1)
summary(svf)
```

Outputs include:

- survival probability estimates
- number at risk
- number of events
- confidence intervals
- median survival time

---

## Treatment Comparison

Survival curves are estimated separately for treatment groups.

```r
svf2t <- survfit(srem ~ treat, data = remission)
```

This allows comparison of survival distributions between:

- Control group
- 6-MP treatment group

Differences in survival curves provide insight into the **treatment effectiveness on relapse time**.

---

# Visualization

Kaplan–Meier curves are plotted to visualize survival probabilities over time.

```r
plot(
  svf2t,
  col = 3:4,
  lwd = 3,
  xlab = "Time to relapse [Weeks]",
  ylab = expression(bolditalic(hat(S)(t)))
)
legend("bottomleft", levels(remission$treat), col = 3:4, lwd = 3)
```

Additional visualizations include:

- Survival functions \(S(t)\)
- Cumulative incidence functions \(F(t)\)
- Cumulative hazard functions \(\Lambda(t)\)

These plots provide intuitive insight into how relapse risk evolves over time.

---

# Additional Analysis

The project also compares:

- **Kaplan–Meier estimator**
- **Nelson–Aalen estimator**

```r
svf2tNA <- survfit(srem ~ treat, remission, stype = 2, ctype = 1)
```

Comparing estimators helps evaluate differences in survival function estimation approaches.

---

# Technologies

- **R**
- `survival`
- `Hmisc`
- `survminer` (optional visualization improvements)

---

# Key Skills Demonstrated

This project demonstrates practical skills relevant for **health data science and biostatistics**, including:

- Survival analysis
- Handling censored clinical data
- Kaplan–Meier modeling
- Clinical trial data interpretation
- Statistical programming in R
- Data visualization for biomedical research

---

# Repository Structure

```
survival-analysis-project/
│
├── data/
│   └── remission_dataset.RData
│
├── scripts/
│   └── survival_analysis.R
│
├── plots/
│   └── survival_curves.png
│
└── README.md
```

---

# Potential Extensions

Future improvements could include:

- Cox proportional hazards modeling
- Log-rank tests for treatment comparison
- Bootstrapped survival estimates
- Integration with real-world clinical datasets

---

# Author

Johanna Albers  
Data Science / Health Data Analytics
