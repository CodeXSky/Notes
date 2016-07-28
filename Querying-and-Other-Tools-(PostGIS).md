Here are some examples of queries and other useful commands.

### Queries
* Selecting by location and counting: `select count(t.pickup_latitude) from green_trips as t, nynta as n where n.ntaname = 'East Harlem North' and st_intersects(t.the_geom,n.geom);`
* Selecting by location with a radius: `select t.pickup_longitude from green_trips as t, nynta as n where n.ntaname = 'West Village' and st_dwithin(t.the_geom,n.geom,100);`
* Adding trips by location: `select n.ntaname, count(t.pickup_latitude) from nynta as n, green_trips as t where st_intersects(t.the_geom,n.geom) group by n.ntaname;`
* More adding trips by location: `select n.ntaname, count(pickup_latitude) as total, sum(t.cash) as sum_cash, sum(t.credit) as sum_credit from nynta as n, green_trips as t where st_intersects(t.the_geom,n.geom) group by n.ntaname;`

### Other
* List all databases with `\l`. Or list with description and size (disk usage): `\l+`
* List all databases outside Postgresql: `psql -l`
* List all tables and their size: `\d+`
* Viewing database size (inside psql): `SELECT pg_size_pretty(pg_database_size('dbname'));`
* List first n records in a table: `SELECT column (or *) FROM table LIMIT n`
* Deleting database: `drop database database_name;` or from the command line directly: `dropdb database_name`.
* Show location of database: `show data_directory;`
* Removing a constraint so you can reproject:
```sql
alter table green_trips
drop constraint "enforce_srid_the_geom";
```
* Reproject table using a new SRID:
```sql
ALTER TABLE green_trips
alter column the_geom type geometry(point,2263)
using st_transform(the_geom,2263);
```
* Print SRDI (limit to 1 row): `select st_srid(geom) from nynta limit 1;`
* To delete a specific record do: `delete from only table_name where condition returning *;`

### Viewing database data in QGIS
* Right-click on PostGIS (Browser panel) and set up a new connection.
* Add name, host is probably `localhost`, port is default `5432`, add database name.

### Creating tables from queries and exporting to csv
* Creating table from query:
```sql
create table temp_results as
select n.ntaname, count(pickup_latitude) as total, sum(t.cash) as sum_cash, sum(t.credit) as sum_credit from nynta as n, green_trips as t where st_intersects(t.the_geom,n.geom) group by n.ntaname;
```
* Exporting to csv: `copy temp_results to 'path/to/file.csv' delimiter ',' csv header;`
* Example of query: `copy (select od_pair, count(od_pair), date_trunc('year', f_ocurrencia_hecho) as year from crimes where param_hecho = 5 group by od_pair, year) to '/Users/juansaldarriaga/Google_Drive/01_SIDL/02_SIDL_Projects/1507_Victims_and_Displacement_Colombia/02_Data/02_Processed_Data/1603/OD_Pair_All_Years.csv';`
* Export table to shapefile (from outside postgres): `pgsql2shp -f "path/to/shapefile.shp" database_name table_name`

### Drop table
* `drop table tableName;`

### Change date (timestamp) format
* `SET datestyle TO "ISO, DMY";` or any other combination (MYD, YMD, etc)

### Renaming a table
* `alter table tableName rename to newTableName;`

### Joining data from two tables
* There are multiple types of joins but the normal one is `SELECT * FROM weather LEFT OUTER JOIN cities ON (weather.city = cities.name);`
* [Join Tutorial](https://www.postgresql.org/docs/8.3/static/tutorial-join.html)
* [Join Tutorial](http://www.tutorialspoint.com/postgresql/postgresql_using_joins.htm)

### Adding and updating column
* `Alter table tableName add column columnName dataType;`
* `Update tableName set columnName = ST_Distance_Sphere(tableName.geom, tableName2.geom);`
* `Update tableName set columnName = date(columnName) - date(columnName);`: produces an `int`.
