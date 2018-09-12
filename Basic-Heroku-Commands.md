### Deleting an app
* `heroku apps:destroy`

### Add postgresql database to project
* `heroku addons:create heroku-postgresql:hobby-dev`

### Enter the postgresql database
* `heroku pg:psql`

### Export table from a Heroku database
* The normal `copy` command doesn't work with these permissions. Use this one instead: `\COPY tableName TO 'path/to/file.csv' WITH (FORMAT csv, DELIMITER ',',  HEADER true);`

### Process for creating a table from an app
* Open the python console in your Heroku instance: `heroku run python`
* Import the `db` class from SQLAlchemy: `from app import db`
* Create the `db` tables: `db.create_all()`
* `exit()`

### Backups
* Manually backing up a database: `heroku pg:backups:capture --app appName` (Note: in the `hobby` plan, only 2 manual backups are kept)
* Setup scheduled backups: `heroku pg:backups:schedule --at '00:00 America/New_York' --app appName`
* Check scheduled backups: `heroku pg:backups:schedules --app appName`
* Check backups: `heroku pg:backups --app appName`
* Download latest backup: `heroku pg:backups:download`
* Restore database from a backup:
  * Local database: `pg_restore --verbose --clean --no-acl --no-owner -h localhost -d databaseName latest.dump `
