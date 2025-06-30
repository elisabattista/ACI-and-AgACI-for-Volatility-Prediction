# ACI-and-AgACI-for-Volatility-Prediction

## Team and Course Information

This project was developed as a **group assignment** for the **Time Series** course.  
**Team members:**  
- Elisa Battista  
- Simone Cuonzo  
- Lorenzo Di Giannantonio  

The project reflects collaborative work including data analysis, coding, and discussion.

## Project Description

This repository contains an implementation and comparison of two conformal prediction frameworks — Adaptive Conformal Inference (ACI) and Aggregated Adaptive Conformal Inference (AgACI) — applied to forecasting volatility in financial time series.

We use real financial asset data and combine conformal prediction methods with GARCH models to quantify uncertainty through prediction intervals.

### Project overview

- **Part I:** Implementation of ACI for volatility prediction using GARCH(1,1) and a more advanced GARCH variant. We compare standard CP and adaptive CP strategies with different score normalizations.  
- **Part II:** Extension with AgACI, a parameter-free adaptive aggregation method over multiple ACI experts with varying adaptation rates. We apply it to volatility uncertainty quantification and compare coverage performances.

### Tools and libraries

- R, R Markdown (.Rmd and HTML outputs)  
- quantmod (financial data retrieval)  
- rugarch (GARCH modeling)  
- opera (experts aggregation for AgACI)  

