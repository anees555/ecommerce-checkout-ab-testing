# Statistical Analysis

## 1. Overview

This report checks what the checkout A/B experiment tells us statistically.

Variant A is the current checkout and Variant B is the redesigned checkout. The experiment has 200,000 users, with one row per user, and ran for around six weeks. The main question here is whether purchase conversion was different between the two variants.

This report focuses on the statistical analysis only. The final business recommendation will be handled separately.

## 2. Primary Metric

The primary metric is **purchase conversion rate**:

```text
purchase conversion rate = purchasers / users
```

This metric tells us the share of users who completed a purchase. Since the main purpose of a checkout is to help users complete orders, this is the main outcome for the experiment.

## 3. Observed Conversion Results

| Variant | Users | Purchasers | Conversion Rate |
|---|---:|---:|---:|
| A | 100,304 | 9,750 | 9.72% |
| B | 99,696 | 10,663 | 10.70% |

The observed difference, calculated as B minus A, was about **+0.98 percentage points**.

The relative lift was about **+10.03%** compared with Variant A. This is the observed result in this sample. It is not, by itself, proof that the difference is statistically meaningful.

## 4. Hypothesis Test

### Hypotheses

- **Null hypothesis ($H_0$):** $p_A = p_B$
- **Alternative hypothesis ($H_1$):** $p_A \ne p_B$

The test was two-sided because the redesigned checkout could have increased conversion, decreased conversion, or made no real difference.

The significance level was $\alpha = 0.05$.

### Test Used

I used a two-proportion z-test because the outcome is binary: each user either purchased or did not purchase. The test compares the purchase proportions in A and B.

The result was:

- z-statistic: **-7.20**
- p-value: **5.93e-13**
- Decision: **Reject $H_0$** at $\alpha = 0.05$

The z-statistic is negative because Statsmodels received the variants in A minus B order. The actual effect direction is still B higher than A. For a two-sided test, changing the sign does not change the p-value or the decision.

In simple terms, the p-value tells us how unusual a difference this large would be if the underlying conversion rates were actually equal. It is not the probability that the null hypothesis is true.

Since the p-value is far below 0.05, the data provides statistical evidence that purchase conversion differed between A and B. This does not prove that the same effect will happen for every future user.

## 5. 95% Confidence Interval

The confidence interval was calculated for **B minus A**. The observed difference was about **+0.98 percentage points**, and the 95% confidence interval was approximately:

**+0.71 to +1.24 percentage points**

A confidence interval gives a range around the estimated effect. One number gives us the point estimate, but the interval shows how much uncertainty is around that estimate.

The interval does not contain zero. So, a zero difference is not included in this calculated range. This is consistent with the earlier hypothesis-test decision to reject $H_0$ at $\alpha = 0.05$.

The correct frequentist interpretation is not that there is a 95% probability that the true effect is inside this particular interval. If we repeated the same experiment many times and calculated a 95% confidence interval each time, around 95% of those intervals would contain the true population difference, assuming the statistical assumptions are reasonable.

## 6. Practical Significance

Statistical significance and practical significance are different things.

Statistical significance asks whether the observed difference would be unusual under the null hypothesis. Practical significance asks whether the size of the difference is large enough to matter in the real situation.

Here, the observed effect was:

- Absolute difference: **+0.98 percentage points**
- Relative lift: **+10.03%**

As a simple translation, a +0.98 percentage-point difference corresponds to roughly **980 additional purchases per 100,000 users** if the observed effect stayed similar. This is only an illustrative estimate, not a guaranteed future result.

A statistically significant result does not automatically mean the effect is large, valuable, or easy to implement. Those questions need business context, cost information, revenue analysis, and guardrail checks.

## 7. Checkout Funnel Analysis

### Checkout Start Rate

Checkout start rate is calculated as users who started checkout divided by all users in the variant.

| Variant | Checkout Start Rate |
|---|---:|
| A | 29.29% |
| B | 28.96% |
| Difference | -0.33 percentage points |
| Relative difference | -1.12% |

The z-statistic was **1.62** and the p-value was **0.10547**. The observed rate was slightly lower in B, but the test did not provide enough statistical evidence of a difference at $\alpha = 0.05$.

### Checkout-to-Purchase Rate

This rate uses checkout starters as the denominator:

```text
checkout-to-purchase rate = purchasers / checkout starters
```

| Variant | Checkout-to-Purchase Rate |
|---|---:|
| A | 33.19% |
| B | 36.93% |
| Difference | +3.74 percentage points |
| Relative difference | +11.28% |

The z-statistic was **-9.47** and the p-value was approximately **2.8160e-21**. The rate was higher for B, and the test provided strong statistical evidence of a difference.

This result shows a difference in the observed experiment data. It should not be described as absolute proof that the redesign will cause the same change in every future setting.

## 8. Revenue Analysis

Revenue was handled separately from conversion because it is highly skewed and contains many zero values for non-purchasers.

### Revenue per User

Revenue per user uses all users in each variant, including users with zero revenue.

| Variant | Revenue per User |
|---|---:|
| A | $7.8066 |
| B | $8.6911 |
| Difference | +$0.8845 |
| Relative difference | +11.33% |

The Mann-Whitney U p-value was approximately **4.5030e-13**.

Because revenue is skewed, a rank-based Mann-Whitney test was used instead of blindly applying a normal-based test. This test checks whether observations from one group tend to be systematically higher or lower than observations from the other group. It is not a direct test of the difference in mean revenue.

### Average Order Value

AOV uses purchasing users only. It answers a different question from revenue per user: how much did purchasers spend on average?

| Variant | AOV |
|---|---:|
| A | $80.3115 |
| B | $81.2594 |
| Difference | +$0.9478 |
| Relative difference | +1.18% |

The Mann-Whitney p-value for AOV was approximately **0.4073**. At $\alpha = 0.05$, this does not provide enough statistical evidence of a difference in the AOV distributions.

So, revenue per user and AOV should not be mixed together. Revenue per user includes conversion and order value in one user-level metric. AOV looks only at users who purchased.

## 9. Guardrail Analysis

Guardrails help check whether an improvement in the primary metric comes together with deterioration in other important metrics.

### Payment Failure Rate

Payment failure rate uses users who started checkout as the denominator:

```text
payment failure rate = payment failures / checkout starters
```

| Variant | Payment Failure Rate |
|---|---:|
| A | 2.26% |
| B | 2.13% |
| Difference | -0.13 percentage points |
| Relative difference | -5.90% |

The z-statistic was **1.10** and the p-value was **0.2718**. The observed rate was slightly lower in B, but there was not enough statistical evidence to conclude that the variants differ in payment failure rate.

### Refund Rate

Refund rate uses purchasers as the denominator:

```text
refund rate = refunds / purchasers
```

| Variant | Refund Rate |
|---|---:|
| A | 5.65% |
| B | 4.96% |
| Difference | -0.69 percentage points |
| Relative difference | -12.21% |

The z-statistic was **2.20** and the p-value was **0.02778**. The observed refund rate was lower in B, and the difference was statistically significant at $\alpha = 0.05$.

Still, this does not mean B will reduce refunds in every future situation. It only describes the evidence from this experiment and its assumptions.

### Page Load Time

Page-load time is treated as a post-treatment performance guardrail because the checkout experience can affect it.

| Variant | Mean Page Load Time |
|---|---:|
| A | 2,839.9617 ms |
| B | 2,771.0405 ms |
| Difference | -68.9212 ms |
| Relative difference | approximately -2.43% |

The Mann-Whitney p-value was extremely small and displayed as `0.0000e+00` because of numerical formatting. This does not mean the p-value is literally zero.

With a large sample of 200,000 users, even a fairly small difference can become statistically significant. The estimated difference of about 69 ms may or may not be operationally important. Statistical significance alone cannot answer that question.

## 10. Statistical Summary

| Metric | Variant A | Variant B | Difference | Relative Difference/Lift | Statistical Result |
|---|---:|---:|---:|---:|---|
| Purchase conversion | 9.72% | 10.70% | +0.98 pp | +10.03% | 95% CI: +0.71 to +1.24 pp; z = -7.20; p = 5.93e-13; Reject $H_0$ |
| Checkout start rate | 29.29% | 28.96% | -0.33 pp | -1.12% | z = 1.62; p = 0.10547 |
| Checkout-to-purchase rate | 33.19% | 36.93% | +3.74 pp | +11.28% | z = -9.47; p = 2.8160e-21 |
| Revenue per user | $7.8066 | $8.6911 | +$0.8845 | +11.33% | Mann-Whitney p = 4.5030e-13 |
| AOV | $80.3115 | $81.2594 | +$0.9478 | +1.18% | Mann-Whitney p = 0.4073 |
| Payment failure rate | 2.26% | 2.13% | -0.13 pp | -5.90% | z = 1.10; p = 0.2718 |
| Refund rate | 5.65% | 4.96% | -0.69 pp | -12.21% | z = 2.20; p = 0.02778 |
| Page load time | 2,839.9617 ms | 2,771.0405 ms | -68.9212 ms | -2.43% | Mann-Whitney p extremely small; displayed as 0.0000e+00 |

## 11. Overall Statistical Findings

Variant B had a higher observed purchase conversion rate than Variant A. The difference was around **+0.98 percentage points**, with an estimated relative lift of about **+10.03%**.

The two-proportion z-test rejected $H_0$ at $\alpha = 0.05$, and the 95% confidence interval for B minus A was positive, approximately **+0.71 to +1.24 percentage points**. So, the data provides statistical evidence of a difference in purchase conversion.

The checkout-to-purchase rate was also higher in B and showed statistical evidence of a difference. Revenue per user showed a statistically significant distributional difference in the Mann-Whitney test, while AOV did not show enough statistical evidence of a difference.

Payment failure rate did not show enough evidence of a difference. Refund rate and page-load time showed statistically significant differences in this analysis. These results still need to be understood with practical context, because statistical significance and practical significance are not the same thing.

This report focuses only on what the statistical analysis tells us. The final business interpretation and recommendation will be handled separately.
