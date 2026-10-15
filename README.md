# Retail Sales Analytics & Revenue Forecasting

## Project Overview
This project analyzes online retail transactions to understand sales performance, identify business trends, and forecast daily revenue using machine learning.

## Business Objectives
- Analyze overall retail revenue and sales performance.
- Identify monthly revenue trends.
- Find top-performing products and countries.
- Analyze customer purchasing patterns.
- Build and evaluate daily revenue forecasting models.
- Present insights through a Power BI dashboard.

## Tools & Technologies
- Python
- Pandas and NumPy
- Matplotlib
- Scikit-learn
- Jupyter Notebook
- Power BI
- Git and GitHub

## Project Structure
```text
Retail_Sales_Analytics/
├── Retail_Sales_Analytics.ipynb
├── README.md
├── data/
│   └── Online Retail.xlsx
├── outputs/
│   ├── retail_final_forecast.csv
│   ├── retail_final_model_comparison.csv
│   ├── retail_kpi_summary.csv
│   ├── monthly_sales.csv
│   ├── country_sales.csv
│   ├── top_products.csv
│   └── top_customers.csv
├── models/
│   ├── retail_best_model.pkl
│   └── retail_model_features.pkl
└── dashboard/
    └── Retail_Sales_Analytics.pbix
```

## Data Preparation
The workflow includes:
- Removing duplicate transactions.
- Excluding cancellation invoices from the sales analysis.
- Filtering non-positive quantities and unit prices.
- Converting invoice dates to datetime format.
- Calculating revenue as quantity multiplied by unit price.

Missing customer IDs limit customer-level analysis. Revenue calculations represent the cleaned sales data, not necessarily audited accounting revenue.

## Exploratory Data Analysis
The project explores:
- Overall revenue and transaction KPIs.
- Monthly revenue trends.
- Revenue by country.
- Best-performing products.
- Customer-level sales.
- Unusual transactions and zero-revenue days.

## Revenue Forecasting
The primary model is Random Forest with calendar and lag-based features.

Features include:
- Previous-day revenue.
- Revenue from seven days earlier.
- Previous seven-day average revenue.
- Day of week.
- Month.

### Model Evaluation

| Model | MAE | RMSE | R² |
|---|---:|---:|---:|
| Linear Regression + Calendar | 17060.665 | 25978.769 | 0.284 |
| Random Forest + Calendar | 13788.144 | 23796.083 | 0.400 |
| Random Forest + Calendar + Saturday Rule | 13784.248 | 23796.080 | 0.400 |

The Saturday adjustment produces only a negligible improvement in test metrics. It should only be used as a business rule if the zero-Saturday-sales pattern is confirmed as an operating constraint.

### Interpretation
- MAE measures average absolute prediction error.
- RMSE penalizes larger prediction errors more heavily.
- R² measures how much variation in the test-set revenue is explained by the model.

The results indicate that Random Forest performs better than the tested linear regression approach, but it still struggles to predict sudden revenue spikes.

## Power BI Dashboard
The Power BI report is saved in `dashboard/Retail_Sales_Analytics.pbix`.

Open it using Power BI Desktop to explore the dashboard and its available filters.

## Important Limitations
- The dataset covers December 2010 through December 9, 2011; December 2011 is incomplete.
- The dataset is historical and should not be treated as a current business forecast.
- Some unusually large transactions may substantially influence revenue and model evaluation.
- Missing customer IDs restrict customer-level analysis.
- Saturday revenue is zero throughout the cleaned dataset; the reason should be verified before applying a permanent business rule.
- Model metrics are based on a chronological holdout test set and may not generalize to other periods.

## How to Run
1. Install Python and Jupyter Notebook.
2. Install the required libraries:
   `pip install pandas numpy matplotlib scikit-learn openpyxl joblib`
3. Place the source dataset in the `data/` folder.
4. Open `Retail_Sales_Analytics.ipynb`.
5. Update file paths to match the project folder structure.
6. Run notebook cells in order.
7. Open the `.pbix` file in Power BI Desktop to view the dashboard.

## Future Improvements
- Compare forecasts with stronger seasonal baselines.
- Validate unusual transactions and operating-day assumptions.
- Add more rigorous time-series validation.
- Improve prediction of large revenue spikes.
- Refine Power BI relationships and interactive filtering.
- Add dashboard screenshots and documented business recommendations.

## Author
Created as a data analytics and machine learning portfolio project.
