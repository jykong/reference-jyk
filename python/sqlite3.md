### Python SQLite Bindings References
    import sqlite3

#### Connect
Connecting obtains a single access file lock, no multi-app access

    conn = sqlite3.connect('database_filename.db')

Closing connection objects

    conn.close()

#### Queries & Cursor Object
Cursor object accesses database similar to the SQL command line

    query = "select col1 from some_table;"
    cur = conn.cursor()
    cur.execute(query)
    results = cur.fetchall()

SQLite commits each query automatically.

SQLite allows the cursor object to be bypassed by calling execute from the connection object. This creates an anonymous cursor object behind the hood.

    results = conn.execute(query).fetchall()

#### Fetching Output
Each row returned as a tuple

    one_result = cur.fetchone()
    all_results = cur.fetchall()       # returns list of tuples
    n_results = cur.fetchmany(n_rows)  # returns list of tuples
