# Adaptive Conformal Inference and AgACI for Volatility Prediction

This repository contains a group project developed for the *Time Series and Financial Time Series* course at Sapienza University of Rome.

The project investigates uncertainty quantification in financial volatility forecasting using GARCH models, Adaptive Conformal Inference (ACI), and Aggregated Adaptive Conformal Inference (AgACI).

Microsoft (MSFT) daily returns were used as a case study.

## Volatility Modelling

The first part of the project focused on modelling volatility.

After computing daily returns, we analysed their statistical properties and verified the presence of volatility clustering and ARCH effects through autocorrelation analysis, Ljung-Box tests and ARCH-LM tests.

Since volatility was clearly time-varying, several GARCH-family models were considered:

* sGARCH
* eGARCH
* apARCH

under different conditional distributions:

* Normal
* Student-t
* GED

Models were compared using Log-Likelihood, AIC and BIC.

The results showed that asymmetric models combined with heavy-tailed distributions provided the best fit to the data. While apARCH(1,1) with Student-t innovations achieved the best information criteria, eGARCH(1,1) with Student-t innovations offered a very similar fit with lower computational complexity and was therefore selected for the conformal prediction stage.

## Adaptive Conformal Inference

Once a volatility model had been selected, we applied Adaptive Conformal Inference to construct prediction intervals with a target miscoverage level of 5%.

Unlike standard conformal prediction, which relies on exchangeability assumptions that are often unrealistic in financial applications, ACI updates the miscoverage parameter over time in order to adapt to distributional changes.

Several configurations were compared:

* Adaptive vs Non-Adaptive approaches
* Simple vs Momentum updates
* Normalized vs Non-normalized conformity scores

The analysis showed that adaptive methods were generally more robust when the underlying distribution changed over time. Score normalization improved stability, while Simple and Momentum updates produced very similar results.

We also investigated the role of the adaptation parameter γ. Larger values allowed the algorithm to react more quickly to changing market conditions, although excessively large values could lead to instability.

## Aggregated Adaptive Conformal Inference

A limitation of ACI is the need to choose a specific value for γ.

To address this issue, we implemented AgACI, which replaces a single adaptive expert with a collection of experts using different adaptation rates.

The following values were considered:

* 0.001
* 0.004
* 0.007
* 0.010
* 0.013

Each expert generated its own adaptive prediction intervals.

Rather than selecting one expert in advance, the experts were combined through BOA (Bernstein Online Aggregation), an online learning procedure that dynamically assigns larger weights to the experts that perform better over time.

AgACI was also compared with a Naive Strategy that periodically selects a single expert based on past performance.

## Main Findings

The project led to several conclusions:

* Microsoft returns exhibit clear volatility clustering and significant ARCH effects.
* Asymmetric GARCH models with Student-t innovations provide the most realistic description of volatility dynamics.
* Adaptive Conformal Inference improves interval reliability in the presence of distribution shifts.
* The choice of γ plays an important role in the behaviour of ACI.
* AgACI removes the need to commit to a single γ by combining multiple adaptive experts.
* Online aggregation provides a more robust framework for uncertainty quantification in financial volatility forecasting.

This project allowed us to explore the complete workflow from volatility modelling to uncertainty quantification, combining classical time series methods with modern adaptive conformal prediction techniques.

## Team

This project was developed in collaboration with Simone Cuonzo and Lorenzo Di Giannantonio as part of a group assignment.
