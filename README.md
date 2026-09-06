# Fisher Scoring and MCMC for GLMs

## Overview
This project 
- implements two estimation approaches for Generalized Linear Models (GLMs) from scratch:
  - Fisher Scoring (a Newton-type maximum likelihood algorithm) and
  - Random Walk Metropolis-Hastings MCMC (a Bayesian sampling approach) and
- compares their results on two real-world datasets:
  - credit card approval (logistic regression) and
  - hospital length of stay after cardiac procedures (Poisson regression, log link).

*[Completed as part of a team assignment. I led the implementation of the Fisher Scoring and MCMC algorithms, and reviewed and revised the written report.]*

## Approach/Methods
- Derived and implemented the Fisher Scoring algorithm for GLM parameter estimation, including the score function and Fisher information matrix for canonical and non-canonical link functions
- Proved the equivalence of Fisher Scoring and Newton's method under canonical links, and analyzed why this equivalence breaks down for non-canonical links (e.g. probit)
- Implemented Random Walk Metropolis-Hastings MCMC with a Gaussian random-walk proposal and weakly informative Gaussian priors on the coefficients
- Assessed MCMC convergence via trace plots and autocorrelation (ACF) diagnostics
- Applied logistic regression (Fisher Scoring + MCMC) to a credit card approval dataset, excluding post-approval variables (`expenditure`, `share`) to avoid data leakage
- Applied Poisson regression (log link) to a hospital length-of-stay dataset (CABG vs. PTCA procedures)
- Back-transformed standardized coefficients to original units and reported effects as Odds Ratios / Incidence Rate Ratios

## Key Results
- Fisher Scoring converged in 7 iterations (credit card model) and 15 iterations (hospital stay model); both showed stable, well-behaved convergence
- MCMC chains for both datasets showed stable trace plots and rapidly decaying autocorrelation (within ~7–10 lags), indicating good mixing
- Fisher Scoring (MLE) and MCMC (Bayesian posterior mean) produced highly consistent coefficient estimates across both datasets, with overlapping confidence/credible intervals
- **Credit card approval**: driven mainly by creditworthiness indicators. Each derogatory report reduces approval odds by ~82.7%, each active account increases odds by ~14.1%, and self-employment reduces odds by ~53.1%
- **Hospital length of stay**: driven mainly by clinical factors. Undergoing a CABG procedure (vs. PTCA) is associated with a ~209.6% increase in expected stay duration; emergency/urgent admission increases expected stay by ~20.9%; male patients have ~10.1% shorter expected stays than female patients

## Tools Used
Python: NumPy, SciPy, pandas, Matplotlib, Seaborn

## Repository Contents
- `stats_project_fisher_scoring_mcmc.ipynb`: full analysis - algorithm implementation, both dataset applications, diagnostics, and results
- `data/creditcard.csv`: credit card approval dataset (logistic regression)
- `data/azcabgptca.csv`: hospital length-of-stay dataset (Poisson regression)
- `report.pdf`: compiled written report
- `report/report.tex`: LaTeX source of the report
- `mcmc_trace_acf_procedure.png` and `mcmc_trace_acf_income.png` : MCMC diagnostic plots (trace + ACF) for the income coefficient (credit card model) and procedure coefficient (hospital stay model)
