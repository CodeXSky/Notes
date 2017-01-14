Based on [this tutorial](http://morphocode.com/how-to-install-postgis-on-mac-os-x/) from Morphocode.

### Installing PostgreSQL and PostGIS
Use [Homebrew](http://brew.sh/) to intall both:
* `brew install postgres`
  * You will get this as an answer:
  ```bash
  ==> Installing dependencies for postgresql: readline
  ==> Installing postgresql dependency: readline
  ==> Downloading https://homebrew.bintray.com/bottles/readline-7.0.1.sierra.bottle.tar.gz
  ######################################################################## 100.0%
  ==> Pouring readline-7.0.1.sierra.bottle.tar.gz
  ==> Caveats
  This formula is keg-only, which means it was not symlinked into /usr/local.

  macOS provides the BSD libedit library, which shadows libreadline.
  In order to prevent conflicts when programs look for libreadline we are
  defaulting this GNU Readline installation to keg-only.


  Generally there are no consequences of this for you. If you build your
  own software and it requires this formula, you'll need to add to your
  build variables:

      LDFLAGS:  -L/usr/local/opt/readline/lib
      CPPFLAGS: -I/usr/local/opt/readline/include

  ==> Summary
  🍺  /usr/local/Cellar/readline/7.0.1: 46 files, 2M
  ==> Installing postgresql 
  ==> Downloading https://homebrew.bintray.com/bottles/postgresql-9.6.1.sierra.bottle.tar.gz
  ######################################################################## 100.0%
  ==> Pouring postgresql-9.6.1.sierra.bottle.tar.gz
  ==> Using the sandbox
  ==> /usr/local/Cellar/postgresql/9.6.1/bin/initdb /usr/local/var/postgres
  ==> Caveats
  If builds of PostgreSQL 9 are failing and you have version 8.x installed,
  you may need to remove the previous version first. See:
    https://github.com/Homebrew/homebrew/issues/2510

  To migrate existing data from a previous major version (pre-9.0) of PostgreSQL, see:
    https://www.postgresql.org/docs/9.6/static/upgrading.html

  To migrate existing data from a previous minor version (9.0-9.5) of PostgreSQL, see:
    https://www.postgresql.org/docs/9.6/static/pgupgrade.html

    You will need your previous PostgreSQL installation from brew to perform `pg_upgrade`.
    Do not run `brew cleanup postgresql` until you have performed the migration.

  To have launchd start postgresql now and restart at login:
    brew services start postgresql
  Or, if you don't want/need a background service you can just run:
    pg_ctl -D /usr/local/var/postgres start
  ==> Summary
  🍺  /usr/local/Cellar/postgresql/9.6.1: 3,242 files, 36.4M
  ```
* `brew install postgis`

### Starting a PostgreSQL Server
* First you need to point to the right location on your computer with `pg_ctl -D /usr/local/var/postgres start` (this is the default location).
* Create a variable that holds the path with `export PGDATA='/usr/local/var/postgres'`.
* Check to see if the server is runing with `pg_ctl status`.
* You should get something like this: `pg_ctl: server is running (PID: 18740)
/usr/local/Cellar/postgresql/9.4.1/bin/postgres "-D" "/usr/local/var/postgres"`.

### Creating the database
* Next, if this is a fresh install, you need to start the database cluster with `initdb /usr/local/var/postgres`.
* Finally, create a new database with `createdb database_name`.
* To connect to the new database do `psql database_name`.
* You need to enable PostGIS: `CREATE EXTENSION postgis;` (Remember, the sql commands end with a `;`).
* To check if you have PostGIS support do `SELECT PostGIS_Version();`.
* To quit psql type `\q`.

### Other commands
* Stop postgresql: `pg_ctl -D /usr/local/var/postgres stop -s -m fast`.
* Start postgresql and use a log file: `pg_ctl -D /usr/local/var/postgres -l /usr/local/var/postgres/server.log start`.
* Drop a database: `dropdb database_name`.
* Delete a postgresql cluster: `rm -rf /usr/local/var/postgres/`.
* List all tables in database: `\dt`.
* List all databases (from terminal prompt): `psql -l`
* List all previous commands (history): `\s`

### Useful links
* Find the SRID number [here](http://prj2epsg.org/search) by copying the text of the .prj file. You can do the reverse [here](http://www.epsg-registry.org/).
* This [cheatsheet](http://www.bostongis.com/pgsql2shp_shp2pgsql_quickguide.bqg) seems to be useful for loading data.
* [Here](http://workshops.boundlessgeo.com/postgis-intro/index.html) is the Boundless tutorial for the GUI version of PostGIS.