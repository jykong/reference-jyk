## SQL Basics Reference

#### Syntax
* Newlines are ignored
* End all sql commands with a semicolon ;
* **NOTE**: keywords do not need to be capitalized, they are by convention

#### Show Column Header Names, Data Types & Primary Key
    PRAGMA table_info(some_table);

### Read
#### SELECT, FROM
Returns row data from the specified columns from the specified table

    SELECT col1, col2
    FROM some_table;

The column order of the data is returned in the order of the columns listed

Use the wildcard * to select all columns

    SELECT *
    FROM some_table;

#### WHERE
Filters rows based on specified column & condition

    SELECT col1, col2
    FROM some_table
    WHERE col1 > 0.5;

Valid comparison operators

    <  <=
    >  >=
    =  !=

Conditions can be combined using logical operators AND and OR with parentheses

    SELECT col1
    FROM some_table
    WHERE col2 = 'some_string' AND (col3 != 42 OR col4 < 0.1);

#### LIMIT
Caps the output data to the specified number of rows

    SELECT col1, col2
    FROM some_table
    LIMIT 10;

#### ORDER BY
Sorts the output data rows by the specified column

    SELECT col1
    FROM some_table
    ORDER BY col1 DESC;

Columns can be ordered ascending or descending: `ASC` or `DESC`

Multiple columns can be used to sort

    SELECT col1, col2
    FROM some_table
    ORDER BY col1 DESC, col2 ASC;

#### Aggregation Functions
##### COUNT
Returns the length of non-null rows of the specified column, * for the whole table

    SELECT COUNT(col1)
    FROM some_table;

##### MIN, MAX, SUM, AVG
Returns the min/max/sum/average of numeric columns

    SELECT MIN(col1), MAX(col1), SUM(col1), AVG(col1) FROM some_table;

#### AS
AS renames the column or aggregation function in the output column header

    SELECT AVG(col1) AS col1_mean, SUM(col2) AS col2_sum
    FROM some_table;

#### DISTINCT
Returns only unique rows

    SELECT DISTINCT col1
    FROM some_table;

Can be used on aggregation functions

    SELECT COUNT(DISTINCT col1)
    FROM some_table;

#### Arithmetic
##### Constants
Use a decimal point to force float output

    SELECT col1 / 1000.0
    FROM some_table;

##### Columns
Arithmetic operations can be performed across numerical columns

    SELECT (col1 / col2) + col3
    FROM some_table;

##### Rounding
Rounds floats to the specified number of decimal spaces

    SELECT ROUND(col1 / col2, 2)
    FROM some_table;

#### GROUP BY
GROUP BY groups aggregation by categories, much like pivot tables

    SELECT col2, sum(col1)
    FROM some_table
    GROUP BY col2;

Instead of summing along the entire column, summations are done across all `col1` values with the same `col2` label. The output has rows equal to the number of unique `col2` labels.

#### HAVING
Performs conditional filtering similar to WHERE, except does so on virtual columns created using GROUP BY and named using AS

    SELECT col2, sum(col1) AS col1_sum
    FROM some_table
    GROUP BY col2
    HAVING col1_sum > 100;

### Data Types
#### Common Types
* `integer`
* `float`
* `real` -- similar to float
* `text` -- similar to string
* `varchar(255)` -- similar to string

#### Null
Use keyword `NULL` for missing / null data

Use `IS NULL` and `IS NOT NULL` to compare with `NULL` values

    SELECT col1
    FROM some_table
    WHERE col1 IS NOT NULL;

#### Datetime
Strings are used for datetime. Written in standard format, they can be compared numerically

    SELECT datetime_col1
    FROM some_table
    WHERE datatime_col1 > "2016-05-19 13:00";

### Write
#### INSERT INTO, VALUES
Add row data into existing table

    INSERT INTO some_table
    VALUES (123, "abc");

#### INSERT INTO, SELECT
Copy data from one table to another

    INSERT INTO some_table
    SELECT * FROM some_other_table;

Copy between tables specifying columns. No need to specify `some_table.id` if set to primary key.

    INSERT INTO some_table(col1, col2)
    SELECT col8, col9 FROM some_other_table;

#### UPDATE, SET
Modify cells of data

    UPDATE some_table
    SET col1="new value"
    WHERE col1="old value"

If WHERE is not specified, overwrites all `col1` values

#### DELETE FROM
Delete / drop rows of data

    DELETE FROM some_table
    WHERE col1="some value";

If WHERE is not specified, deletes all rows

### Modify
#### ALTER TABLE, ADD
    ALTER TABLE some_table
    ADD new_col <col_data_type>;
#### ALTER TABLE, DROP COLUMN
    ALTER TABLE some_table
    DROP COLUMN col1;

#### CREATE TABLE
    CREATE TABLE some_table(
      id integer PRIMARY KEY,
      col1 text,
      col2 float
    );

Using first column `id` as an integer primary key is conventional

#### DROP TABLE
    DROP TABLE some_table;
