# BeverageSales-Regression-Analysis
ML project analyzing 7,700+ beverage sales transactions to predict operating profit using multiple linear regression, achieving 85% R-squared. 

## 📊 Project Overview
This project analyzes over 7,700 beverage sales transactions to understand and predict operating profit using multiple linear regression. The analysis explores how various factors including pricing strategies, sales volume, retailer partnerships, regional differences, and beverage brands impact profitability in the retail beverage industry.

### Features Used:
Numerical Features:
1. price_per_unit: Unit price of beverage
2. units_sold: Quantity sold per transaction
3. total_sales: Revenue per transaction

### Categorical Features:
1. retailer: Sales channel (Amazon, BevCo, FizzyCo, Target, Walmart, West Soda)
2. region: Geographic region (Northeast, South, Southeast, West, Midwest)
3. beverage_brand: Product type (Coca-Cola, Dasani Water, Diet Coke, Fanta, Powerade, Sprite)

### Engineered Features:
1. year: Extracted from invoice_date (2022, 2023)
2. season: Derived from month (Spring, Summer, Fall, Winter)
   
### Target Variable:
1. operating_profit: The profit generated from each transaction

## 🎯 Results Summary
### Initial Model Performance:
- R-squared: 0.852 (85.2% variance explained)
- Observations: 7,718
- Significant Predictors: price_per_unit, units_sold, select retailers, regions, and beverage brands

### Refined Model Performance:
- R-squared: 0.851 (maintained explanatory power)
- Features Removed: 6 insignificant predictors (p > 0.05)
- Model Simplification: Reduced from 19 to 13 predictors

### Key Business Insights:
- Volume is King: Units sold shows the strongest impact on profit (coef: 430.80)
- Pricing Matters: Each $1 increase in price adds $215.41 to profit
- Regional Performance: South region outperforms (+$61.58) while West underperforms (-$64.38)
- Brand Hierarchy: Coca-cola significantly outperforms all other beverages
- Retailer Impact: Walmart shows negative profit impact (-$42.58) compared to Amazon, while specialty retailers (FizzyCo, West Soda) add ~$19 more - consider channel optimization
- Growth Trajectory: 2023 shows only modest improvement (+$17) over 2022, suggesting operational efficiency gains

## 🔍 Methodology
### 1. Data Understanding & Quality Assessment
- Loaded and explored 7,718 transaction records
- Verified data integrity: No null values or duplicate records found
- Examined data types and basic statistics

### 2. Exploratory Data Analysis
#### Categorical Feature Distribution
- Analyzed distribution using value_counts() for retailers, regions, and beverage brands
- Identified balanced representation across categories

#### Numerical Feature Analysis
- **Correlation Analysis:** Discovered strong correlation between total_sales and operating_profit (0.935)
- **VIF Testing:** Identified severe multicollinearity when including total_sales with price and units
- **Outlier Detection**: Found 0.84% outliers in price_per_unit and 8.28% in total_sales using IQR method

### 3. Feature Engineering
- Extracted year from invoice_date
- Created season by mapping months:
    - Spring: January, February, March, April
    - Summer: May, June, July, August
    - Fall: September, October, November, December

### 4. Model Development Workflow
#### Data Preparation:
- Captured relevant features into X and the outcome (operating_profit) into y
- One-Hot Encoded the categorical features to sustain nominality of features
- Drop one encoded column from each category to prevent dummy variable trap and avoid multicollinearity
- Scaled numerical features in X_train using RobustScaler to optimize outliers, applied the same scale to X_test to prevent data leakage

#### Model Training & Evaluation:
- Fitted OLS regression model using statsmodels
- Evaluated using R-squared, adjusted R-squared, and coefficient significance
- Checked model assumptions through residual diagnostic

#### 5. Model Refinement
Identified 6 features with p-values > 0.05:
- retailer_BevCo, retailer_Target
- region_Southeast
- season_Summer, season_Winter
- beverage_brand_7UP (reference category)

Removed insignificant features and refitted model
Maintained R-squared of 0.851 with improved parsimony

## 📈 Visualizations
### 1. Numerical Feature Correlation Heatmap
Key Observations:
1. Strong positive correlation between units_sold and operating_profit (0.87)
2. Total_sales shows highest correlation with operating_profit (0.94)
3. Operating margin shows weak negative correlations with all features

### 2. Initial Model - OLS Summary
Model Statistics:
1. R-squared: 0.852
2. F-statistic: 2341 (p < 0.001)
3. 19 predictors including all categorical dummy variables

### 3. Refined Model - OLS Summary
Model Statistics:
1. R-squared: 0.851
2. Reduced to 13 significant predictors only
3. Improved model interpretability without sacrificing predictive power

## 🔑 Key Findings
**1. Sales Volume is the Primary Profit Driver**
Units sold demonstrates the strongest relationship with operating profit (coefficient: 430.80), indicating that each additional unit sold contributes $430.80 to profit. This effect is nearly double that of pricing, suggesting volume-based strategies offer the greatest profit potential.

**2. Pricing Shows Significant but Secondary Impact**
While price per unit positively impacts profit (+$215.41 per dollar increase), its effect is roughly half that of volume. This suggests aggressive pricing strategies should be balanced against potential volume impacts.

**3. Stark Performance Disparities Across Retailers**
Walmart significantly underperforms the Amazon baseline by $49.94 per transaction, while specialty beverage retailers (FizzyCo +$19.51, West Soda +$18.48) show superior profitability. This 3x profit gap between best and worst performers indicates substantial opportunity for channel optimization.

**4. Regional Markets Show 2.5x Profit Variance**
The South region outperforms by $61.58 per transaction while the West underperforms by $64.38, creating a $126 profit differential between regions. The Northeast also lags (-$27.82), suggesting geographic expansion should prioritize Southern markets.

**5. Coca-Cola Dominates the Brand Portfolio**
All alternative beverages show negative coefficients compared to Coca-Cola, with Diet Coke (-$82.87) and Powerade (-$74.26) showing the steepest profit penalties. Even the best-performing alternative (Dasani Water at -$24.26) generates significantly less profit than Coca-Cola.

**6. Modest Year-over-Year Growth**
The $17.28 profit increase from 2022 to 2023 represents only 4.5% growth relative to the base profit of $381.63, suggesting market maturity or need for operational improvements.

**7. Model Demonstrates Strong Predictive Power**
With an R-squared of 0.852 and all predictors showing p-values < 0.01, the model reliably captures profit drivers while maintaining parsimony after removing non-significant variables.

## 📁 Dataset Information
### Overview
The dataset contains transactional beverage sales data from major US retailers, capturing detailed information about pricing, volume, profitability, and operational metrics across different regions and time periods.

### Dataset Characteristics
- **Total Records:** 9648 transactions
- **Time Period:** 2022-2023 (2 years)
- **Geographic Coverage:** 5 US regions (Northeast, South, Southeast, West, Midwest)
- **Data Quality**: Complete dataset with no missing values or duplicates

### Features Description
#### Numerical Variables (5):
1. **price_per_unit:** Unit selling price of beverage products
2. **units_sold:** Quantity sold per transaction
3. **total_sales:** Total revenue per transaction (price × units)
4. **operating_profit:** Target variable - profit generated per transaction
5. **operating_margin:** Profit margin percentage (initially included, later excluded due to low correlation)

#### Categorical Variables (4)
1. **retailer (6 categories):** Amazon, BevCo, FizzyCo, Target, Walmart, West Soda
2. **region (5 categories):** Northeast, South, Southeast, West, Midwest
3. **beverage_brand (7 categories):** Coca-Cola, 7UP, Dasani Water, Diet Coke, Fanta, Powerade, Sprite
4. **invoice_date:** Transaction date (later engineered into year and season)
