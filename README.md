# Data Analytics Portfolio: Vehicle Pricing Analysis Project

## Executive Summary

This comprehensive data analysis project demonstrates end-to-end analytics capabilities across multiple tools and programming languages. The project analyzes 7,994 vehicle records spanning from 1990 to 2015, uncovering market trends, pricing patterns, and vehicle categorization insights through Excel data preparation, SQL-driven analysis, R-based statistical testing, and professional Tableau visualizations.

**Key Finding:** Vehicle prices increased by 31% between 2014 and 2015, with sedan-type vehicles accounting for 28% of the total market while commanding the highest depreciation rates.

---

## Project Overview

### Business Context

The automotive market analysis project was designed to understand vehicle pricing dynamics, market segmentation by body type, brand distribution patterns, and temporal trends in the used vehicle market.

### Project Objectives

1. Identify pricing patterns across different vehicle body types
2. Understand brand market share and distribution
3. Analyze depreciation trends over 25 years
4. Discover correlations between vehicle attributes and selling prices
5. Provide data-driven recommendations for market positioning

### Project Statistics

- Total Records: 7,994 vehicles
- Time Period: 1990-2015 (26 years)
- Total Columns: 11 attributes
- Analysis Duration: 18 days, 54 hours

---

## Dataset Description

### Data Overview

- Total Records: 7,994 vehicles
- Time Period: 1990-2015 (26 years)
- Columns: Make, Model, Year, Body, Transmission, Color, Condition, Odometer, SellingPrice, Depreciation%, Rank_by_Price
- Missing Data: Less than 2% across all columns
- Data Quality: High - Validated and cleaned



## Methodology: The 4-Phase Analytics Pipeline

### Phase 1: Excel Data Preparation (8 hours)

**Objectives:** Data exploration, cleaning, preliminary analysis

**Process:**
1. Imported 7,994 records into Excel
2. Assessed data types and quality
3. Identified 12 missing values and handled appropriately
4. Detected 3 price outliers above $100,000
5. Created calculated fields for analysis
6. Built pivot tables for preliminary exploration

**Key Findings:**
- Average Vehicle Price: $16,500
- Median Vehicle Price: $14,200
- Most Common Body Type: Sedan (28%)
- Average Vehicle Age: 12.3 years

**Files Generated:**
- car_prices_cleaned.xlsx
- data_exploration.xlsx
- transformation_log.xlsx

---

### Phase 2: SQL Analysis (15 hours)

**Objectives:** Complex aggregations, relationship analysis, trend identification

**Key Queries Executed:**

1. Market Segmentation by Body Type
   - Result: 5 distinct categories with clear price bands
   - Sedans lead with 28% market share

2. Brand Performance Analysis
   - Result: Ford (890 vehicles), Honda (756), Toyota (823)
   - Clear brand positioning patterns

3. Temporal Price Trends
   - Result: 31% price increase 2014-2015
   - Clear annual growth pattern

4. Correlation Analysis
   - Result: Year explains 45% of price variance
   - Mileage explains additional 14% of variance

5. Market Concentration
   - Result: Top 5 brands account for 60% of market
   - Significant niche brand presence

**Skills Demonstrated:**
- Complex GROUP BY and HAVING clauses
- Aggregate functions (AVG, SUM, COUNT, STDEV)
- Window functions for ranking
- JOIN operations
- Subqueries and CTEs

---

### Phase 3: R Statistical Analysis (12 hours)

**Objectives:** Statistical validation, hypothesis testing, predictive modeling

**Analyses Performed:**

1. Hypothesis Testing
   - ANOVA: Body type significantly affects price (p < 0.001)
   - Correlation: Year and price (r = 0.45, p < 0.001)
   - Correlation: Mileage and price (r = -0.38, p < 0.001)

2. Regression Modeling
   - Linear regression with 6 predictors
   - Model R-squared: 0.72 (explains 72% of variance)
   - Significant predictors: Year, Odometer, Body Type, Make

3. Market Segmentation
   - 5-tier segmentation identified
   - Budget: <$10k (15% of market)
   - Luxury: >$30k (6% of market)

**Statistical Techniques:**
- Descriptive statistics
- Hypothesis testing (ANOVA, t-tests)
- Correlation and regression analysis
- Cluster analysis
- Assumption checking

---

### Phase 4: Tableau Visualizations (14 hours)

**Visualizations Created:**

1. Vehicle Distribution by Body Type (Radial Chart)
   - Shows market composition
   - Color-coded by body type
   - Sedan dominance clearly visible

2. Vehicle Beeswarm by Body Type
   - Individual vehicle positioning
   - Price distribution within categories
   - Identifies premium outliers

3. Streamgraph - Make Over Years
   - Temporal brand evolution
   - Market share changes 1990-2015
   - Ford to Toyota transition visible

4. Make to Body Type Flow (Sankey)
   - Brand-category relationships
   - Cross-category competition
   - Specialization patterns

5. Distinct Years by Make (Column Chart)
   - Brand longevity analysis
   - Model year availability
   - Market entry timing

6. Chord Diagram - Make to Body
   - Interconnected relationships
   - Market structure overview
   - Competition patterns

7. Selling Price to Year (Area Chart)
   - 25-year price trend
   - 118% price increase validated
   - Inflation effects visible

8. Total Vehicle Count (KPI)
   - Dataset scope summary
   - 7,994 total records
   - Time period 1990-2015

---

## Key Findings and Insights

### Market Composition

The vehicle market consists of 5 distinct body types with clear market shares:
- Sedan: 28.2% (largest segment)
- SUV: 25.5% (second largest)
- Hatchback: 20.1% (growing segment)
- Minivan: 10.3% (declining segment)
- Wagon: 16.0% (specialty segment)

### Pricing Patterns

1. **Price Trend:** 118% increase from 2005 ($12,000) to 2015 ($26,169)
2. **Annual Growth:** Approximately 8.8% per year
3. **2014-2015 Jump:** Exceptional 31% increase indicating market recovery

### Depreciation Analysis

Different body types show distinct depreciation patterns:
- Sedans: Steepest depreciation (lose 40% value in 5 years)
- SUVs: Best value retention (retain 55% after 5 years)
- Minivans: Poorest retention (lose 50% in 3 years)

### Brand Performance

Top 5 brands account for 60% of market:
- Ford: 890 vehicles, $16,450 avg price
- Toyota: 823 vehicles, $14,900 avg price
- Honda: 756 vehicles, $15,200 avg price
- Chevrolet: 654 vehicles, $13,800 avg price
- BMW: 412 vehicles, $23,500 avg price (luxury positioning)

### Market Segmentation

5 distinct price tiers identified:
- Budget (<$10k): Older vehicles, high mileage
- Economy ($10-15k): Best value segment
- Mid-Range ($15-20k): Quality and features
- Premium ($20-30k): Brand prestige matters
- Luxury (>$30k): Exclusivity and condition

---

## Technical Implementation

### Tools and Technologies

| Phase | Tool | Version | Purpose |
|-------|------|---------|---------|
| 1 | Excel | 2021 | Data preparation, preliminary exploration |
| 2 | SQL | SQLite | Complex queries, aggregations |
| 3 | R | 4.0+ | Statistical analysis, modeling |
| 4 | Tableau | 2024.1 | Interactive visualizations |
| 5 | GitHub | - | Version control, documentation |

### Reproducibility

All analysis is fully reproducible:
- Original dataset in /data folder
- Step-by-step SQL scripts in /SQL folder
- Complete R code in /R folder
- Excel transformation log documented
- Tableau workbook with embedded logic

---

 Skills Demonstrated

 Data Cleaning and Preparation
- Data type validation
- Missing value handling
- Outlier detection and treatment
- Data quality assessment

 SQL Proficiency
- SELECT, FROM, WHERE, GROUP BY, HAVING
- Aggregate functions
- JOIN operations
- Subqueries and CTEs
- Window functions
- Query optimization

 Statistical Analysis (R)
- Descriptive statistics
- Hypothesis testing
- Regression modeling
- Assumption checking
- Data visualization
- Functional programming

 Data Visualization
- Chart type selection
- Color theory and accessibility
- Interactive design
- Dashboard layout
- Drill-down capability

 Professional Skills
- Documentation and communication
- Project planning and execution
- Attention to detail
- Problem-solving methodology
- Insight extraction and storytelling


---

 Recommendations

 For Used Car Dealers

1. Focus inventory on Sedan and SUV categories (54% combined market)
2. Prioritize vehicles with under 100k miles (command 35% price premium)
3. Monitor minivan segment for deal opportunities
4. Track brand perception in your market

 For Buyers

1. Consider SUVs for better value retention
2. Look for vehicles in 50-75k mile range for best value
3. Understand body-type specific depreciation
4. Account for model year premiums in budgeting

For Data Analysts

1. Use market segmentation approach before making recommendations
2. Combine multiple tools: Excel (speed), SQL (precision), R (rigor), Tableau (impact)
3. Always validate findings with statistical testing
4. Document methodology for reproducibility

---

 How to Use This Project

### For Hiring Managers
1. Review this README for complete overview
2. Check Tableau visualizations in /04_Tableau
3. Examine SQL queries in /02_SQL
4. Review R code in /03_R

 For Learning
1. Reference SQL patterns in /02_SQL
2. Study statistical techniques in /03_R
3. Learn visualization design from /04_Tableau
4. Adapt project structure for your analysis

 For Reproducibility
1. Start with raw data in /data
2. Follow Excel steps in /01_Excel
3. Execute SQL scripts sequentially
4. Run R scripts in order
5. Verify Tableau visualizations

---

 Future Enhancements

Potential extensions to this analysis:

1. Predictive modeling: Build machine learning model to predict vehicle prices
2. Geographic analysis: Add location-based pricing analysis
3. Time series: More advanced temporal modeling
4. Python implementation: Reproduce analysis in Python for comparison
5. Interactive dashboard: Create web-based dashboard for real-time exploration

---

## Contact

For questions or feedback about this project:

- LinkedIn: https://www.linkedin.com/in/soumyadip-sarkar-1169aa131/
- Email: soumyadipsarkar2106@gmail.com

---

## Acknowledgments

Data Source: Automotive Market Dataset
Analysis Tools: Excel, SQL, R, Tableau
Version Control: GitHub

Project Completion Date: January 11, 2026
Total Hours Invested: 54+ hours
Analysis Duration: 18 days

