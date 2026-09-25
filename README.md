# E-Commerce Checkout A/B Testing Case Study

## Overview

This project analyzes an e-commerce company testing two checkout experiences. Variant A is the existing checkout and Variant B is the redesigned version.

The main question is simple: does the redesigned checkout change purchase conversion?

The analysis first validates the experiment and data quality, then evaluates the conversion difference statistically and translates the result into business impact. Additional analysis looks at the checkout funnel, revenue, guardrail metrics, user segments, and logistic regression.

## Business Problem

The company wants to know whether the new checkout experience (B) performs differently from the current experience (A).

A redesign may look better visually, but that does not necessarily mean it improves business outcomes. The experiment therefore needs to be evaluated using both statistical evidence and practical business impact.

## Project Goals

- Validate data quality and experiment randomization
- Check whether the A/B groups are reasonably balanced
- Compare purchase conversion between A and B
- Measure statistical significance and uncertainty
- Quantify the observed effect size
- Evaluate practical and business impact
- Analyze the checkout funnel
- Check important guardrail metrics
- Explore differences across user segments
- Use logistic regression to examine the treatment relationship after adjustment
- Build an interactive Power BI dashboard

## Dataset

- 200,000 unique users
- One row per user
- Approximately 6 weeks of experiment data
- Randomized control and treatment groups
- User, experiment, conversion, revenue, and performance fields

This project uses a synthetically generated dataset containing 200,000 user-level observations. It does not contain real customer or personally identifiable information.

Detailed column descriptions are available in the data dictionary. The README does not list every field so that it remains easy to scan.

## Experiment Design

| Component | Definition |
|---|---|
| Experimental unit | User |
| Control | Variant A — existing checkout |
| Treatment | Variant B — redesigned checkout |
| Primary metric | Purchase conversion rate |
| Secondary metrics | Checkout start rate, checkout-to-purchase rate, revenue per user, AOV |
| Guardrails | Payment failure rate, refund rate, page load time |
| Significance level | α = 0.05 |
| Primary statistical test | Two-proportion z-test |
| Confidence interval | 95% |

The primary hypothesis was:

- **H₀:** Purchase conversion is the same for A and B
- **H₁:** Purchase conversion differs between A and B



## Analysis Approach

```text
Data Quality
      ↓
Experiment Validation
      ↓
EDA
      ↓
A/B Test
      ↓
Confidence Interval & Effect Size
      ↓
Business Impact
      ↓
Segment Analysis
      ↓
Logistic Regression
      ↓
Power BI Dashboard
      ↓
Final Findings
 ```

 ## What I Learned

- How to validate an A/B experiment before interpreting its results
- How randomization and sample-ratio checks help identify experiment-quality issues
- How to compare conversion rates using hypothesis testing and confidence intervals
- How to distinguish statistical significance from practical business significance
- How to analyze an e-commerce conversion funnel and identify where changes occur
- How to interpret revenue per user, AOV, and operational guardrail metrics
- How logistic regression can be used to examine relationships after adjusting for observed characteristics
- How to translate statistical findings into clear business insights
- How to communicate analytical results through an interactive Power BI dashboard
- How to document an end-to-end data analysis project from experiment design to final findings

## Limitations

- The dataset is synthetically generated and does not represent real customer behavior.
- The experiment covers approximately six weeks, so long-term effects cannot be established.
- Segment-level analysis is exploratory and should not automatically be interpreted as causal.
- The analysis only includes the variables available in the dataset, so unmeasured factors may still exist.
- The business-impact calculation is an observed-data scenario, not a validated financial forecast.
- Actual production impact would depend on traffic volume, implementation costs, customer behavior, and whether the experimental result generalizes to real-world traffic.
- The analysis does not evaluate long-term customer retention, lifetime value, or other post-experiment effects.

## Final Findings

Variant B had a higher observed purchase conversion rate than Variant A:

- **Variant A:** 9.72%
- **Variant B:** 10.70%
- **Absolute difference:** +0.98 percentage points
- **Relative lift:** +10.03%

The two-proportion z-test produced a p-value of approximately **5.93 × 10⁻¹³**, and the 95% confidence interval for the conversion difference was approximately **+0.71 to +1.24 percentage points**.

The checkout funnel suggests that the improvement was concentrated after users started checkout. Checkout start rate was slightly lower for B, while checkout-to-purchase conversion was higher.

Variant B also had higher observed revenue per user:

- **A:** $7.81
- **B:** $8.69
- **Difference:** +$0.88 per user

Average order value changed only slightly, so the observed revenue difference was primarily associated with more completed purchases rather than substantially larger orders.

The logistic regression analysis produced a similar treatment relationship after adjusting for observed pre-treatment characteristics. The adjusted odds ratio for Variant B was **1.1135**.

Overall, the experiment provides strong statistical evidence of a difference in purchase conversion between the two checkout experiences. The results also show a positive observed business impact, although the findings should be validated with real production traffic and longer-term business metrics before making broader conclusions.