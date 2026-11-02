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

## Next Steps

- Exploratory Data Analysis (EDA)
- Data visualisation
- Feature engineering
- Payment-status analysis
- Predictive modelling
- Model evaluation

---

**Project:** InvoiceIQ  
**Internship:** AI/ML Internship  
**Stage:** Week 1 – Data Cleaning