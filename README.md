# Quarter-Hourly Electricity Price Forecasting

Bachelor's thesis in Computer Science at Technische Hochschule Ulm, comparing statistical, machine learning, and deep learning models for the German day-ahead electricity market after the October 2025 market reform.

## Overview

This project forecasts the next day's 96 quarter-hourly electricity prices using historical prices and day-ahead forecasts of electricity demand, wind generation, and solar generation.

The study compares:
- LEAR — Lasso Estimated Autoregressive model
- XGBoost
- LSTM — Long Short-Term Memory neural network
- A weekly naive baseline

## Data

Source: Bundesnetzagentur's SMARD platform, covering the German-Luxembourg bidding zone. Day-ahead spot prices are based on EPEX SPOT prices.

- Historical hourly prices: January 2020–September 2025
- Quarter-hourly prices: October 2025–February 2026
- Final feature matrix: 13,824 observations across 144 days
- Seven input features per quarter-hourly observation

## My Work

- Cleaned and aligned datasets with different timestamp formats
- Handled duplicate timestamps associated with daylight saving time
- Engineered daily, weekly, and cross-granularity price features
- Incorporated day-ahead load, wind, and solar forecasts
- Implemented and compared LEAR, XGBoost, and LSTM models
- Evaluated training-window schemes and parameter sensitivity
- Conducted feature ablation and intraday error analysis

## Evaluation

Models were evaluated chronologically over 44 days:
16 January–28 February 2026, covering 4,224 quarter-hourly predictions.

LEAR and XGBoost were evaluated using both four-window forecast averaging and an expanding-window approach. LSTM used expanding-window retraining.

## Main Results

Results for the selected seven-feature model configurations:

| Model | MAE (EUR/MWh) | RMSE (EUR/MWh) |
|---|---:|---:|
| Weekly naive baseline | 21.19 | 30.25 |
| LEAR | 12.06 | 16.08 |
| XGBoost | 11.55 | 16.27 |
| LSTM | 20.64 | 28.51 |

- XGBoost achieved the lowest MAE in the main comparison.
- LEAR achieved the lowest RMSE in the main comparison.
- Removing the two cross-granularity features slightly reduced MAE for all three models; XGBoost achieved an MAE of 11.33 EUR/MWh in this ablation.
- The tested LSTM architecture was less competitive with the limited training sample.
- Forecast accuracy varied by time of day, with lower errors at night.

## Limitations

The evaluation covers only 44 winter days. Model configurations were compared and selected using the same evaluation period, without a separate validation set. No formal statistical significance tests were performed.

These results are exploratory and do not establish general model superiority.

## Repository Structure

- `notebooks/`: Data cleaning, feature engineering, modeling, and analysis
- `data/`: Prepared datasets and saved model outputs
- `results/`: Visualizations and comparison plots

## Technologies

Python · Pandas · Jupyter Notebook · XGBoost · LSTM

## Author

Ebtehal Aldheeshy
Bachelor's Thesis, Computer Science
Technische Hochschule Ulm — June 2026
