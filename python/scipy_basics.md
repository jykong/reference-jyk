### SciPy Basics Reference

#### Stats
    from scipy.stats import <statistic>

##### Summary Statistics
    skew(data)
    kurtosis(data)

##### Distributions
    y_probabilities = norm.pdf(x_array, mean, std_dev)

##### Correlation / R-value / Pearson's R
    r_value, p_value = pearsonr(var1, var2)
