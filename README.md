# Use_sql_with_flask
Postgresql is one of the sql versions. Install it before proceeding further.

## start using postgresql on ubuntu
To start fresh remove the old Install
```
sudo apt-get remove postgresql
```
Install new postgresql copy
```
sudo apt-get install postgresql
```
To set the password
```
sudo passwd postgres
```
Start the service (If you do not do this step, server running error will be shown)
```
sudo service postgresql start
# connect to postgresql
sudo -u postgres psql
```
We can quit postgres by using ```\q```.

# Create new database.
Create new database from ubuntu prompt ```$ sudo -u postgres createdb <name-of-new-database>```.

## Access database
Access a database using ```psql <databaseName>```.

# Create
```
CREATE TABLE flights (
    id SERIAL PRIMARY KEY,
    origin VARCHAR NOT NULL,
    destination VARCHAR NOT NULL,
    duration INTEGER NOT NULL
);

```
