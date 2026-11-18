# InvoiceIQ – Week 3 Feature Engineering Report

## 1. Project Overview

Project: InvoiceIQ – Invoice Payment Delay & Cash-Flow Intelligence Platform

Organisation: Orvians Technologies

Week: 3 – Feature Engineering and ML Data Preparation

Objective:
Transform the cleaned invoice dataset into machine-learning-ready
features while maintaining chronological separation and preventing
data leakage.

## 2. Dataset Information

Source dataset: Organisation-provided Global B2B Invoice and Payments Dataset.

Cleaned dataset: data/cleaned/InvoiceIQ_Cleaned_Data.csv

Total records: 2,000,000

Total original columns: 39

Invoice date range: 2024-01-01 to 2025-12-31

## 3. Feature Engineering

### Time Features

The following features were created:

- invoice_month
- invoice_weekday
- is_month_end
- payment_term_days

Payment term days represents the number of days between
invoice date and due date.

The invoice date was used as the prediction reference date.

### Customer Historical Features

The following historical features were created:

- customer_previous_invoice_count
- customer_previous_avg_amount
- customer_previous_avg_delay
- customer_previous_late_rate
- customer_no_invoice_history
- customer_no_payment_history

Historical information was restricted to information available
before the current invoice's prediction date.

Invoices generated on the same date were excluded from one
another's historical invoice calculations.

Payment history was restricted to payments completed before
the current invoice date.

### Amount Features

The following features were created:

- customer_currency_previous_avg_amount
- customer_amount_vs_history
- customer_amount_vs_history_log
- customer_no_same_currency_history

Historical amount comparisons were calculated separately
for each customer and currency.

The original total_amount distribution had positive skewness
of approximately 1.03. A logarithmic transformation of the
original amount overcorrected the skewness, so the original
amount was retained.

## 4. Target Variables

### Regression Target: delay_days

Calculated using actual cleaned payment date minus due date.

Only invoices with known completed payment outcomes were
included in regression target datasets.

Target observations:

- Early payments: 1,305,067
- On-time payments: 53,752
- Late payments: 0
- Unknown payment outcomes: 641,181

### Classification Target: paid_late

Definition:

- 1 = Payment made after due date
- 0 = Payment made on or before due date
- Missing = Payment outcome unavailable

No positive late-payment examples were present in the dataset.

Therefore, meaningful late-payment classification cannot
currently be trained or evaluated.

The dataset must not be treated as evidence of a validated
late-payment prediction model.

## 5. Chronological Data Split

The dataset was divided by invoice date without random shuffling.

| Split | Date range | Records |
|---|---|---:|
| Training | 2024-01-01 to 2024-12-31 | 1,001,116 |
| Validation | 2025-01-01 to 2025-06-30 | 495,347 |
| Testing | 2025-07-01 to 2025-12-31 | 503,537 |

Regression target availability:

| Split | Known outcomes | Unknown outcomes |
|---|---:|---:|
| Training | 680,398 | 320,718 |
| Validation | 336,301 | 159,046 |
| Testing | 342,120 | 161,417 |

## 6. Encoding and Scaling

Numerical features:
- Missing values imputed using training-set medians.
- StandardScaler fitted on training data only.

Categorical features:
- Missing values imputed using training-set most frequent values.
- OneHotEncoder used with handle_unknown='ignore'.

Frequency encoding:
- sales_rep encoded using training-set frequencies only.
- The same mapping applied to validation and testing data.
- Unseen categories handled with a frequency of zero.

The preprocessing pipeline was fitted only on training data.

## 7. Final ML-Ready Features

The final pipeline contains 31 raw predictor columns before
encoding:

| Raw feature group | Count |
|---|---:|
| Numerical | 20 |
| Categorical | 10 |
| Frequency encoded | 1 |
| Total raw predictors | 31 |

After preprocessing and encoding, the final feature matrices
contain 193 machine-learning predictor features.

| Encoded feature group | Count |
|---|---:|
| Numerical | 20 |
| One-hot encoded categorical | 172 |
| Frequency encoded | 1 |
| Total | 193 |

The categorical feature count includes four amount-bucket
categories.

### Amount Bucket Engineering

The total_amount feature was divided into four categories
using quartile boundaries calculated exclusively from the
training data.

| Boundary | Training-set value |
|---|---:|
| Q1 | 9,487.945 |
| Q2 (Median) | 25,372.315 |
| Q3 | 51,515.99 |

The resulting categories are:

- Low Amount
- Medium Amount
- High Amount
- Very High Amount

The same training-derived boundaries were applied to
training, validation, and testing datasets. No validation
or testing information was used to calculate the boundaries.

The bucket configuration was saved separately as
amount_bucket_config.joblib.

Final regression dataset shapes:

| Dataset | Feature shape |
|---|---:|
| Training | 680,398 x 193 |
| Validation | 336,301 x 193 |
| Testing | 342,120 x 193 |

All feature matrices were stored as sparse CSR matrices
for efficient memory usage.

## 8. Data Leakage Audit

The following outcome-related columns were excluded
from model predictors:

- payment_date
- payment_date_clean
- payment_delay_days
- days_to_pay
- paid_late_flag
- payment_status
- is_paid
- is_open
- is_overdue
- overdue_target
- paid_late
- delay_days

Historical customer features were calculated using only
eligible prior information.

The encoded feature audit found no forbidden outcome columns.

Targets were kept separate from predictors.

## 9. Saved Deliverables

The following 13 files were saved in data/processed/:

- X_train.npz
- X_validation.npz
- X_test.npz
- y_train.npy
- y_validation.npy
- y_test.npy
- feature_catalogue.csv
- detailed_feature_catalogue.csv
- preprocessor.joblib
- sales_rep_frequency_map.joblib
- chronological_split_summary.csv
- leakage_audit.csv
- amount_bucket_config.joblib

The saved feature matrices, targets, preprocessing pipeline,
frequency mapping, and amount-bucket configuration were
reloaded and verified.

All nine reload verification checks passed:

1. Training feature matrix
2. Validation feature matrix
3. Testing feature matrix
4. Training target
5. Validation target
6. Testing target
7. Preprocessor
8. Sales representative frequency mapping
9. Amount-bucket configuration

Verification result: 9 passed, 0 failed.

## 10. Limitations and Assumptions

1. No late-payment examples were present in the dataset.
2. Classification modelling for paid_late is therefore not
   currently feasible.
3. Regression modelling is limited to paid invoices and
   observed early/on-time payment delays.
4. Results cannot establish performance on late payments.
5. Historical features depend on the availability and
   correctness of prior invoice and payment records.
6. The raw payment_date column was not treated as an actual
   payment outcome because it contained placeholder values.
7. The current regression dataset represents paid invoices,
   not all invoices at the time they are issued.

## 11. Conclusion

Week 3 successfully transformed the cleaned invoice dataset
into 193 machine-learning predictor features.

Chronological splitting, training-only preprocessing,
historical customer feature engineering, categorical encoding,
sparse matrix storage, and leakage checks were completed.

All saved datasets were successfully reloaded and verified.

The absence of late-payment examples was identified as a
significant dataset limitation and documented for future
modelling decisions.

## 12. Point-in-Time Historical Feature Validation

An independent sample of 200 invoices was checked against the original dataset to validate the historical customer features.

The following five features were tested:

1. customer_previous_invoice_count
2. customer_previous_avg_amount
3. customer_previous_avg_delay
4. customer_previous_late_rate
5. customer_currency_previous_avg_amount

**Validation Results:**

| Historical Feature | Passed | Failed |
|---|---:|---:|
| Previous Invoice Count | 200 | 0 |
| Previous Average Amount | 200 | 0 |
| Previous Average Delay | 200 | 0 |
| Previous Late Rate | 200 | 0 |
| Previous Same-Currency Average Amount | 200 | 0 |
| **Total** | **1,000** | **0** |

All 1,000 comparisons passed successfully, with zero failures.

This sample-based validation provides additional evidence that the historical customer features respect the prediction-time boundary and use only information available before the current invoice date.

**Validation Limitation:** This was a sample-based audit of 200 invoices, not an exhaustive verification of all 2 million records.
