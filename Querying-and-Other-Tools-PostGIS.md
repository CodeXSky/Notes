Here are some examples of queries and other useful commands.

### Queries
* Selecting by location and counting: `select count(t.pickup_latitude) from green_trips as t, nynta as n where n.ntaname = 'East Harlem North' and st_intersects(t.the_geom,n.geom);`
* Selecting by location with a radius: `select t.pickup_longitude from green_trips as t, nynta as n where n.ntaname = 'West Village' and st_dwithin(t.the_geom,n.geom,100);`
* Adding trips by location: `select n.ntaname, count(t.pickup_latitude) from nynta as n, green_trips as t where st_intersects(t.the_geom,n.geom) group by n.ntaname;`
* More adding trips by location: `select n.ntaname, count(pickup_latitude) as total, sum(t.cash) as sum_cash, sum(t.credit) as sum_credit from nynta as n, green_trips as t where st_intersects(t.the_geom,n.geom) group by n.ntaname;`

### Other
* List all databases with `\l`.
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