# Adaptive Conformal Inference and AgACI for Volatility Prediction

This repository contains a group project developed for the **Time Series and Financial Time Series** course at **Sapienza University of Rome**.

The project investigates uncertainty quantification in financial volatility forecasting using **Adaptive Conformal Inference (ACI)** and **Aggregated Adaptive Conformal Inference (AgACI)**.

Financial volatility is difficult to forecast because market conditions and volatility regimes change over time. For this reason, in addition to volatility modelling, the project focuses on constructing reliable prediction intervals that remain informative under distributional shifts.

Microsoft (**MSFT**) daily returns were used as a case study.

---

## Project Overview

The project is divided into three main stages:

### 1. Volatility Modelling

The first step consisted of modelling volatility through the GARCH family of models.

After computing daily returns, we analysed their statistical properties and investigated volatility clustering through:

* Autocorrelation analysis
* Ljung-Box tests
* ARCH-LM tests

The results confirmed the presence of significant ARCH effects, making GARCH-type models suitable for the analysis.

Several specifications were considered:

**Models**

* sGARCH
* eGARCH
* apARCH

**Conditional distributions**

* Normal
* Student-t
* GED

Models were compared using:

* Log-Likelihood
* AIC
* BIC

The analysis showed that asymmetric models combined with heavy-tailed distributions provided the best fit to the data. While **apARCH(1,1) with Student-t innovations** achieved the best information criteria, **eGARCH(1,1) with Student-t innovations** offered very similar performance with lower computational complexity and was therefore selected for the conformal prediction stage.

---

### 2. Adaptive Conformal Inference (ACI)

Once a volatility model had been selected, Adaptive Conformal Inference was applied to construct prediction intervals with a target miscoverage level of:

**α = 0.05**

corresponding to a 95% coverage level.

Unlike standard conformal prediction, which relies on exchangeability assumptions, ACI dynamically updates the miscoverage parameter over time in order to adapt to changes in the underlying data-generating process.

Several configurations were compared:

* Adaptive vs Non-Adaptive approaches
* Simple vs Momentum updates
* Normalized vs Non-normalized conformity scores

We also investigated the role of the adaptation parameter **γ**.

The analysis showed that:

* Adaptive methods were generally more robust under distribution shifts.
* Score normalization improved the stability of coverage rates.
* Simple and Momentum updates produced similar results.
* Better volatility models translated into more reliable conformal intervals.
* Larger γ values improved responsiveness, although excessively large values could generate instability.

---

### 3. Aggregated Adaptive Conformal Inference (AgACI)

A limitation of ACI is the need to choose a specific adaptation parameter γ.

To address this issue, we implemented **Aggregated Adaptive Conformal Inference (AgACI)**.

Instead of relying on a single γ value, AgACI combines multiple adaptive experts using different adaptation rates:

* 0.001
* 0.004
* 0.007
* 0.010
* 0.013

Each expert generates its own adaptive prediction intervals.

The experts are then aggregated through **BOA (Bernstein Online Aggregation)**, an online learning procedure that dynamically assigns larger weights to the experts that perform better over time.

AgACI was also compared with a **Naive Strategy**, which periodically selects the expert that performed best in the recent past.

---

## Main Findings

The project led to several conclusions:

* Microsoft returns exhibit clear volatility clustering and significant ARCH effects.
* Asymmetric GARCH models with Student-t innovations provide the most realistic description of volatility dynamics.
* Adaptive Conformal Inference improves interval reliability when the underlying distribution changes over time.
* The choice of γ plays an important role in the behaviour of ACI.
* AgACI removes the need to commit to a single γ by combining multiple adaptive experts.
* Online aggregation provides a more robust framework for uncertainty quantification in financial volatility forecasting.

---

## Tools and Libraries

* R
* R Markdown
* quantmod
* rugarch
* opera

---

## Team

This project was developed as a group assignment by:

* Elisa Battista
* Simone Cuonzo
* Lorenzo Di Giannantonio
