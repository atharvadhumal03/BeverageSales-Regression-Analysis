# Figures Directory

This directory contains all visualizations and statistical outputs generated from the Beverage Sales Profit Analysis project.

## Figure Descriptions

### 1.heatmap.png
**Description**: Correlation matrix heatmap showing relationships between numerical features
**Key Insights**:
 - Strong positive correlation between units_sold and operating_profit (0.87)
 - Very high correlation between total_sales and operating_profit (0.94)
 - Operating margin shows weak negative correlations with all features
**Purpose**: Identify multicollinearity and feature relationships for model development

### 2.First Model - OLS.png
**Description**: Complete statsmodels OLS regression summary table
**Model Stats**:
 - R-squared: 0.852
 - 19 predictors (including all dummy variables)
 - 6 non-significant features identified
**Purpose**: Document initial model performance and coefficient significance

### 3.Redefined Model - OLS.png
**Description**: OLS summary after removing non-significant features
**Model Stats**:
 - R-squared: 0.852 (maintained)
 - 14 predictors (all significant at p < 0.01)
 - Improved condition number: 10.7
**Purpose**: Show improved model parsimony without sacrificing performance
