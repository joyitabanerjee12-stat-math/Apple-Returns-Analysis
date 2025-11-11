# Analysis of Apple (AAPL) Daily Returns Using ANOVA and T-Test

## Introduction
This analysis examines the daily returns of Apple Inc. (AAPL) to determine whether there is a statistically significant difference in returns between days when the stock moves up versus down.

The dataset consists of daily closing prices for Apple in early 2023. Daily returns were computed as:

\[
\text{Return}_t = \frac{P_t - P_{t-1}}{P_{t-1}}
\]

where \(P_t\) is the closing price on day \(t\).

---

## Data Preparation
1. **Compute Apple Returns:** Daily returns were calculated in Excel from closing prices.  
2. **Classify Returns into Groups:**  
   - **Up:** Return > 0  
   - **Down:** Return < 0  
3. **Organize Data for Analysis:** Two columns were created for the groups:

| Group | Column |
|-------|--------|
| Down  | I      |
| Up    | J      |

Blank cells were left where necessary.

---

## Statistical Methods

### 1. One-Way ANOVA
**Hypotheses:**  
\[
H_0: \mu_\text{Up} = \mu_\text{Down}  
\]  
\[
H_1: \mu_\text{Up} \neq \mu_\text{Down}
\]

**ANOVA Calculations in Excel:**

| Statistic | Formula / Description |
|-----------|---------------------|
| n (group counts) | `=COUNT(I2:I30)` and `=COUNT(J2:J30)` |
| Group Means | `=AVERAGE(I2:I30)` and `=AVERAGE(J2:J30)` |
| Overall Mean | `=AVERAGE(I2:J30)` |
| SSB | `=COUNT(I2:I30)*(mean_Down-overall_mean)^2 + COUNT(J2:J30)*(mean_Up-overall_mean)^2` |
| SSW | Sum of squared deviations from each group mean |
| MSB | `SSB/(k-1)` |
| MSW | `SSW/(N-k)` |
| F-statistic | `=MSB/MSW` |
| p-value | `=1-F.DIST(F_stat, k-1, N-k, TRUE)` |

**Results:**

| Group   | Count | Mean      |
|---------|-------|----------|
| Down    | 9   | -0.003174842|
| Up      | 20   | 0.003927445|
| Overall | 29   | 0.001723287|

| Statistic   | Value        |
|------------|--------------|
| SSB        | 0.000313091  |
| SSW        | 4.33984E-05  |
| MSB        | 0.000313091  |
| MSW        | 1.60735E-06  |
| F          | 194.787612   |
| p-value    | 7.27 × 10⁻¹⁴ |

**Interpretation:**  
- p-value << 0.05 → reject \(H_0\)  
- There is a statistically significant difference between Up and Down day returns.

---

### 2. Two-Sample T-Test
Because there are only two groups, a t-test provides an equivalent test.  

**Excel Formula:**  

```excel
=T.TEST(I2:I30, J2:J30, 2, 3)
