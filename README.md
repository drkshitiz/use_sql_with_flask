# Use_sql_with_flask
Postgresql <https://www.postgresql.org/docs/12/tutorial-createdb.html> is one of the sql versions. Install it before proceeding further.

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

## Create new database.
Create new database from ubuntu prompt ```$ sudo -u postgres createdb <name-of-new-database>```.

## Access database
Access a database using ```psql <databaseName>```.

### Create table in the database
```
CREATE TABLE flights (
    id SERIAL PRIMARY KEY,
    origin VARCHAR NOT NULL,
    destination VARCHAR NOT NULL,
    duration INTEGER NOT NULL
);
```
Use ```\d``` to see different parts of the database.

### SQL constraints for columns
```
NOT NULL, UNIQUE, PRIMARY KEY, DEFAULT, CHECK
```

### How to insert data into a SQL table
```
INSERT INTO flights
(origin, destination, duration)
VALUES ('New York', 'London', 415);
```
## How to read tables of SQL database
### SELECT columns - How to select data from COLUMNS of a SQL table
```
SELECT * FROM flights;
SELECT origin, destination FROM flights;

```

### WHERE clause to filter rows from an SQL table
```
SELECT * FROM flights WHERE destination = 'Paris' AND duration > 500;
```

### 'LIKE %a%' - Select for row in which origin starts has a
```
SELECT * FROM flights WHERE origin LIKE '%a%';
```
### Perform calculations on tables in the database
#### Count number of rows in a SQL table
```
SELECT COUNT(*) FROM flights;
```

#### Calculate average - AVG - in SQL table
```
SELECT AVG(duration) FROM flights WHERE origin = 'New York';
```

## UPDATE entries in tables of a SQL database
```
UPDATE flights SET duration = 430 WHERE origin = 'New York' AND destination = 'London';
UPDATE flights SET duration = duration + 15 WHERE origin = 'New York' AND destination = 'London';
```

## Delete entries from the table
```
DELETE FROM flights WHERE destination = 'Tokyo';

```
## How to limit number of results from a SQL table
```
SELECT * FROM flights LIMIT 2;
```

## ORDER BY - How to sort SQL table
```
SELECT * FROM flights ORDER BY duration ASC;
SELECT * FROM flights ORDER BY duration ASC LIMIT 3;
```

## Group By and multiple SELECt parameters HAVING clause
```
SELECT origin, COUNT(*) FROM flights GROUP BY origin;
SELECT origin, COUNT(*) FROM flights GROUP BY origin HAVING COUNT(*) > 1;
```

## Foreign keys usage in sql
```
CREATE TABLE passengers(
  id SERIAL PRIMARY KEY,
  name VARCHAR NOT NULL,
  flight_id INTEGER REFERENCES flights
  )
```

## Joins
Joins are useful if we have to deal with multiple tables.
### inner JOIN
Inner join tabulates the matching values of the two tables
```
SELECT origin, destination, name FROM flights JOIN passengers ON passengers.flight_id = flights.id;

SELECT name, origin, destination FROM flights JOIN passengers ON passengers.flight_id = flights.id WHERE origin = 'New York';
```
### LEFT JOIN
left join shows the matching rows + remaining rows of the left table.
```
SELECT origin, destination, name FROM flights LEFT JOIN passengers ON passengers.flight_id = flights.id;
```
## Complex SQO queries
```
SELECT * FROM flights WHERE id IN (SELECT flight_id FROM passengers GROUP BY flight_id HAVING COUNT(*) > 1);
```
## How to get help in postgresql
```\h``` - General help

```\h INSERT``` - help on INSERT ommand
## Services for hosting sql databases <https://www.adminer.org/> (https://adminer.cs50.net/).

## Race conditions and SQL transactions
Help in avoiding running multiple transactions at the same time.
### Begin and commit commands

# SQL alchemy library
SQL alchemy library helps in connecting python and SQL to develp web applications. 
