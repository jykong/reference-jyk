### Python PostgreSQL Bindings Reference
    import psycopg2

#### Connect
If no server specified, defaults to `localhost`

    conn = psycopg2.connect("dbname=some_db user=some_user")

Closing connection objects

    conn.close()

#### Cursor Object
Cursor object accesses database similar to the SQL command line

    cur = conn.cursor()

#### Queries

    cur.execute(query)

Queries are queued within a transaction. The transaction is fulfilled when `commit` is called.

    cur.commit()

Use `rollback` to clear the transaction queue

    cur.rollback()

To autocommit on execute, set the `autocommit` property to `True`

    conn.autocommit = True
