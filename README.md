# InvoiceIQ – Invoice Payment Delay & Cash-Flow Intelligence Platform

## Project Overview

InvoiceIQ is an AI/ML project focused on analysing invoice and payment information to understand payment behaviour, identify overdue invoices, and support cash-flow intelligence.

This project is being developed as part of an 8-week AI/ML internship.

## Week 1 – Data Collection and Cleaning

The objective of Week 1 was to transform raw invoice data into a clean, structured and analysis-ready dataset.

### Dataset Information

- Total records: 2,000,000
- Original columns: 31
- Cleaned columns: 39
- Missing values in original columns: 0
- Duplicate invoice IDs: 0
- Duplicate complete rows: 0

### Technologies Used

- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Jupyter Notebook
- VS Code

### Data Cleaning Activities

1. Loaded the original invoice dataset using Pandas.
2. Inspected dataset dimensions and data types.
3. Checked missing values and duplicate records.
4. Converted invoice, due and payment dates into datetime format.
5. Checked invalid dates and impossible date combinations.
6. Checked negative financial values.
7. Validated subtotal and total amount calculations.
8. Standardised currency and text fields.
9. Created additional analytical columns.
10. Saved the cleaned dataset and documentation.

### Important Data Quality Finding

All Paid invoices have payment dates on or before their due dates. The dataset contains no Paid invoices with a positive payment delay.

Additionally, Pending, Overdue and Cancelled records have payment dates equal to their due dates. These dates have therefore not been treated as confirmed actual payment dates.

This limitation has been documented and must be considered during future modelling.

### New Columns Created

- payment_date_clean
- invoice_to_due_days
- days_to_pay
- payment_delay_days
- paid_late_flag
- is_paid
- is_open
- overdue_target

### Project Structure

```text
InvoiceIQ/
│
├── data/
│   ├── raw/
│   └── cleaned/
│
├── notebooks/
│
├── scripts/
│
├── reports/
│
└── README.md
```

### Week 1 Deliverables

- Cleaned invoice dataset
- Data dictionary
- Data cleaning log
- Data cleaning Jupyter Notebook
- Project documentation

## Week 2 – Exploratory Data Analysis (EDA)

The objective of Week 2 was to analyse the cleaned invoice dataset, understand payment behaviour, identify outstanding invoices, and extract meaningful business insights that can support future predictive modelling.

### EDA Activities

1. Analysed the overall invoice distribution and financial amounts.
2. Studied payment behaviour using Days to Pay and Payment Delay.
3. Analysed invoice payment statuses: Paid, Pending, Overdue and Cancelled.
4. Examined outstanding invoice balances separately across currencies.
5. Performed customer-level and country-level payment analysis.
6. Analysed monthly invoice volume and payment trends.
7. Conducted outstanding invoice ageing analysis.
8. Examined correlations between numerical features.
9. Identified potential features and targets for future machine learning models.
10. Documented business insights, data limitations and modelling considerations.

### Key Dataset Findings

- Total invoices analysed: 2,000,000
- Total original columns: 31
- Engineered columns: 39
- Verified paid invoices: 1,358,819
- Pending invoices: 341,015
- Overdue invoices: 199,777
- Cancelled invoices: 100,389
- Outstanding invoices (Pending + Overdue): 540,792

### Important Analytical Findings

- Approximately 67.94% of invoices were marked as Paid.
- Approximately 27.04% of invoices were classified as outstanding.
- Average Days to Pay for verified paid invoices was 15 days.
- The average Payment Delay was approximately -15.02 days, indicating early payment behaviour.
- No verified positive payment-delay examples were found among paid invoices.
- Outstanding balances were analysed separately by currency to avoid misleading cross-currency aggregation.
- Approximately 87.14% of past-due outstanding invoices fell into the 90+ days ageing category, using a provisional analysis cutoff of 31 December 2025.

### Business Insights and Visualisations

The analysis included:

- Invoice amount distribution across currencies.
- Days to Pay and Payment Delay distributions.
- Outstanding invoice ageing analysis.
- Invoice amount versus payment delay.
- Country-wise payment behaviour.
- Monthly invoice volume and payment trends.
- Customer-level overdue-status analysis.
- Correlation analysis between numerical features.

### Machine Learning Considerations

The EDA identified potential directions for future machine learning development, including:

- Invoice payment-status classification.
- Outstanding invoice analysis.
- Customer payment behaviour analysis.
- Cash-flow and outstanding-balance intelligence.

**Important limitation:** The dataset does not contain verified positive late-payment examples among paid invoices. Therefore, a reliable model for predicting actual late payments cannot be developed from the current verified paid-payment outcomes alone. Additional representative labelled data may be required.

Payment Delay and Days to Pay must also be excluded from features used for predictions made before payment, as these values depend on future payment information and could cause data leakage.

### Week 2 Deliverables

- Exploratory Data Analysis Jupyter Notebook.
- EDA report and business insights.
- Data visualisation charts.
- Customer, country and payment-status analysis.
- Outstanding invoice ageing analysis.
- Machine learning feasibility observations.
- Project documentation and submission report.
## Next Steps

- Exploratory Data Analysis (EDA)
- Data visualisation
- Feature engineering
- Payment-status analysis
- Predictive modelling
- Model evaluation

## Next Steps

- Feature selection and feature engineering.
- Machine learning dataset preparation.
- Model development and training.
- Model evaluation and performance comparison.
- Payment-status prediction.
- Cash-flow intelligence and reporting.
- Development of the InvoiceIQ web application.

---

**Project:** InvoiceIQ  
**Internship:** AI/ML Internship  
**Stage:** Week 1 – Data Cleaning
**Stage:** Week 2 – Exploratory Data Analysis (EDA)