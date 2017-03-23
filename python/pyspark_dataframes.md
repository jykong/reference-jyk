
### PySpark DataFrames
Pandas-like DataFrame features for PySpark. DataFrames are built on RDDs with metadata. Starting from Spark 2.0, DataFrames will be the primary abstraction.

#### Importing Data
    from pyspark.sql import SQLContext
    sqlCtx = SQLContext(sc)

From Pandas:

    spark_df = sqlCtx.createDataFrame(pandas_df)

From a Python data structure:

    spark_df = sqlCtx.createDataFrame(list_of_tuples, ['col1_name', 'col2_name'])

From a JSON file:

    spark_df = sqlCtx.read.json("some_file.json")

From a text file:

    spark_df = sqlCtx.read.text("some_text_file.txt")

#### Preview / Inspect DataFrame
    df.printSchema()
    df.show(n_rows)
    df.describe().show()
    df.rdd.getNumPartitions()

#### DataFrame Transformations
##### Column Selection
Column selection is lazy evaluated. Double-bracket `[[]]` and `select()` are equivalent. Although, `select()` appears to be preferred.

    df[['col1']]
    df[['col1', 'col2', 'col3']]

`select()` allows for column name selection using both single-quote `''` or dot `.` notation. `select()` returns a DataFrame, wheresas `df['col1']` or `df.col1` notation returns a Column object.

    df.select('col1', 'col2', 'col3')
    df.select(df.col1, df.col2, df.col3)

    df.select('*')    # '*' selects all columns

##### Column Modification
`select` allows for column modification. Use `alias` to rename columns.

    new_df = df.select(df.col1, (df.col2 + 10).alias('new_col2'))

`drop` drops columns

    new_df = df.drop(df.col1, df.col2)

##### Column Renaming
`selectExpr()` allows for column alias renaming

    new_df = df.selectExpr("col1 as first_col", "col2 as second_col")

##### Casting
    from pyspark.sql.types import DoubleType
    new_df = df.select(df.col1.cast(DoubleType()))

##### Filters & Boolean Masking
Works much like Pandas DataFrames

    filtered_rows = df[boolean_mask]
    filtered_rows = df[df['col1'] == some_value]
    filtered_rows = df.filter(df.col1 == some_value)

##### Dataframe (Table) Join
    df1.join(df2, 'col1')   # defaults to inner join
    df1.join(df2, 'col1', 'outer')
    df1.join(df2, df1.col1 == df2.col2, 'inner')

[join reference](https://spark.apache.org/docs/latest/api/python/pyspark.sql.html#pyspark.sql.DataFrame.join)

##### Sort
    sorted_df = df.sort(df.col1,)
    sorted_df = df.sort(df.col1, ascending=False)

##### Order By
    ordered_df = df.orderBy(df['col1'])
    ordered_df = df.orderBy(df.col1.desc())

##### Group By
    grouped_df = df.groupBy('col1')

No argument `groupBy()` can be used to aggregate across all rows. See `agg` for equivalent functionality with different syntax.

    grouped_df = df.groupBy()

##### Aggregation Functions
    grouped_df.count()

`avg()`, `min()`, `max()`, `sum()` can be empty or have column name arguments

    grouped_df.avg()
    grouped_df.avg('col1', 'col2')

##### SQL DataFrame Functions
    from pyspark.sql import functions as F
    F.max(df.col1)

See [sql function docs](https://spark.apache.org/docs/latest/api/python/pyspark.sql.html#module-pyspark.sql.functions) for a full list

##### Aggregate Selection
    from pyspark.sql import functions as F
    df.agg(F.avg(df.col1), F.min(df.col2))

`agg()` applies aggregation across all rows. Usage is similar to `select()`, except for aggregation.

##### Distinct / Drop Duplicates
    new_df = some_df.distinct()

`distinct()` filters out duplicate rows

    new_df = some_df.dropDuplicates(['col1', 'col2'])

`dropDuplicates()` filters out duplicate rows based on the specified columns

##### Null Values
    null_vals_df = some_df.filter(some_df.col1.isNull())

`isNull()` returns null rows

    filled_df = some_df.na.fill(some_val)

`na` selects null rows and `fill()` replaces them

##### Sample
Filters random rows from the DataFrame

    df.sample(withReplacement=False, fraction=0.1)

##### User Defined Functions
`udf` accepts a function variable or lambda function and a PySpark type class. User defined functions are slow, so use built-ins whenever possible.

    from pyspark.sql.types import IntegerType

    len_func = sqlCtx.udf(lambda row: len(row), IntegerType())
    df.select(len_func(df.col1).alias('col1_lengths'))

#### DataFrame Actions
##### Show
Similar to `head()` in Pandas. Returns top n elements. Print-friendly.

    df.show(n_elements)
    df.show(n_elements, truncate=False)

Databricks notebook has `display(df)`, which is even prettier & scrollable

##### Describe
Similar to `describe` in Pandas. Computes summary statistics on each column. Print-friendly.

    df.describe()

##### Output to Pandas
    pandas_df = df.toPandas()

#### SQL Statements
SQL-like features for PySpark.

    from pyspark.sql import SQLContext
    sqlCtx = SQLContext(sc)
    df = sqlCtx.read.json("some_file.json")

`regsiterTempTable()` sets a Spark DataFrame as a SQL table

    df.registerTempTable("sql_table_name")

`tableNames()` queries SQL tables

    print(sqlCtx.tableNames())

Use `sql()` on the `SQLContext` object to make SQL queries. Do not include terminating semi-colons, as they will throw errors. SQL queries are lazy evaluated.

    new_df = sqlCtx.sql("SELECT col1 FROM sql_table_name")

##### Inspect Catalyst Optimizer
Produces an output explaining how the catalyst optimizer would execute the current query plan.

    # apply some transformations to df
    df.explain(True)
