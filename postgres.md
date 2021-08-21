# Analytics on UN Population (using POSTGRESQL)

***
In this poject we are provided with a raw data that consists of Population statistics of different countries and region around the world. This data is provided to the United Nations Organization and can be downloaded via this link: <https://datahub.io/core/population-growth-estimates-and-projections/r/population-estimates.csv> Our aim in this project will be to view the diffrent statistical viewpoints according to the tasks given.

## Instruction

***

### 1) Install Postgresql

* Open Terminal and run the following command

```bash
sudo apt install postgresql
```

### 2) Open POSTGRESQL environment

* Change the current user to postgres user which is by deafult present in your local machine by running the following command

```bash
sudo su - postgres
```

* Now that you have changed the current user from root user to postgres, run the following command to open the pgshell environment in your terminal.

```bash
psql
```

* After this command, you will be inside a postgreql shell where you can write postgresql commands, the default command notation will be changed to

```psql
postgres=# <your command here>
```

### 3) Create a Database

* Run the following command to create a new database named 'demo'

```psql
CREATE DATABASE demo;
```

* Run the following command to list all the databases along with their user.

```psql
\l
```

* Switch to the new database 'demo' that we just created by running the following command

```psql
\c demo
```

### 4) Creating the Dataset table

* Run the following command to create an empty table named project specifying all the column attributes. Also specifying the the respective data types for column attribute.

```sql
CREATE TABLE project(Region TEXT, Country_Code INT, Year INT, Population FLOAT);
```

* Next we have to to copy the data from our CSV file to the new table created, run the following command to do so,

```SQL
COPY project
FROM '/path_to_your_csv_file'
DELIMETER ','
CSV HEADER;
```

## Queries

***
Given below are four scenarios according to which we have to write SQL queries to display the data.

### 1) India population over years

```SQL
SELECT Year, Population FROM project WHERE Region='India';
```

We were asked to output the Population of India Year-wise. Here we use WHERE clause to filter out the data where Region='India'.

### 2) For the year 2014, Population of ASEAN countries

```SQL
SELECT  Region AS ASEAN_Country, Population FROM project WHERE Year=2014 AND Region IN ('Brunei Darussalam', 'Cambodia', 'Indonesia', 'Laos', 'Malaysia', 'Myanmar', 'Philippines', 'Singapore', 'Thailand', 'Vietnam') ;
```

Here we were asked to display Population of all the ASEAN countries. We used WHERE clause to filter out the ASEAN countries population only for the year 2014.

### 3) Over the years, TOTAL population of SAARC countries

```SQL
SELECT Year, SUM(Population) as Total_Population FROM project WHERE Region IN ('Afghanistan', 'Bangladesh', 'Bhutan', 'India', 'Maldives', 'Nepal', 'Sri Lanka', 'Pakistan') GROUP BY Year;
```

Here we were asked to display the total population of SAARC countries year-wise. To sum up all the population of different SAARC countries we used the aggregate method in SQL which is SUM(), and to group the data year-wise we used GROUP BY clause.

### 4) Population of ASEAN Countries over Years

```SQL
SELECT Year, SUM(Population) as Total_Population FROM project WHERE Region IN ('Brunei Darussalam', 'Cambodia', 'Indonesia', 'Laos', 'Malaysia', 'Myanmar', 'Philippines', 'Singapore', 'Thailand', 'Vietnam') GROUP BY Year;
```

Here we were asked to display the total population of ASEAN countries Year-wise. To sum up all the population of different ASEAN countries we used the aggregate method in SQL which is SUM(), and to group the data year-wise we used GROUP BY clause.
