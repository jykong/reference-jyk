## Basic Pandas Reference
Pandas is built on top of Numpy. Uses DataFrames and Series instead of Arrays for easier manipulation of data.

#### Importing Pandas
    import pandas
Frequently imported as `pd`

    import pandas as pd

#### Reading In CSV, Outputting CSV
Reads in CSV as a DataFrame, automatically treating 1st row as header

    dataframe = pandas.read_csv("file.csv")

In case of encoding error, trying a different encoding

    dataframe = pandas.read_csv("file.csv", encoding="iso-8859-1")

[Standard Encodings](https://docs.python.org/3/library/codecs.html#standard-encodings)

Output a DataFrame to CSV file

    dataframe.to_csv("file.csv", index=False)

#### Inspecting Dataframes
    dataframe.head()      # outputs the first 5 rows
    dataframe.shape       # outputs the dimensions as a tuple
    dataframe.dtypes      # outputs the column names + data types
    dataframe.describe()  # outputs basic summary statistics for numeric value columns

    dataframe.columns     # outputs the column headers as an index
    dataframe.index       # outputs the row index

#### Empty Values: NaN
Empty / null values in a DataFrame or Series are represented with NaN (Not a Number)

### Series
#### Series data object
Instead of returning 1-D arrays as vectors like NumPy, Pandas returns a Series object.

    series_object = dataframe["col_name"]
    series_object = dataframe.loc[0]

When outputting a column from a DataFrame, the row index becomes the Series index.

When outputting a row from a DataFrame, the column header becomes the Series index.

Each Series object has an index AND a integer position. The index can handle a variety of datatypes. Each entry in the index is mapped to a corresponding value, similar to a dictionary.

    mapped_value = series_object["some_index_element"]

Series objects can also be addressed by position.

    value = series_object[0]
    sublist = series_object[2:5]

Creating a Series object via Series constructor

    from pandas import Series
    series_object = Series(index=array-like1, data=array-like2)
    # len(array-like1) must be equal to len(array-like2)

#### Inspecting a Series
    series_object.head()      # outputs the first 5 rows
    series_object.dtypes      # outputs series name + data type
    series_object.describe()  # outputs basic summary statistics
    series_object.value_counts()    # outputs frequency table over each value

#### Manipulating Series
Outputting the index / values

    index = series_object.index   # same as .keys()
    values = series_object.values
    unique_values = series_object.unique()  # includes NA

Converting Series object to dictionary, index -> keys

    dict = series_object.to_dict()

Reindexing

    reindexed_series = series_object.reindex(new_index)

Sorting

    index_sorted = series_object.sort_index()
    values_sorted = series_object.sort_values()

Arithmetic operations on Series values are treated like NumPy arrays

    scaled_seies_vector = series_object/100
    pairwise_sum_series = series1 + series2

Comparison operations on Series values output Boolean Series like NumPy

    bool_series = (series_object == "magic string")

Boolean Series can be used to select / deselect items in a Series (masking)

    subsetted_series = series_object[bool_series]
    subsetted_series = series_object[series_object < 100]

#### Checking for NaN values
    boolean_series = pandas.isnull(some_series_object)    # Series values True if null

    n = pandas.count(some_series_object)    # Counts the number of Nan & None values

#### Basic Statistics
Automatically omit NaN values

    series_object.mean()
    series_object.median()
    series_object.var()
    series_object.std()
    series_object.skew()
    series_object.kurtosis()

    series_object.min()
    series_object.max()
    series_object.idxmin()    # returns indices of min values
    series_object.idxmax()    # returns indices of max values

### DataFrames
Like Series objects, dataframe rows can be accessed either by position or index

#### Selecting Dataframe Rows by Position / Index
dataframe.iloc[] - get [row,col] by position, sorting / dropping rows may change position of rows relative to their index

    dataframe.iloc[0]        # outputs the first row as a Series
    dataframe.iloc[0:3]      # slice 0-2 rows of dataframe
    dataframe.iloc[[0,1,2]]  # same as above, except enumerating rows with a list

    dataframe.iloc[0,0]      # outputs the first row element of the first column
    dataframe.iloc[:,0]      # outputs the first column

dataframe.loc[] - get [row,col] by index

    dataframe.loc["row_index", "col_index"]
    dataframe.loc[:, 'col11':'col99']    # slice columns by name

[Indexing](http://pandas.pydata.org/pandas-docs/stable/indexing.html)

[Selection](http://pandas.pydata.org/pandas-docs/stable/cookbook.html#cookbook-selection)

#### Alternative Selecting Dataframe Columns by Index
    dataframe["col_name"]         # outputs the column matching "col_name"
    dataframe[["col1", "col2"]]   # outputs multiple columns

#### Selecting Dataframe Rows by Boolean Series
    filtered_dataframe = dataframe[bool_data_series]

Comparison operations on a series object will return a boolean series

    filtered_dataframe = dataframe[dataframe['col1'] == some_value]

Use `.isin` to match against multiple values

    target_values = ['val1', 'val2']
    filtered_dateframe = dataframe[dataframe['col1'].isin(target_values)]

#### Adding / Replacing Entire Dataframe Columns
    dataframe["new_col_name"] = some_series_object
    dataframe["existing_col_name"] = some_series_object

#### Concatenate, Merge, Join Rows / Columns
    new_df = pandas.concat([dataframe, other_df_rows])
    new_df = pandas.concat([dataframe, other_df_cols], axis=1)

[Merges & Joins](http://pandas.pydata.org/pandas-docs/stable/merging.html)

#### *WARNING* - about chained indexing
    new_df = dataframe[dataframe['col1']] == some_value]
    new_df.loc[:] = something              # will throw a warning

First, `dataframe[dataframe['col1']]` initiates a `__getitem__` call that may return a copy or slice an index view of the original dataframe. Then, `new_df.loc[:] =` initiates a `__setitem__` call that will try write on what may be a copy, which would not update the original dataframe.

[Indexing View vs Copy](http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy)

See section on [Setting With Copy](http://tomaugspurger.github.io/modern-1.html)

Using a constructor call to create a new object often fixes the chained indexing problem

    new_df = pandas.DataFrame(dataframe)
    new_series = pandas.Series(dataframe['col1'])

#### Modifying Values
Iterates over each element in the series/dataframe

    replace_dict = {
      'old_value1': new_value1,
      'old_value2': 'new_value2'
    }
    new_dataframe = dataframe['col1'].map(replace_dict)

#### Renaming Columns
    dataframe.columns = new_column_names

Using replace_dict similar to `.map`

    replace_dict = {
      'old_col1': 'new_col1',
      'old_col2': 'new_col2'
    }
    new_dataframe = dataframe.rename(index=str, columns=replace_dict)

#### Dropping Rows / Columns
    new_df = dataframe.drop('row_index')                            # drop row by index
    dataframe.drop('col_name', axis=1, inplace=True)                # drop col by name
    new_df = dataframe[dataframe['col_name'] != 'unwanted_value']   # drop row by value

#### Apply
    series_result = series_object.apply(single_arg_func)      # calls on each element
    series_result = dataframe.apply(single_arg_func)          # calls on each column
    series_result = dataframe.apply(single_arg_func, axis=1)  # calls on each row

    def single_arg_func(some_series):           # example single argument function
      # do stuff with series
      return series_object

    df_result = dataframe.apply(lambda x: x*2)            # doubles each element
    series_result = dataframe.apply(lambda x: np.sum(x))  # sums across rows

#### Sorting Dataframes
Sort defaults to outputig a new dataframe. Use inplace to modify existing dataframe.

    dataframe.sort_values("col_to_sort_by", inplace=True, ascending=False)

#### Data Types
    dataframe.dtypes

* object (String)
* int
* float
* datetime
* bool

Cast series as a data type

    new_series = series_object.astype(<data_type>)

#### Handling NaN values
Filter rows *not containing* NaN values

    filtered_notnull_rows = dataframe[pandas.notnull(dataframe['col1'])]

Extract rows *containing* NaN values

    extracted_null_rows = dataframe[pandas.isnull(dataframe['col1'])]

Drop rows containing NaN values

    new_dataframe = dataframe.dropna()        # Drop all rows with NaN values
    new_dataframe = dataframe.dropna(axis=1)  # Drop all columns with NaN values
    new_dataframe = dataframe.dropna(subset=["col1", "col2"])   # Drop all rows with NaN in col1 and col2

Fill rows containing NaN values with another value

    new_dataframe = dataframe.fillna(new_value)

#### Reset Index

dataframe.reset_index()

    reindexed_df = dataframe.reset_index(drop=True)        # Resets index based on current positions
    dataframe.reset_index(drop=True, inplace=True)         # Inplace version

#### Custom Index
Drop current index and use a specified column as the index instead.

    reindexed_df = dataframe.set_index("col_name", inplace=False, drop=True)
