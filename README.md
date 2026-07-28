# Nonparametric Survival Analysis in R  
### Kaplan–Meier Estimation of Time to Leukemia Relapse

This repository contains an R-based analysis of **time-to-event clinical trial data** using **nonparametric survival analysis methods**.

The project demonstrates how to analyze **right-censored medical data**, estimate survival probabilities using the **Kaplan–Meier estimator**, and compare treatment groups in a leukemia clinical trial dataset.

The analysis was conducted as part of the **Advanced Health Data Analysis – Survival Analysis course (2025/26)**.

---

# Project Overview

The objective of this project is to demonstrate core techniques used in **biostatistics and health data science**, including:

- exploratory analysis of clinical time-to-event data  
- handling **right-censored observations**  
- estimation of survival functions  
- comparison of treatment groups  
- visualization of survival curves and hazard functions  

The analysis evaluates whether a **6-MP treatment improves time until leukemia relapse compared to a control group**.

---

# Dataset

The dataset represents a **clinical trial on leukemia relapse**.

Variables:

| Variable | Description |
|--------|-------------|
| `pair` | Patient pair identifier |
| `time` | Time until relapse (weeks) |
| `cens` | Relapse indicator (event vs censored) |
| `treat` | Treatment group (Control or 6-MP) |
| `status` | Disease stage |

Key characteristics:

- **42 observations**
- **Right-censored survival data**
- Two treatment groups (Control vs 6-MP)

---

# Methods

## Survival Object

The analysis uses the `Surv()` object from the **survival** package to encode time-to-event data and censoring information.

```r
library(survival)

srem <- with(remission, Surv(time, cens))
```

Right-censored observations are automatically handled within this structure.

---

## Kaplan–Meier Estimation

The survival function \(S(t)\) is estimated using the **Kaplan–Meier estimator**:

```r
svf <- survfit(srem ~ 1)
summary(svf)
```

Outputs include:

- survival probability estimates
- number of individuals at risk
- number of events
- confidence intervals
- median survival time

---

## Treatment Comparison

Survival curves are estimated separately for each treatment group:

```r
svf2t <- survfit(srem ~ treat, data = remission)
summary(svf2t)
```

This allows comparison of relapse times between:

- Control group
- 6-MP treatment group

---

# Visualization

The repository includes several visualizations:

### Kaplan–Meier Survival Curves

```r
plot(svf2t,
     col = 3:4,
     lwd = 3,
     xlab = "Time to relapse [Weeks]",
     ylab = expression(bolditalic(hat(S)(t))))
legend("bottomleft", levels(remission$treat), col = 3:4, lwd = 3)
```

### Additional Plots

The project also visualizes:

- survival functions \(S(t)\)
- cumulative distribution functions \(F(t)\)
- cumulative hazard functions \(\Lambda(t)\)

These plots help interpret how relapse risk evolves over time under different treatments.

---

# Key Insights

Exploratory analysis shows:

- the **6-MP treatment group has longer follow-up times**
- the **control group survival curve drops to zero**, indicating relapse events for all patients
- the treatment group maintains higher survival probabilities

This suggests a **potential beneficial treatment effect**, which motivates further modeling (e.g., Cox regression).

---

# Technologies Used

- **R**
- `survival`
- `Hmisc`

Optional visualization improvements:

- `survminer`

---

# Repository Structure

```
survival-analysis-kaplan-meier/
│
├── Nonparametric_estimation_survival_function.qmd
├── Ahda_RLab1.RData
├── plots/
└── README.md
```

---

# Skills Demonstrated

This project demonstrates practical skills used in **health data science and clinical analytics**:

- survival analysis
- Kaplan–Meier estimation
- handling censored medical data
- clinical trial data exploration
- statistical programming in R
- reproducible analysis using Quarto

---

# Potential Extensions

Future analyses could include:

- Cox proportional hazards modeling
- log-rank test for survival differences
- bootstrapped survival estimates
- integration with real-world clinical datasets

---

# Author

Johanna Albers  
Data Science / Health Data Analytics| `status` | Disease stage |

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
## Reproducing this analysis

Install the dependencies with `setup.R` (R)

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
