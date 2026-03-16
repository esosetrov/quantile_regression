# quantile_regression

Quantile regression implementation with statsmodels using Engel dataset. Analyzes conditional distributions, compares with OLS, visualizes results, and demonstrates inventory optimization applications. Includes diagnostics and alternative approaches.


## Overview

This notebook provides a complete workflow for quantile regression analysis, from basic implementation to advanced applications. Unlike ordinary least squares (OLS) regression which models conditional means, quantile regression models conditional quantiles, offering a more complete view of the relationship between variables across the entire distribution.

## Key Features

- **Complete Implementation**: Full quantile regression workflow using `statsmodels.QuantReg`.
- **Multiple Quantile Analysis**: Estimates from τ=0.05 to τ=0.95 with 0.1 increments.
- **Comparative Analysis**: Direct comparisons with OLS regression results.
- **Advanced Diagnostics**: Residual analysis, sparsity measures, heteroscedasticity detection.
- **Practical Applications**: Inventory optimization with reorder point calculation.
- **Alternative Approaches**: Composite quantile regression and methodological extensions.
- **Comprehensive Visualization**: Multiple plotting techniques for result interpretation.

## Key Findings from the Analysis

### 1. **Non-Constant Relationship**
The income coefficient increases from 0.3434 (τ=0.05) to 0.7091 (τ=0.95), demonstrating that the effect of income on food expenditure is not constant across the distribution.

### 2. **Heteroscedasticity Detection**
- Heteroscedasticity ratio R = 0.5094 > 0.
- Confirms increasing variability in food expenditure with higher income.
- Invalidates key OLS assumption of homoscedasticity.

### 3. **Model Comparisons**
- **OLS**: Intercept = 147.48, Slope = 0.4852, R² = 0.8304.
- **LAD (Median)**: Intercept = 81.48, Slope = 0.5602, Pseudo R² = 0.6206.
- **Composite Quantile (τ=0.25,0.5,0.75)**: Average slope = 0.5594.

### 4. **Practical Inventory Applications**
Service level reorder points at mean income:
- 70%: 677.46
- 80%: 705.96  
- 90%: 741.62
- 95%: 760.74

## Technical Implementation

### Libraries Used
- `statsmodels` (v0.14.0+) - Quantile regression implementation;
- `pandas` (v2.0.0+) - Data manipulation;
- `numpy` - Numerical operations;
- `matplotlib` - Visualization.

### Core Methodology

```python
# Basic quantile regression implementation
mod = smf.quantreg("foodexp ~ income", data)
res = mod.fit(q=0.5)  # Median regression
```

### Advanced Techniques

1. **Multiple Quantile Estimation**: Simultaneous estimation across quantile spectrum
2. **Composite Quantile Regression**: Pooled estimation for improved efficiency
3. **Sparsity Analysis**: Quantile-specific precision assessment
4. **Confidence Intervals**: Point-wise and uniform confidence bands

## Project Structure

```
1. Environment Setup and Imports
2. Introduction and Theoretical Background
3. Data Loading and Exploration
4. Quantile Regression Analysis
5. Comparison with OLS Regression
6. Visualization of Results
7. Alternative Approaches and Extensions
8. Model Diagnostics
9. Practical Applications and Interpretation
10. Conclusion and Best Practices
11. References
```

## Applications

### Business & Economics
- **Demand Forecasting**: Tail behavior analysis for inventory management
- **Risk Assessment**: Extreme quantile analysis for financial risk
- **Policy Analysis**: Distributional effects of economic policies
- **Customer Segmentation**: Behavior analysis across different quantiles

### Supply Chain & Operations
- **Safety Stock Calculation**: Direct quantile-based reorder points
- **Service Level Optimization**: Trade-off analysis between inventory costs and service levels
- **Demand Planning**: Complete distribution forecasting rather than just mean predictions

## Visualizations Included

1. **Raw Data Scatter Plot**: Income vs. food expenditure with histograms
2. **Quantile Regression Lines**: Multiple quantile fits vs. OLS line
3. **Coefficient Comparison**: Income coefficients across quantiles with confidence intervals
4. **Residual Diagnostics**: Four-panel diagnostic plots for median regression
5. **Sparsity Analysis**: U-shaped pattern of estimation precision across quantiles

##  Key Insights for Practitioners

1. **Distribution Matters**: Average effects (OLS) can mask important distributional differences
2. **Tail Behavior**: Extreme quantiles often have different relationships than central ones
3. **Robustness**: Median regression (LAD) provides outlier-resistant estimates
4. **Decision Support**: Different quantiles support different business decisions
5. **Model Validation**: Always check for heteroscedasticity when using regression models

##  Limitations and Considerations

- **Computational Intensity**: Multiple quantile estimation requires more computation than OLS
- **Sample Size Requirements**: Reliable extreme quantile estimates need sufficient data
- **Interpretation Complexity**: Requires thinking in terms of distributions rather than single numbers
- **Crossing Quantiles**: Possible in nonlinear settings (less common in linear models)

## Academic Background

Based on seminal work by:
- **Roger Koenker & Gilbert Bassett (1978)**: Introduction of regression quantiles
- **Roger Koenker & Kevin F. Hallock (2001)**: Accessible economic applications
- **Ernst Engel (1857)**: Original Engel curve analysis

## Getting Started

### Prerequisites
```bash
pip install statsmodels pandas numpy matplotlib
```

### Basic Usage
```python
import statsmodels.api as sm
import statsmodels.formula.api as smf

# Load data
data = sm.datasets.engel.load_pandas().data

# Fit quantile regression
model = smf.quantreg("foodexp ~ income", data)
results = model.fit(q=0.5)  # Median regression
print(results.summary())
```

##  License

This project is licensed under the MIT License - see the LICENSE file for details.

## Contributing

This notebook serves as an educational resource. For questions, suggestions, or improvements, please open an issue or discussion.

# Note

This notebook is designed for educational and research purposes.
Real-world applications may require additional considerations and validation.