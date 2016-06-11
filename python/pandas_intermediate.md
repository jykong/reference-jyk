## Intermediate Pandas Reference
    import pandas as pd

#### Transpose
Swaps rows & columns

    new_dataframe = dataframe.T

#### String Methods
Array-like indexing. **Can be used on non-string data structures.**

    series_object.str[0]
    series_object.str[4:8]

Python-like string manipulation & regex

    series_object.str.<string_method>()

See [docs](http://pandas.pydata.org/pandas-docs/stable/text.html#method-summary) for a full list

#### Split-Apply-Combine: Group By, Aggregate
`groupby()` split sorts the dataframe by grouping the same values of the specified column

    grouped_df = dataframe.groupby('col1')

Grouped dataframes can be iterated over. Each iteration returns a subset of the original dataframe keyed on on the `groupby()` column

    for group_df in grouped_df:
      # do stuff with group_df dataframe

`aggregate()` combines / reduces rows of each non-keyed column into a single value based on a specified function, keyed on the `groupby()` column

    sums = grouped_df.aggregate(sum)
    counts = grouped_df.aggregate(len)

#### Split Value Categories Into Binary Columns
Binary columns named using `prefix` + `str(value)`. i.e. values via `value_counts()`

    binary_cols_df = pd.get_dummies(dataframe['col1'], prefix='binary_cols_prefix')

#### Correlations
Compute pairwise correlations / r-values

    correlations_dataframe = dataframe.corr()

#### Pivot Tables
Segments aggregation across specified index labels

    pivot_table = dataframe.pivot_table(index="col_name_to_segment_by", values="col_name_to_aggregate", aggfunc=some_func)

    multi_col_pivot_table = dataframe.pivot_table(index="col_name_to_segment_by", values=["col1","col2"], aggfunc=some_func)

#### Crosstab
Groups results into NxN matrix segments. Defaults to frequency counting unless an `aggfunc` is supplied.

    table = pd.crosstab(dataframe['col_as_index'], [dataframe['col1'], dataframe['col2']])

#### Fast operations over row elements
Fastest to slowest:
* `zip`
* `itertuples`
* `iterrows`
* `apply`???
* `str` ???

See this [discussion](http://stackoverflow.com/questions/7837722/what-is-the-most-efficient-way-to-loop-through-dataframes-with-pandas)

TODO: perform experiment on my own

### Plotting
Generic catch-all method

    dataframe.plot(kind='<insert_type')

[Plot types](http://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.plot.html)
#### Histograms
    dataframe['col_name'].hist()
    dataframe['col_name'].hist(columns='col_name', bins=10)
[Histogram docs](http://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.hist.html#pandas.DataFrame.hist)
#### Box Plots
    dataframe.boxplot(by='col_name')

#### Scatter Matrix
Scatter Matrix generates a histogram for each column variable and scatter plots pairwise

    from pandas.tools.plotting import scatter_matrix

    scatter_matrix(dataframe, figsize=[6,6])

Be sure to choose just the variables of interest in the dataframe, as a large number of columns may cause the scatter matrix to take a while
