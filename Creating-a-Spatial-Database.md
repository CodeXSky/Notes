Based on [this tutorial](http://morphocode.com/how-to-install-postgis-on-mac-os-x/) from Morphocode.

### Installing PostgreSQL and PostGIS
Use [Homebrew](http://brew.sh/) to intall both:
* `brew install postgres`
* `brew install postgis`

### Starting a PostgreSQL Server
* First you need to point to the right location on your computer with `pg_ctl -D /usr/local/var/postgres start` (this is the default location).
* Create a variable that holds the path with `export PGDATA='/usr/local/var/postgres'`.
* Check to see if the server is runing with `pg_ctl status`. You should get something like this: `pg_ctl: server is running (PID: 18740)
/usr/local/Cellar/postgresql/9.4.1/bin/postgres "-D" "/usr/local/var/postgres"`.

### Creating the database
* Next you need to start the database cluster with `initdb /usr/local/var/postgres`.