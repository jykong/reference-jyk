## Intermediate Pandas Reference

#### Pivot Tables
    pivot_table = dataframe.pivot_table(index="col_name_to_segment_by", values="col_name_to_aggregate", aggfunc=some_func)

    multi_col_pivot_table = dataframe.pivot_table(index="col_name_to_segment_by", values=["col1","col2"], aggfunc=some_func)

#### Crosstab
    table = pandas.crosstab(dataframe['col_as_index'], [dataframe['col1'], dataframe['col2']])

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
