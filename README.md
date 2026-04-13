# Week 08 - Monday: Time Series Analysis

PG Diploma | AI-ML and Agentic AI Engineering | IIT Gandhinagar

## Overview

This submission covers all seven sub-steps of the Week 08 Monday assignment on Time Series
Foundations and Modeling. The two datasets analysed are daily e-commerce sales and
industrial sensor readings from warehouse equipment.

Sub-steps 1 and 2 cover data characterisation and cleaning. Sub-steps 3 and 4 cover
ARIMA and SARIMA modeling on the sales series. Sub-step 5 builds a Gradient Boosting
failure-risk classifier for the sensor data. Sub-steps 6 and 7 are the optional hard
extensions covering rule-based vs ML comparison and fleet-scale cost optimisation.

## How to Run

1. Place `ecommerce_sales_ts.csv` and `sensor_data.csv` in this directory
   (same folder as `ts_analysis.ipynb`). Both files are provided on the LMS.

2. Install the required packages (see below).

3. Launch Jupyter and open `ts_analysis.ipynb`:

```
jupyter notebook ts_analysis.ipynb
```

4. Run all cells in order from top to bottom. Each sub-step is clearly marked with
   a heading and prints its own findings. The notebook is self-contained.

## Python Version

Python 3.10 or later is required.

## Required Packages

Install all dependencies with:

```
pip install numpy pandas matplotlib seaborn statsmodels scikit-learn scipy
```

| Package       | Minimum version | Purpose                                      |
|---------------|-----------------|----------------------------------------------|
| numpy         | 1.23            | Numerical operations                         |
| pandas        | 1.5             | DataFrame and time-series handling           |
| matplotlib    | 3.6             | Plotting                                     |
| seaborn       | 0.12            | Statistical plots                            |
| statsmodels   | 0.14            | ADF test, decomposition, ARIMA, SARIMA       |
| scikit-learn  | 1.2             | Gradient Boosting classifier, metrics        |
| scipy         | 1.10            | Point-biserial correlation (Sub-step 6)      |

## Repository Structure

```
week-08/
  monday/
    ts_analysis.ipynb   Main notebook (all 7 sub-steps)
    README.md           This file
    prompts.md          AI usage log (prompts and critiques)
```

## Datasets

`ecommerce_sales_ts.csv` — two years of daily Brazilian e-commerce order data.
Reference: kaggle.com/datasets/olistbr/brazilian-ecommerce

`sensor_data.csv` — one year of industrial pump sensor readings sampled at 1-minute
intervals with machine status labels.
Reference: kaggle.com/datasets/nphantawee/pump-sensor-data

Neither dataset is committed to the repository. Place them in this directory before
running the notebook.

## Key Design Decisions

The train/test split on both datasets is strictly temporal. No random splitting is
used anywhere. For the sensor classifier, the last 20 percent of the time-ordered
data forms the test set. For the e-commerce models, the last 30 days form the hold-out
set. This is the only methodologically valid approach for time-series evaluation.

The evaluation metric for the sales models is MAPE, chosen because it is
scale-independent and directly interpretable for inventory planning. The evaluation
metric for the failure classifier is Recall, chosen because the cost of a missed
failure is 10x the cost of a false alarm.

