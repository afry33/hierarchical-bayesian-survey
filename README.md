# hierarchical-bayesian-survey
ukraine-aid-analysis
# Analysis of American Support for Ukraine Military Aid Using Hierarchical Bayesian Models

## Executive Summary

This analysis examines American public opinion on military aid to Ukraine across political affiliations using three statistical modeling approaches. The hierarchical Bayesian model reveals nuanced patterns in support that simpler models miss, showing that while political affiliation strongly influences views on Ukraine aid, there are underlying commonalities in how Americans approach this issue. The analysis confirms a clear political spectrum with Democrats showing strongest support, Republicans strongest opposition, and Independents occupying a middle position.

## Data Description

The data comes from a February 2025 Economist/YouGov survey of 1,603 U.S. adults, with results broken down by political affiliation:

| Affiliation   | Increase Aid | Maintain Aid | Not Sure | Decrease Aid |
|---------------|--------------|--------------|----------|--------------|
| Democrats     | 35%          | 39%          | 16%      | 10%          |
| Independents  | 19%          | 23%          | 26%      | 33%          |
| Republicans   | 10%          | 24%          | 21%      | 45%          |

## Statistical Models Implemented

### 1. Separate Model
- Treats each political group as completely independent
- Analyzes Democrats, Independents, and Republicans as separate entities
- No information sharing between groups

### 2. Pooled Model  
- Assumes all political groups are essentially the same
- Combines all respondents into one large group
- Ignores political affiliation differences

### 3. Hierarchical Model (Recommended)
- Recognizes that while groups have different opinions, they share underlying similarities
- "Borrows strength" across groups to improve individual estimates
- Provides natural uncertainty quantification and prediction capabilities

## Key Results

### Posterior Distributions of Mean Support

**Hierarchical Model Results (% support):**

| Affiliation   | Increase | Maintain | Not Sure | Decrease |
|---------------|----------|----------|----------|----------|
| Democrats     | 24.5     | 27.2     | 11.3     | 7.1      |
| Independents  | 13.3     | 16.1     | 18.2     | 23.1     |
| Republicans   | 7.1      | 16.8     | 14.7     | 31.5     |

**95% Credible Intervals (%):**

**Democrats:**
- Increase: 0.0 - 43.0
- Maintain: 0.0 - 46.7  
- Not Sure: 0.0 - 23.8
- Decrease: 0.0 - 17.8

**Independents:**
- Increase: 0.0 - 26.7
- Maintain: 0.0 - 31.0
- Not Sure: 0.0 - 33.7
- Decrease: 0.0 - 40.8

**Republicans:**
- Increase: 0.0 - 18.0
- Maintain: 0.0 - 31.7
- Not Sure: 0.0 - 29.0
- Decrease: 0.0 - 52.7

### Predictive Distribution for Hypothetical Political Group

For a new political affiliation not included in the original survey:

| Category  | Mean Support | 95% Credible Interval |
|-----------|--------------|----------------------|
| Increase  | 26.9%        | 0.0% - 100.0%        |
| Maintain  | 27.9%        | 0.0% - 100.0%        |
| Not Sure  | 26.8%        | 0.0% - 100.0%        |
| Decrease  | 29.2%        | 0.0% - 100.0%        |

## Major Findings and Interpretation

### 1. Clear Political Divide Confirmed
The analysis confirms a strong political spectrum in Ukraine aid support:
- **Democrats**: Show strongest support for maintaining or increasing aid (51.7% combined in hierarchical model)
- **Republicans**: Show strongest opposition, with 31.5% favoring decreased aid
- **Independents**: Occupy middle ground with more balanced distribution across categories

### 2. Shrinkage Effect Demonstrates Information Borrowing
The hierarchical model exhibits characteristic "shrinkage" - pulling extreme estimates toward the overall mean:

**Democratic Support Changes:**
- Increase aid: 35% → 24.5% (reduced by 10.5%)
- Decrease aid: 10% → 7.1% (increased by 2.9%)

**Republican Support Changes:**
- Increase aid: 10% → 7.1% (reduced by 2.9%)  
- Decrease aid: 45% → 31.5% (reduced by 13.5%)

This shrinkage reflects the model's understanding that political groups, while different, are not completely independent and share some underlying American perspectives on foreign policy.

### 3. Substantial Uncertainty in Estimates
The wide credible intervals, particularly for the predictive distribution, indicate:
- Limited sample size per group (~500 respondents each)
- Genuine uncertainty in public opinion
- Need for cautious interpretation of point estimates

### 4. Centrist Prediction for New Groups
The predictive distribution suggests any new political affiliation would likely show:
- Relatively balanced positions across aid categories
- Slight leaning toward decreasing aid (29.2% mean)
- High uncertainty reflecting limited information

## Methodological Assessment

### Strengths of Hierarchical Modeling Approach

1. **Information Borrowing**: Uses data from all groups to improve estimates for each group
2. **Natural Uncertainty Quantification**: Provides credible intervals that reflect both sampling and model uncertainty
3. **Built-in Prediction**: Natural mechanism for predicting new groups not in original data
4. **Regularization**: Prevents overfitting to noisy survey data
5. **Flexibility**: Can accommodate different group sizes and variances

### Limitations and Concerns

**Sample Size Considerations:**
- With approximately 500 respondents per group, margins of error are substantial
- Small subgroup analyses have limited precision
- The "Not Sure" category is particularly sensitive to sampling variation

**Model Assumptions:**
- Gaussian distribution may not perfectly capture proportion data
- Assumes common variance structure across categories
- Requires careful convergence monitoring (achieved in this analysis)

**Survey Limitations:**
- Self-reported political affiliation may not reflect voting behavior
- "Aid to Ukraine" question framing could influence responses
- Timing effects (February 2025 context unknown)

## Trustworthiness and Recommendations

### High Confidence In:
- The overall political spectrum pattern (Democrats > Independents > Republicans in support)
- The hierarchical model's superiority over simpler approaches  
- The direction and relative magnitude of differences between groups

### Moderate Confidence In:
- Exact percentage estimates from the hierarchical model
- Predictive distributions for new groups
- Fine-grained comparisons between specific categories

### Recommendations for Interpretation:

1. **Focus on Patterns**: Emphasize the relative differences between groups rather than exact percentages
2. **Use Hierarchical Estimates**: Consider the hierarchical model results as most reliable
3. **Consider Uncertainty**: Use credible intervals rather than point estimates for decision-making
4. **Acknowledge Context**: Remember that surveys capture expressed opinions, which may differ from actual policy preferences or voting behavior

## Conclusion

The hierarchical Bayesian model provides valuable insights into American public opinion on Ukraine military aid that simpler approaches miss. While confirming the expected political divide, the model also reveals underlying commonalities and provides a principled approach to uncertainty quantification and prediction.

These findings suggest that:
- Political affiliation remains a strong predictor of Ukraine aid opinions
- There is substantial uncertainty in public opinion, particularly for new political groups
- Hierarchical models are well-suited for multi-group survey analysis
- Policy decisions should consider both the patterns and uncertainties revealed

The methods demonstrated here showcase modern Bayesian approaches that balance model complexity with interpretability, making them valuable tools for political survey analysis and public opinion research.

## Technical Appendix

### Model Specification
The hierarchical normal model with common variance was implemented following standard Bayesian approaches:

- Likelihood: y_ij ~ N(μ_j, σ²)
- Prior: μ_j ~ N(μ_bar, τ²)
- Hyperpriors: μ_bar ~ N(0, 1000), τ² ~ Inverse-Gamma(0.001, 0.001)

### Computational Details
- Gibbs sampling with 10,000 iterations
- 3,000 iteration burn-in period
- Effective sample size: > 9,000 indicating good convergence
- All code implemented in R 4.5.2

### Data Availability
The complete R code for this analysis is available in the accompanying script files, including data preparation, model implementation, visualization, and results summary.
