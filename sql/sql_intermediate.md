## Intermediate SQL Reference
Relations & Table Joins used in database normalization.

### Relations
#### FOREIGN KEY, REFERENCES
Use foreign key to specify a direct mapping of one column to another column of a different table

    CREATE TABLE database_name.some_table(
      id integer PRIMARY KEY,
      col1 text,
      col2 float
      col3 integer,
      FOREIGN KEY(col3) REFERENCES other_table(id)
    );

Tables can have multiple foreign keys (i.e. using [associative tables](https://en.wikipedia.org/wiki/Associative_entity) for many-to-many relations)

#### Force foreign key constraints
Throw an error if an invalid foreign key is inserted

    PRAGMA foreign_keys = ON:

### Table Joins
#### INNER JOIN, ON
Add data from another table based on a foreign key

    SELECT * from left_table
    INNER JOIN right_table
    ON left_table.col3=right_table.id;

All columns of `right_table` data are appended to right of the columns of `left_table` data.

For an `INNER JOIN`, only rows where there is match between `left_table.col3` and `right_table.id` are returned.

#### LEFT OUTER JOIN / RIGHT OUTER JOIN
Similar syntax to `INNER JOIN`

    SELECT * from left_table
    LEFT OUTER JOIN right_table
    ON left_table.col3=right_table.id;

For a `LEFT OUTER JOIN`, all rows from `left_table` are returned. Missing `right_table` values are returned rows of NULL data.

`RIGHT OUTER JOIN` is the reverse of `LEFT OUTER JOIN`. It is rarely used.
