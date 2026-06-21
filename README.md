# Adaptive Conformal Inference and AgACI for Financial Volatility Forecasting

This repository contains a group project developed for the **Time Series and Financial Time Series** course at **Sapienza University of Rome**.

The project investigates the problem of **uncertainty quantification in financial volatility forecasting** through the application of **Adaptive Conformal Inference (ACI)** and **Aggregated Adaptive Conformal Inference (AgACI)**.

While a large literature focuses on producing accurate volatility forecasts, obtaining reliable measures of uncertainty remains considerably more challenging. Financial markets are characterized by volatility clustering, heavy tails and frequent distributional shifts, all of which can undermine the assumptions underlying traditional prediction methods.

To address this problem, we combined volatility modelling techniques from the GARCH family with adaptive conformal prediction methods capable of updating prediction intervals over time.

Microsoft (**MSFT**) daily returns were used as an empirical case study.

---

## Repository Contents

- `Part1_ACI_Theory.pdf` – Theoretical review of Adaptive Conformal Inference under distribution shift.
- `Part2_ACI_AgACI_Implementation.pdf` – Empirical implementation of ACI and AgACI for volatility forecasting.
- `Project_Presentation.pdf` – Final presentation summarizing methodology, implementation and results.
- `PROJECT_OVERVIEW.md` – Additional description of the project structure.

---

## Project Overview

The project is divided into three main stages.

### 1. Volatility Modelling

The first stage focused on modelling volatility through the GARCH family of models.

After computing Microsoft daily returns, we analysed their statistical properties and investigated the presence of volatility clustering and conditional heteroskedasticity through:

- Autocorrelation analysis
- Ljung-Box tests
- ARCH-LM tests

The results confirmed the presence of significant ARCH effects, making GARCH-type models appropriate for the analysis.

Several model specifications were considered.

#### Models

- sGARCH
- eGARCH
- apARCH

#### Conditional Distributions

- Normal
- Student-t
- GED

Models were compared using:

- Log-Likelihood
- Akaike Information Criterion (AIC)
- Bayesian Information Criterion (BIC)

The analysis showed that asymmetric volatility models combined with heavy-tailed distributions provided the best fit to the data.

While **apARCH(1,1) with Student-t innovations** achieved the best information criteria, **eGARCH(1,1) with Student-t innovations** delivered comparable performance with lower computational complexity and was therefore selected for the conformal prediction stage.

---

### 2. Adaptive Conformal Inference (ACI)

After selecting a volatility model, Adaptive Conformal Inference was applied to construct prediction intervals with target miscoverage level

**α = 0.05**

corresponding to a nominal coverage level of 95%.

Unlike standard conformal prediction methods, which rely on exchangeability assumptions, ACI dynamically updates the miscoverage parameter over time in order to adapt to distributional changes.

Several configurations were analysed:

- Adaptive vs Non-Adaptive approaches
- Simple vs Momentum updates
- Normalized vs Non-normalized conformity scores

Particular attention was devoted to the role of the adaptation parameter **γ**, which controls the speed at which the algorithm reacts to coverage errors.

The empirical analysis showed that:

- Adaptive methods were generally more robust under distributional shifts.
- Normalized conformity scores produced more stable coverage behaviour.
- Simple and Momentum updates generated similar results.
- The quality of the underlying volatility model directly affected interval performance.
- Larger γ values increased responsiveness but could also lead to instability when chosen excessively large.

---

### 3. Aggregated Adaptive Conformal Inference (AgACI)

One of the main limitations of ACI is the need to select a specific value for γ.

To overcome this issue, we implemented **Aggregated Adaptive Conformal Inference (AgACI)**.

Instead of relying on a single adaptation rate, AgACI simultaneously combines multiple adaptive experts associated with different γ values:

- 0.001
- 0.004
- 0.007
- 0.010
- 0.013

Each expert generates its own adaptive prediction intervals.

The experts are then aggregated through **BOA (Bernstein Online Aggregation)**, an online learning procedure that dynamically assigns larger weights to experts that perform better over time.

AgACI was also compared with a **Naive Strategy**, which periodically selects the expert that achieved the best recent performance.

This comparison allowed us to evaluate whether dynamic aggregation provides benefits relative to selecting a single expert ex ante.

---

## Main Findings

The project led to the following conclusions:

- Microsoft returns exhibit clear volatility clustering and significant ARCH effects.
- Asymmetric GARCH models with Student-t innovations provide the most realistic description of volatility dynamics.
- Adaptive Conformal Inference improves interval reliability when the underlying distribution changes over time.
- The adaptation parameter γ plays a crucial role in determining the behaviour of ACI.
- AgACI eliminates the need to commit to a single adaptation rate by combining multiple adaptive experts.
- Online expert aggregation provides a more robust framework for uncertainty quantification in financial volatility forecasting.

---

## Skills Demonstrated

- Financial Time Series Analysis
- Volatility Modelling
- GARCH Family Models
- Model Selection and Evaluation
- Statistical Testing
- Conformal Prediction
- Adaptive Conformal Inference (ACI)
- Aggregated Adaptive Conformal Inference (AgACI)
- Online Learning and Expert Aggregation
- Financial Econometrics
- R Programming
- Reproducible Research with R Markdown

---

## Tools and Libraries

- R
- R Markdown
- quantmod
- rugarch
- opera

---

## Team

This project was developed as a group assignment by:

- Elisa Battista
- Simone Cuonzo
- Lorenzo Di Giannantonio
