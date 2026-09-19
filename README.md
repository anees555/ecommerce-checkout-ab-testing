# E-Commerce Checkout A/B Testing Case Study

## Overview

This project looks at an e-commerce company testing two checkout experiences. Variant A is the existing checkout and Variant B is the redesigned version.

The main question is simple: does the redesigned checkout change purchase conversion? The project also checks whether the experiment itself is reliable before making any business conclusions.

## Business Problem

The company wants to know whether the new checkout experience (B) performs differently from the current experience (A). A better-looking redesign is not enough on its own. We need to check the data, compare the groups fairly, and measure both statistical and practical impact.

## Project Goals

- Validate the experiment and randomization
- Compare conversion between A and B
- Measure statistical significance and uncertainty
- Measure practical and business impact
- Check important guardrail metrics
- Analyze differences across user segments

## Dataset

- 200,000 unique users
- One row per user
- Approximately 6 weeks of experiment data
- Randomized control and treatment groups
- User, experiment, conversion, revenue, and performance fields

Detailed column descriptions are available in the data dictionary. The project does not list every field here so the README stays easy to scan.

## Main Metrics

**Primary metric**

- Checkout conversion rate

**Secondary metrics**

- Revenue per user
- Average order value
- Checkout start rate

**Guardrail metrics**

- Payment failure rate
- Refund rate
- Page load time

## Analysis Approach

Data Quality  
→ Experiment Validation  
→ EDA  
→ A/B Test  
→ Confidence Intervals & Effect Size  
→ Business Impact  
→ Segment Analysis  
→ Logistic Regression  
→ Power BI Dashboard

The project focuses on both statistical significance and practical business significance. A result can be statistically convincing but still too small to matter for the business, so both sides are considered.

## Tools Used

Python, Pandas, NumPy, SciPy, Statsmodels, Matplotlib, Seaborn, Jupyter Notebook, Power BI, and Git/GitHub.

## Project Structure

```text
Data/
notebooks/
src/
powerbi/
reports/
project_description.md
README.md
```

## Current Status

- [x] Dataset creation
- [x] Initial data inspection
- [x] Data quality checks
- [x] Experiment validation
- [ ] Statistical analysis
- [ ] Business impact analysis
- [ ] Segment analysis
- [ ] Logistic regression
- [ ] Power BI dashboard
- [ ] Final findings

## Results

Final statistical and business findings will be added after the analysis is complete.

**Current result:** [To be added after analysis]

## What I Learned

- [To be added after completing the project]
- [To be added after completing the project]
- [To be added after completing the project]