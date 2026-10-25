# Stock Return Prediction

Predict next-session returns from daily price and volume history.

- Five-stock study with eleven features and chronological train/validation/test splits.
- Compare zero return, AR, pooled regression, random forest and XGBoost.
- Examine GARCH variance forecasts and a cross-stock feature on matched rows.

AR(5) lowers validation RMSE by about 0.6% versus zero; zero has the lowest MAE. Results are provisional, and the final test period remains reserved.

## Run

Use Python 3.12. From this project folder:

```sh
python3.12 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
jupyter lab stock.ipynb
```

Run all cells from top to bottom. The notebook includes saved tables and figures for reading on GitHub.

To execute without opening Jupyter:

```sh
jupyter nbconvert --execute --to notebook --inplace --ExecutePreprocessor.timeout=600 stock.ipynb
```

## Files

- `stock.ipynb`: analysis, methods, results and limitations.
- `daily_market_data.csv`: daily OHLC prices and share volume, 2013–2018.
- `requirements.txt`: pinned analysis packages and Jupyter tools. Pip installs their dependencies.

Data columns: `date`, `open`, `high`, `low`, `close`, `volume`, `Name`. Prices are USD per share. Data source: [S&P 500 stock data](https://www.kaggle.com/datasets/camnugent/sandp500); notebook references are listed in its Sources section.

Pooled models use `ColumnTransformer` and `Pipeline` to learn stock indicators from training rows only. Numeric features stay unscaled.

Missing sessions stay missing before returns and lags are calculated. asset_337/asset_137 price adjustments need further review. Five selected stocks and one validation period do not establish a trading edge.

Asset IDs are pseudonyms. Price, volume, calendar dates and row order are preserved.
