### SQLite Reference

#### Open database
    sqlite3 filename.db

#### SQLite Command Line
Show tables
    .tables

Help
    .help

Turn Headers On
    .header on

Exit CLI
    .quit

[CLI Reference](https://www.sqlite.org/cli.html)

#### Query Plans
SQLite allows the user to examine the query plan for how it plans to go about performing the query.

    EXPLAIN QUERY PLANS <insert full query here>

This information is useful for understanding performance.

##### Understanding Query Plan Output
    SCAN TABLE some_table

`SCAN TABLE` refers to an O(n) row by row search performed on `some_table`.

    SEARCH TABLE facts USING INTEGER PRIMARY KEY (rowid=?)

`SEARCH TABLE` refers to a Olog(n) binary search. `USING INTEGER PRIMARY KEY` refers to the column `rowid` that the binary search was performed on.

    SEARCH TABLE some_table USING INDEX some_idx(col1=?)

`USING INDEX` refers to the index that the binary search was performed on.

In this case, SQLite two binary searches. First, it did a binary search on the `col1` column of `some_idx` to get the list of `id`s that match `col1=?`. Then it does a binary search on the `id` column of `some_table` to get the row(s) of data from the matching `id`s.

    SEARCH TABLE some_table USING COVERING INDEX some_multi_column_idx (col1=?)

`USING COVER INDEX` refers to the column of data being searched for in `some_table` also exists in `some_multi_column_idx`. As a result, only one search is performed on `some_multi_column_idx` and no search is actually performed on `some_table`.

    col=?
    col<?
    col>?

The `=?`, `<?`, and `>?` refer to the type of comparison used by SQLite. These should correspond with the comparisons used in the `WHERE` or `HAVING` statements of the query.

#### Creating an Index
Indexes are sorted column value -> primary key mappings that allow for O(log N) binary search lookups on specific columns. This is as opposed to O(N) lookups for unsorted full table scans.

    CREATE INDEX index_name ON some_table(col1);
    CREATE INDEX IF NOT EXISTS index_name ON some_table(col1);
