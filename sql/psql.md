### PostgreSQL Command Line
Open from terminal
    >>psql

Accessing a specific database
    >>psql -d some_db

#### Useful commands
* `\q` - Quit
* `\l` - List databases
* `\dt` - List tables in current database
* `\du` - List users
* `\dp` - List user privileges

#### Managing databases
##### CREATE DATABASE, OWNER
    CREATE DATABASE some_db;
    CREATE DATABASE some_db OWNER some_user;
##### DROP DATABASE
    DROP DATABASE some_db;

#### Managing users
##### CREATE ROLE, WITH, LOGIN, PASSWORD
    CREATE ROLE some_user
    WITH <options>
    LOGIN
    PASSWORD 'some_password';

`LOGIN` allows the new user to login and run queries, which the new user can't by default.

Valid options include:
* `CREATEDB`
* `CREATEROLE`
* `SUPERUSER`

See the [full list](http://www.postgresql.org/docs/9.4/static/sql-createrole.html).

##### GRANT, ON, TO
Allow access to specific commands

    GRANT SELECT, INSERT, UPDATE, DELETE ON some_db TO some_user;

Allow all commands

    GRANT ALL PRIVILEGES ON some_db TO some_user;

##### REVOKE, ON, FROM
Removes access. Similar usage as `GRANT`.

    REVOKE ALL PRIVILEGES ON some_db FROM some_user;
