Once you have a spatial database up and running you will probably want to load some data.

### Loading Shapefiles
* To load the shapefiles you will use the shp2pgsql tool.
* First you need to figure out the SRID number of the projection. You can `cat` the .prf file of the shapefile and copy the text into this [website](http://prj2epsg.org/search).
* Then, the command is as follows `shp2pgsql -s 2263 path/to/shapefile.shp | psql -d database_name`.
* The `2263` is the SRID number for the standard projection for New York (NAD83 / New York Long Island (ftUS)).
* The SRID number for WGS84 is `4326`.
* Once this is done, you can go into the database and check to see if the shapefile was imported correctly. It should have a field called "geom" or "the_geom" representing the geometry.
* To list the fields in a table do `\d+ table_name`.
* To list tables in the database do `\dt`.

### Loading a CSV file with lat and lon
* This is a longer process. Basically, you first have to create an empty spatial table in the database, with all the fields and their data type, and then copy onto that table the csv dataset.
* Here I follow [this](http://www.kevfoo.com/2012/01/Importing-CSV-to-PostGIS/) example. Note, you have to add the lat and lon fields too (for some reason he doesn't show that in his code).
* Here is an example of creating a table for a csv file using the Green Cab data:
```sql
CREATE TABLE Green_Trips (
gid serial NOT NULL,
VendorID int,
lpep_pickup_datetime timestamp,
Lpep_dropoff_datetime timestamp,
Store_and_fwd_flag text,
RateCodeID int,
Pickup_longitude float,
Pickup_latitude float,
Dropoff_longitude float,
Dropoff_latitude float,
Passenger_count int,
Trip_distance float,
Fare_amount float,
Extra float,
MTA_tax float,
Tip_amount float,
Tolls_amount float,
Ehail_fee float,
Total_amount float,
Payment_type int,
Trip_type int,
Cash int,
Credit int,
WK_5_10 int,
WK_10_17 int,
WK_17_22 int,
WK_22_5 int,
WKND_5_10 int,
WKND_10_17 int,
WKND_17_22 int,
WKND_22_5 int,
the_geom geometry,
CONSTRAINT greenTrips_pkey PRIMARY KEY (gid),
CONSTRAINT enforce_dims_the_geom CHECK (st_ndims(the_geom) = 2),
CONSTRAINT enforce_geotype_geom CHECK (geometrytype(the_geom) = 'POINT'::text OR the_geom IS NULL),
CONSTRAINT enforce_srid_the_geom CHECK (st_srid(the_geom) = 4326)
);
```

Note: I don't know if the term `float` actually works well. It might be `float8`. This [page](http://www.postgresql.org/docs/9.4/static/datatype.html) has more info.
* Then you need to create the index (don't know exactly what that means...):
```sql
CREATE INDEX green_trips_the_geom_gist
ON green_trips
USING gist
(the_geom );
```
* Then you need to actually copy the csv file into the table. In the database do: `\copy table_name(field1,field2,field3,etc,etc) FROM 'path/to/file.csv' DELIMITERS ',' CSV HEADER;`.
* You can check that the file was imported by printing some of the columns: `SELECT column_name FROM table_name;`.
* The last step is to populate the geometry field based on the lat and lon:
```sql
UPDATE table_name
SET the_geom = ST_GeomFromText('POINT(' || lon_field_name || ' ' || lat_field_name || ')',SRID_number);
```