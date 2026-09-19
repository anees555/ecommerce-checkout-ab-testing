# E-Commerce Checkout A/B Testing Case Study

## Project Purpose

An e-commerce company wants to evaluate whether a redesigned checkout experience (Variant B) improves purchase conversion compared with the existing checkout experience (Variant A).

This project simulates a real-world controlled A/B experiment and focuses on both **statistical validity** and **business impact**.

## Main Objective

Determine whether the redesigned checkout produces a meaningful change in purchase conversion compared with the existing checkout.

## Key Questions

* Is the experiment properly randomized?
* Are Variants A and B reasonably balanced?
* Is there evidence of a difference in conversion rate?
* How large is the observed treatment effect?
* What is the uncertainty around the estimated effect?
* Is the effect statistically significant?
* Is the effect practically meaningful for the business?
* Does the treatment affect different user segments differently?
* Does the redesign introduce negative effects in important guardrail metrics?

## Primary Metric

**Checkout Conversion Rate**

$$
Conversion\ Rate = \frac{Purchases}{Users}
$$

## Secondary Metrics

* Revenue per User
* Average Order Value (AOV)
* Checkout Start Rate
* Purchase Rate among Checkout Starters

## Guardrail Metrics

* Payment Failure Rate
* Refund Rate
* Page Load Time

## Statistical Analysis

The project will include:

* Experiment and randomization validation
* Sample Ratio Mismatch (SRM) check
* Descriptive analysis
* Two-proportion hypothesis test
* P-value
* Confidence interval
* Effect size
* Statistical vs. practical significance
* Segment-level analysis
* Multiple-testing correction
* Logistic regression and interaction analysis

## Tools

* Python
* Pandas
* NumPy
* SciPy
* Statsmodels
* Matplotlib
* Seaborn
* Jupyter Notebook
* Power BI
* Git/GitHub

## Expected Outcome

The final analysis will provide a statistically grounded assessment of the checkout experiment and translate the experimental results into understandable business insights.

The analysis will distinguish between **statistical evidence** and **business significance** rather than relying on p-values alone.
