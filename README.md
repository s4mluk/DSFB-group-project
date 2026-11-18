# Walmart Sales Analysis and Forecasting

University group project (2024): exploratory analysis and sales prediction on Walmart weekly store sales, with external factors such as holidays, temperature, fuel price, CPI and unemployment.

## Data
`Walmart_Sales.csv`: 6,435 rows, no missing values.

- **45 stores**, weekly sales from 2010-02-05 to 2012-10-26 (143 weeks)
- Columns: `Store`, `Date`, `Weekly_Sales`, `Holiday_Flag`, `Temperature`, `Fuel_Price`, `CPI`, `Unemployment`
- Mean weekly sales per store: about 1.05 M, standard deviation about 0.56 M

## Methods (all in `Walmart Sales DA/WorkspaceNotebook.ipynb`)
- **Exploration:** sales trend and distribution, holiday vs non-holiday, total sales by store, correlation matrix, scatter plots against temperature, fuel price and unemployment
- **Hypothesis test:** t-test of holiday vs non-holiday weeks
- **Feature engineering:** year/month/week, lagged sales (1-4 weeks), rolling mean and std
- **Models:** linear regression, random forest (tuned with grid search, 3-fold CV), mean-prediction baseline, SARIMA on total weekly sales (after an ADF stationarity test)
- Metrics: RMSE, MAE, R², 80/20 train-test split

## Key results
- Holiday weeks have significantly different sales than other weeks (t = 2.96, p = 0.003).
- Stores 20, 4 and 14 have the highest total sales; stores 33, 5 and 36 are among the lowest.
- Using only external factors (temperature, fuel price, CPI, unemployment, holiday flag), linear regression explains almost nothing (R² = 0.017). A tuned random forest does better (R² = 0.29, RMSE about 477k, MAE about 371k) but remains modest.
- The SARIMA model (2,1,2)x(1,1,1,52) fits poorly on this short series (R² = -52 on its 12-week comparison), so it is not a usable forecaster as configured.
- Takeaway: store identity and past sales matter far more than weather or macro variables. A better model would use store-level lags and a proper time-based split instead of a random one.

## Repository
```
Walmart_Sales.csv                      # dataset (a second copy is in "Walmart Sales DA/")
Walmart Sales DA/WorkspaceNotebook.ipynb   # full analysis
```

## Run
```bash
pip install pandas numpy matplotlib seaborn scipy scikit-learn statsmodels jupyter
jupyter notebook "Walmart Sales DA/WorkspaceNotebook.ipynb"
```
The notebook reads `Walmart_Sales.csv` from its working directory; copy or point `file_path` to the CSV.

## Team
<!-- TODO: list group members and course name. -->
