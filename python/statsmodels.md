## Statsmodels Reference
statsmodels depends on scipy.stats and plays nice with pandas, but adds additional features similar to R

    import statsmodels.api as sm

### Linear Regression
#### Ordinary Least Squares (OLS)

    linear = sm.OLS(X,y)
    linearfit = linear.fit()
    linearfit.summary()
    linearfit.params
