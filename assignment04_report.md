# Assignment 04 Interpretation Memo

**Student Name:** Katrina Baiza
**Date:** February 12, 2026
**Assignment:** REIT Annual Returns and Predictors (Simple Linear Regression)

---

## 1. Regression Overview

You estimated **three** simple OLS regressions of REIT *annual* returns on different predictors:

| Model | Y Variable | X Variable | Interpretation Focus |
|-------|------------|------------|----------------------|
| 1 | ret (annual) | div12m_me | Dividend yield |
| 2 | ret (annual) | prime_rate | Interest rate sensitivity |
| 3 | ret (annual) | ffo_at_reit | FFO to assets (fundamental performance) |

For each model, summarize the key results in the sections below.
for model 1 the slope is -0.0687 with SE of 0.0325, t stat of -2.114,p value of 0.0346, R^2 0.18%. the 1pp in div12m_m changed to -6.87 decrease in anual returns. It is a negative value but still significant. For model 2 slope is -0.0194, SE is 0.0030, t stat is -6.487, p value is <0.001, r^2 1.64%. the 1pp increase in prime rate changed to -1.94 decrease in annual returns. this is highly significant and shows REITs are sensitive. Model 3 has a slope of 0.5770, SE is 0.5675, t stat is 1.017, p value is 0.3093, r^2 0.04%. This has a positive point estimate but it is not significant and fundamental profitability does not rely on prediction of returns.

## 2. Coefficient Comparison (All Three Regressions)

**Model 1: ret ~ div12m_me**
- Intercept (β₀): 0.1082 (SE: 0.0060, p-value: <0.001)
- Slope (β₁): -0.0687 (SE: 0.0325, p-value: 0.0346)
- R²: 0.0018 | N: 2,527

**Model 2: ret ~ prime_rate**
- Intercept (β₀): 0.1998 (SE: 0.0158, p-value: <0.001)
- Slope (β₁): -0.0194 (SE: 0.0030, p-value: <0.001)
- R²: 0.0164 | N: 2,527

**Model 3: ret ~ ffo_at_reit**
- Intercept (β₀): 0.0973 (SE: 0.0092, p-value: <0.001)
- Slope (β₁): 0.5770 (SE: 0.5675, p-value: 0.3093)
- R²: 0.0004 | N: 2,518

*Note: Model 3 may have fewer observations if ffo_at_reit has missing values; statsmodels drops those rows.*

---

## 3. Slope Interpretation (Economic Units)

**Dividend Yield (div12m_me):**
- A 1 percentage point increase in dividend yield (12-month dividends / market equity) is associated with a **-6.87 percentage point** decrease in annual return.
- Higher dividend yield is associated with lower returns in this sample. This counterintuitive result may reflect that REITs with high dividend yields are often distressed or facing limited growth opportunities, leading investors to demand higher yields as compensation for risk. Alternatively, high-dividend REITs may have less cash available for reinvestment and growth.

**Prime Loan Rate (prime_rate):**
- A 1 percentage point increase in the year-end prime rate is associated with a **-1.94 percentage point** decrease in annual return.
- The evidence strongly suggests that REIT returns are negatively sensitive to interest rates. This makes economic sense: REITs are capital-intensive businesses that rely on debt financing, and they compete with bonds for investor capital. When interest rates rise, borrowing costs increase and bond yields become more attractive, reducing demand for REITs and lowering their returns.

**FFO to Assets (ffo_at_reit):**
- A 1 unit increase in FFO/Assets (fundamental performance) is associated with a **57.7 percentage point** increase in annual return.
- While the point estimate suggests that more profitable REITs (higher FFO/Assets) earn higher returns, this relationship is not statistically significant. The large standard error and lack of significance suggest that cross-sectional variation in FFO/Assets does not reliably predict returns in this dataset.

---

## 4. Statistical Significance

For each slope, at the 5% significance level:
- **div12m_me:** Significant (p = 0.0346) — We can reject the null hypothesis that dividend yield has no relationship with annual returns, though the evidence is modest.
- **prime_rate:** Significant (p < 0.001) — We have very strong evidence that the prime rate is negatively related to REIT returns, with a highly significant t-statistic of -6.49.
- **ffo_at_reit:** Not significant (p = 0.3093) — We cannot reject the null hypothesis that FFO/Assets has no relationship with returns; the positive slope may simply be due to sampling variation.

**Which predictor has the strongest statistical evidence of a relationship with annual returns?** The prime rate shows by far the strongest statistical evidence, with a t-statistic of -6.49 and p-value near zero. This suggests that interest rate sensitivity is a robust and important driver of REIT returns.

---

## 5. Model Fit (R-squared)

Compare R² across the three models:
- The prime rate model has the highest R² at 1.64%, explaining about 1.6% of the variation in annual REIT returns. The dividend yield model explains only 0.18%, and the FFO/Assets model explains essentially nothing (0.04%).
- These R² values are all very low, indicating that each single predictor alone explains very little of the variation in REIT returns. This is not surprising for annual stock returns, which are notoriously difficult to predict and are driven by many factors including market-wide movements, sector trends, property-specific news, and idiosyncratic shocks.
- The low R² suggests that (1) REIT returns are driven by many omitted variables, (2) there is substantial unpredictable (random) variation in returns, and (3) simple univariate models are insufficient for forecasting. A multiple regression model that includes several predictors simultaneously might improve explanatory power.

---

## 6. Omitted Variables

By using only one predictor at a time, we might be omitting:
- **Market returns (overall stock market performance)**: REITs are part of the broader equity market and their returns are likely correlated with market-wide movements. If market returns are high during low-interest-rate periods, omitting the market return could bias our prime rate coefficient.
- **Property type/sector**: Different REIT sectors (residential, office, retail, industrial) may have different return profiles and sensitivities to interest rates or dividends. Omitting sector controls could mask important heterogeneity.
- **Firm size and leverage**: Larger REITs or those with different debt levels may respond differently to interest rates. If leverage is correlated with both dividend yield and returns, our dividend yield slope may be capturing a leverage effect rather than a pure dividend effect.

**Potential bias:** For example, if low interest rates coincide with strong economic growth (an omitted variable), and both affect REIT returns positively, then our estimated negative coefficient on prime_rate may be overstated (too negative). Similarly, the negative coefficient on dividend yield might be biased if high-dividend REITs are also high-leverage firms facing financial distress (omitted distress indicator).

---

## 7. Summary and Next Steps

**Key Takeaway:**
Among the three predictors examined, the prime loan rate shows the strongest and most economically meaningful relationship with REIT annual returns. A 1 percentage point increase in the prime rate is associated with a 1.94 percentage point decrease in returns (t = -6.49, p < 0.001), consistent with the theory that REITs are interest-rate-sensitive assets. Dividend yield also shows a significant but weaker negative relationship, which may reflect distress or limited growth opportunities among high-yield REITs. FFO/Assets shows no significant relationship with returns, suggesting that fundamental profitability metrics do not strongly predict cross-sectional return variation in this annual sample.

**What we would do next:**
- Extend to multiple regression (include two or more predictors) to control for confounding and estimate partial effects
- Test for heteroskedasticity and other OLS assumption violations to ensure our standard errors are reliable
- Examine whether relationships vary by time period or REIT sector, as sensitivities may differ across market conditions and property types
- Include market returns and other macroeconomic variables to better isolate the effect of each predictor

---

## Reproducibility Checklist
- [x] Script runs end-to-end without errors
- [x] Regression output saved to `Results/regression_div12m_me.txt`, `regression_prime_rate.txt`, `regression_ffo_at_reit.txt`
- [x] Scatter plots saved to `Results/scatter_div12m_me.png`, `scatter_prime_rate.png`, `scatter_ffo_at_reit.png`
- [x] Report accurately reflects regression results
- [x] All interpretations are in economic units (not just statistical jargon)
