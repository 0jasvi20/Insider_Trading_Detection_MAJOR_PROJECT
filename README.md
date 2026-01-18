# Insider Trading Detection – Data Preparation & Feature Engineering 
# week 1 - 16/1/26
# Overview
This repository contains the data acquisition, preprocessing, and feature engineering pipeline for a Major Project on Insider Trading Detection using Machine Learning.
The goal of this stage is to transform raw SEC insider trading filings into a clean, structured, and analysis-ready dataset that can later be used for anomaly detection, risk scoring, and time-series forecasting.

This work represents the foundational phase of a larger end-to-end system.

# Dataset Source

    1. Source: SEC Insider Trading Data (via Kaggle – layline/insidertrading)
    2. Data Type: Public regulatory filings (non-derivative transactions)
    3. Reason for selection:
        1. Authentic real-world financial data
        2. Large scale (millions of records)
        3. Rich insider role and transaction details
        4. Suitable for unsupervised learning due to the lack of labels

# What Has Been Implemented So Far
1. Dataset Download & Sampling
   
        1. Kaggle API was used to download the full insider trading dataset.
        2. Due to the large size, a 1 million row sample was created from:
               lit_nonderiv.csv (non-derivative insider transactions)
        3. A smaller 200,000 row sample was created from:
               lit_reportingowner.csv (insider role information)
        4. These samples are saved as reusable CSV files to avoid repeated downloads.

2. Transaction Data Cleaning

        From the non-derivative transaction dataset:
             1. Selected only relevant columns such as:
                  Accession number
                  Filing date
                  Transaction date
                  Transaction type (Buy/Sell)
                  Shares traded
                  Shares owned after the transaction
                  Ownership type (Direct/Indirect)
            2. Renamed columns for clarity and consistency.
            3. Encoded transaction type:
                Buy (Acquire) → 1
                Sell (Dispose) → 0
            4. Converted dates to proper datetime format.
            5. Converted share values to numeric.
            6. Removed rows with missing or invalid values.

        The result is a clean transaction-level dataset suitable for behavioural analysis.

3. Ownership & Insider Role Processing

        From the reporting owner dataset:

          1. Extracted insider role information:
                Director
                Officer
                Ten-percent owner

          2. Converted role indicators to binary format.
          3. Cleaned and standardised officer titles.
          4. Reduced the dataset to only role-relevant columns.
   
        This step enables linking transaction behavior with insider authority level.

4. Data Integration

        1. Merged transaction data and owner role data using the SEC accession number.
        2. Ensured missing role values were handled safely.
        3. Created a unified dataset containing both:
              Transaction behavior
              Insider role information

        This integration allows role-aware insider trading analysis.

5. Feature Engineering

        The following domain-driven features were created:

          1. Direct Ownership Flag
          Indicates whether the trade was made directly or indirectly.
          2. Top Insider Indicator (is_top_insider)
          Flags whether the trader is a director, officer, or major shareholder.
          3. Transaction vs Filing Gap (Initial version)
          Measures the delay between transaction date and SEC filing date
          (later corrected in subsequent phases).
  
        These features convert raw regulatory data into machine-learning-ready signals.

# Current Output

    A merged dataset with ~1.46 million records
    Clean numerical and categorical features
    Insider role enrichment
    Ready for:
      Anomaly detection
      Risk scoring
      Time-series aggregation

# Technologies & Libraries Used

    Python
    Pandas – data manipulation, cleaning, merging
    NumPy – numerical operations
    Kaggle API – dataset acquisition
