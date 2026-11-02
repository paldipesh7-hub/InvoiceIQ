# InvoiceIQ – Week 1 Progress Report

## 1. Objective

The objective of Week 1 was to inspect, validate, clean and prepare the selected invoice dataset for future analysis and machine learning tasks.

## 2. Dataset Overview

| Description | Result |
|---|---:|
| Original records | 2,000,000 |
| Original columns | 31 |
| Final columns | 39 |
| Missing values in original data | 0 |
| Duplicate rows | 0 |
| Duplicate invoice IDs | 0 |

## 3. Data Quality Checks

The following checks were performed:

- Missing-value analysis
- Duplicate-record analysis
- Date-format validation
- Invoice-date and due-date validation
- Negative financial-value checks
- Zero-value analysis
- Financial calculation validation
- Payment-status analysis
- Currency standardisation

No invalid dates, duplicate invoice IDs or negative financial values were found in the checks performed.

Financial calculations were validated with a tolerance of 0.02, with no mismatches found.

## 4. Payment Status Distribution

| Payment Status | Number of Invoices |
|---|---:|
| Paid | 1,358,819 |
| Pending | 341,015 |
| Overdue | 199,777 |
| Cancelled | 100,389 |
| **Total** | **2,000,000** |

## 5. Payment Date Investigation

A detailed investigation identified an unusual pattern:

- All Paid invoices were paid on or before their due dates.
- No Paid invoices had positive payment delays.
- Pending, Overdue and Cancelled invoices had payment dates equal to their due dates.
- Paid invoice payment delays ranged from -60 to 0 days.
- Average payment delay for Paid invoices was approximately -15.02 days.

Therefore, the payment dates of non-Paid invoices were not treated as confirmed actual payment dates.

## 6. Data Transformation

The following additional columns were created:

- payment_date_clean
- invoice_to_due_days
- days_to_pay
- payment_delay_days
- paid_late_flag
- is_paid
- is_open
- overdue_target

Original payment-date information was preserved.

## 7. Important Limitation

The selected dataset does not contain confirmed examples of invoices paid after their due dates.

Consequently, actual late-payment prediction using historical payment-delay values cannot currently be validated with this dataset.

The `overdue_target` column was created from the existing payment-status field as an alternative status-based classification target. It should not be interpreted as a verified actual late-payment outcome.

Future modelling must avoid using target-derived columns as input features.

## 8. Deliverables Completed

- Cleaned invoice dataset
- Data dictionary
- Data cleaning log
- Jupyter Notebook
- README documentation

## 9. Conclusion

Week 1 successfully established a structured and documented invoice dataset for further analysis.

The data-quality investigation also identified an important limitation in the payment-date information. This finding has been documented to ensure that future analysis and modelling remain transparent and avoid misleading conclusions.

**Project:** InvoiceIQ  
**Stage:** Week 1 – Data Cleaning