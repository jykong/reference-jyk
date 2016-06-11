### SciPy Basics Reference

#### Linspace
    from scipy import linspace

    x = linspace(x_min, x_max, n_intervals)   # outputs an a linear array
    # step size computed by (x_max - x_min) / n_intervals

#### Stats
    from scipy.stats import <function>

##### Summary Statistics
    skew(data)
    kurtosis(data)

##### Distributions
Normal

    y_probabilities = norm.pdf(x_array, mean, std_dev)
T

    y_probabilities = t.pdf(x_array, degf)
    y_cumulative_prob = t.cdf(x_arrya, degf)
Binomial

    y_probabilities = binom.pmf(x_array, N, p)
    y_cumulative_prob = binom.cdf(x_array, N, p)

##### Correlation / R-value / Pearson's R
    r_value, p_value = pearsonr(var1, var2)

##### Linear Regression
    slope, intercept, r_value, p_value, stderr = linregress(x, y)

##### Chisquare / Significant Difference from Expected Value
    chisquared_value, p_value = chisquare(observed_list, expected_list)

    chisq_v, p_value, degf, expected_v = chi2_contingency(observed_table)
    # takes in a table / matrix and computes expected values automatically
    # use with crosstab() from pandas

#### Probability
    from scipy.misc import <function>

    factorial(n)
    comb(N, k)    # combinations, N choose k

#### Distance Measures
    from scipy.spatial import distance

Euclidean / Root Sum Squared (RSS)

    rss = distance.euclidean(vector1, vector2)
