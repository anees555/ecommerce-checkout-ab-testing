# Experiment Design — E-Commerce Checkout A/B Test

## 1. Business Problem

The e-commerce platform is testing a redesigned checkout experience. The current checkout flow is used as Variant A, while the redesigned checkout flow is Variant B.

The main business question is whether the redesigned checkout changes the percentage of users who complete a purchase.

The experiment is designed to measure the effect of the checkout redesign using randomized assignment and statistical inference rather than relying only on the observed difference between the two groups.

## 2. Experiment Objective

The primary objective is to determine whether Variant B produces a statistically significant change in purchase conversion compared with Variant A.

The analysis will also examine whether the change has practical business significance and whether the redesign affects other important metrics such as payment failures, refunds, checkout starts, and revenue.

## 3. Experimental Unit

The experimental unit is the **user**.

Each user is assigned to one checkout variant, and the dataset contains one row per user. This is important because observations from the same user should not be treated as independent experimental units.

The primary outcome for each user is binary:

* `purchase = 1` → the user completed a purchase
* `purchase = 0` → the user did not complete a purchase

## 4. Experiment Groups

### Control — Variant A

Variant A represents the existing checkout experience.

### Treatment — Variant B

Variant B represents the redesigned checkout experience.

The primary comparison is:

**Variant B vs Variant A**

The experiment uses randomized assignment with an intended allocation of approximately 50% of users to each variant.

## 5. Randomization

Users are randomly assigned to either Variant A or Variant B.

Randomization is used to reduce systematic differences between the groups and make the treatment groups comparable on average. This allows differences in outcomes between the groups to be interpreted as evidence about the effect of the checkout redesign, assuming the experiment is implemented correctly.

The experiment validation stage checks whether the observed allocation is consistent with the intended 50/50 assignment and whether important pre-treatment characteristics are reasonably balanced between the groups.

## 6. Primary Metric

The primary metric is **purchase conversion rate**.

$$
Conversion\ Rate = \frac{Number\ of\ Users\ Who\ Purchased}{Total\ Number\ of\ Users}
$$

The conversion rate is calculated at the user level.

This metric was selected because the main business objective of the checkout redesign is to influence the proportion of users who complete a purchase.

## 7. Secondary Metrics

The following metrics will provide additional context:

### Checkout Start Rate

$$
Checkout\ Start\ Rate =
\frac{Users\ Who\ Started\ Checkout}{Total\ Users}
$$

This helps determine whether the redesign is associated with changes earlier in the checkout funnel.

### Checkout-to-Purchase Rate

$$
Checkout\text{-}to\text{-}Purchase =
\frac{Users\ Who\ Purchased}{Users\ Who\ Started\ Checkout}
$$

This measures how effectively users who enter checkout complete a purchase.

### Revenue per User

$$
Revenue\ per\ User =
\frac{Total\ Revenue}{Total\ Users}
$$

This provides a business-oriented measure of the financial impact of the experiment.

### Average Order Value

$$
AOV =
\frac{Total\ Revenue}{Number\ of\ Purchasers}
$$

AOV will be interpreted separately from conversion because a change in conversion does not necessarily imply a change in order value.

## 8. Guardrail Metrics

The experiment will also monitor metrics that could indicate unintended negative effects.

The main guardrails are:

* Payment failure rate
* Refund rate
* Page load time

These metrics are not the primary basis for determining the treatment effect on purchase conversion. They are used to identify potential negative side effects of the redesigned checkout.

## 9. Hypotheses

The primary hypothesis concerns the difference in purchase conversion between Variant A and Variant B.

Let:

* \(p_A\) = purchase conversion rate for Variant A
* \(p_B\) = purchase conversion rate for Variant B

### Null Hypothesis

$$
H_0: p_A = p_B
$$

There is no difference in purchase conversion between the two checkout variants.

### Alternative Hypothesis

$$
H_1: p_A \neq p_B
$$

There is a difference in purchase conversion between the two checkout variants.

A two-sided hypothesis is used because the redesigned checkout could potentially increase or decrease conversion.

## 10. Significance Level

The significance level is set to:

$$
\alpha = 0.05
$$

A p-value below 0.05 will be considered statistically significant under this predefined threshold.

The p-value will not be interpreted as the probability that Variant B is better. Instead, it measures how unusual the observed difference would be if the null hypothesis of equal conversion rates were true.

## 11. Statistical Test

The primary statistical test will be a **two-proportion z-test**.

This test is appropriate because:

* the outcome is binary (`purchase` or `no purchase`);
* the primary metric is a proportion;
* the two groups are independently assigned users;
* the experiment compares conversion rates between two groups.

The analysis will calculate:

* Conversion rate for Variant A
* Conversion rate for Variant B
* Absolute difference in conversion rate
* Relative lift
* Standard error
* Test statistic
* p-value
* 95% confidence interval

## 12. Effect Size

Statistical significance alone will not determine the business interpretation of the experiment.

Two effect-size measures will be reported.

### Absolute Difference

$$
Difference = p_B - p_A
$$

This will be reported in **percentage points**.

For example, if conversion changes from 9% to 10%, the absolute difference is **+1 percentage point**, not +1%.

### Relative Lift

$$
Relative\ Lift =
\frac{p_B-p_A}{p_A}\times100
$$

This expresses the change relative to the baseline conversion rate of Variant A.

## 13. Confidence Interval

A **95% confidence interval** will be reported for the difference in conversion rates.

The confidence interval provides a range of plausible values for the underlying difference between the two variants.

The confidence interval will be considered together with the p-value and observed effect size rather than relying on statistical significance alone.

## 14. Statistical vs Practical Significance

The experiment will distinguish between statistical significance and practical business significance.

A statistically significant result indicates that the observed difference provides sufficient evidence against the null hypothesis at the chosen significance level.

However, a statistically significant difference may still be too small to have meaningful business value.

Therefore, the final interpretation will consider:

* Size of the conversion effect
* Confidence interval
* Statistical significance
* Revenue impact
* Operational or customer-experience effects
* Guardrail metrics

No treatment decision will be based solely on the p-value.

## 15. Sample and Experiment Period

The dataset contains approximately **200,000 users** observed over approximately six weeks.

The experiment period will be examined for allocation consistency and temporal variation before the primary statistical analysis.

The complete available experiment data will be analyzed rather than selecting only favorable dates or periods.

## 16. Analysis Principles

The analysis will follow these principles:

1. Analyze users according to their assigned experiment variant.
2. Use purchase conversion as the predefined primary metric.
3. Perform experiment and data-quality validation before interpreting treatment effects.
4. Use a two-sided hypothesis test with \(\alpha = 0.05\).
5. Report both statistical uncertainty and effect size.
6. Distinguish statistical significance from practical business significance.
7. Treat segmentation analysis as additional analysis rather than replacing the primary experiment result.
8. Avoid selectively reporting time periods or segments based on the observed results.
9. Consider multiple-testing issues when evaluating multiple secondary metrics or segments.
10. Interpret guardrail metrics alongside the primary conversion result.

## 17. Planned Analysis Workflow

The experiment analysis will follow this sequence:

**Data Quality → Experiment Validation → Randomization/SRM Check → A/B Balance Check → Funnel Analysis → Primary Conversion Analysis → Confidence Interval → Effect Size → Business Metrics → Guardrails → Segment Analysis → Additional Modeling**

The primary treatment-effect conclusion will be based on the randomized A/B comparison and the predefined primary metric.

## 18. Expected Outcome

The analysis is intended to determine whether the redesigned checkout provides evidence of a change in purchase conversion and to quantify the size and uncertainty of that change.

The final conclusion will separate:

* what was observed in the data,
* what is statistically supported,
* and what may be meaningful from a business perspective.
