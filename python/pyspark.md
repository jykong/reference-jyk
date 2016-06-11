### Spark Python API Reference

    from pyspark import SparkContext
    sc = SparkContext("local", "App Name")

#### Resilient Distributed Database (RDD)
Data is stored as immutable RDDs. They are immutable (cannot be overwritten) for performance reasons. Bits and parts of RDDs can be anywhere in the data cluster.

#### Lazy Evaluation
A lot of commands in Spark are done via lazy evaluation. Instead of executing the command immediately, the command is set up and promised for when it is needed. An analogy would be setting up an on-demand assembly line that is only triggered to operate when a product is needed at the end, as opposed to operating every step every time regardless to whether or not the next step needs it.

#### Basics
    raw_data = sc.textFile("some_text_file")

`raw_data` is now an RDD. `textFile()` is lazy evaluated.

    raw_data.take(5)      # returns & prints the first 5 elements

`take` is an action. This causes `textFile()` to evaluate, at least for the first 5 elements.

#### Transformations
Transformations are lazy evaluated

##### Map
Operates much like Python map

    new_rdd = some_rdd.map(some_func)

Map return values have a 1-to-1 mapping with the input data.

Use `.flatMap()` to combine output into one single flat list, instead of nested lists. Flat map is okay with functions that do not return values for every input data.

    new_rdd = some_rdd.flatMap(some_func)


##### Filter
Operates much like Python filter

    new_rdd = some_rdd.filter(some_boolean_func)

##### Reduce By Key
Does an grouped reduction / aggregation on an array of 2-element tuples. First item in the tuples is the key, the second item is reduced / aggregated by the specified function.

    reduced_rdd = some_rdd_of_tuples.reduceByKey(lambda x,y: some_func(x,y))

#### Actions
##### Take
Similar to `head()` in Pandas. Returns top n elements.

    some_rdd.take(n_elements)

##### Count
Similar to `len()`

    some_rdd.count()


    reduce()
    saveAsTextFile()
    collect()

#### PySpark DataFrames
Pandas-like features for PySpark

    from pyspark.sql import SQLContext
    sqlCtx = SQLContext(sc)
    df = sqlCtx.read.json("some_file.json")
    df.printSchema()
    df.show(n_rows)
    df.describe().show()

##### Column Selection
Column selection is lazy evaluated. Double-bracket `[[]]` and `select()` are equivalent.

    df[['col1']]
    df[['col1', 'col2', 'col3']]
    df.select('col1', 'col2', 'col3')

##### Boolean Masking
Works much like Pandas DataFrames

    filtered_rows = df[boolean_mask]
    filtered_rows = df[df['col1'] == some_value]

##### Output to Pandas
    pandas_df = df.toPandas()

#### PySpark SQL
SQL-like features for PySpark.

    from pyspark.sql import SQLContext
    sqlCtx = SQLContext(sc)
    df = sqlCtx.read.json("some_file.json")
    df.registerTempTable("sql_table_name")
    print(sqlCtx.tableNames())

Use `sql()` on the `SQLContext` object to make SQL queries. Do not include terminating semi-colons, as they will throw errors. SQL queries are lazy evaluated.

    new_df = sqlCtx.sql("SELECT col1 FROM sql_table_name")
