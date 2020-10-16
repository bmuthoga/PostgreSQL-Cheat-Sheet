# PostgreSQL-Cheat-Sheet
> A summary (cheat sheet) of PostgreSQL commands for quick reference.
<hr>

# Table of Contents
1. [Introduction](#introduction)
2. [Create Database](#create-database)
2. [Create Table](#create-table)

# <a name="introduction"></a>Introduction

## PostgreSQL Datatypes
* Benefits of having datatypes:
  * Consistency
  * Data integrity
  * Performance

* The datatypes include:
  * **Numeric**
    * **Integer:** used for storing whole numbers
    * **Serial:** auto-incrementing integer
    * **Decimal:** user-specified precision

  * **Character**
    * **character(n):** Fixed to n length and padded with blanks for values shorter than n length
    * **character varying(n), varchar(n):** variable length, but limited to n
    * **Text:** variable length, unlimited

  * **Temporal**
    * **Date:** store date values only
    * **Time:** time of day only
    * **Timestamp:** date and time of day values
    * **Timestampz:** date and time of day values with the time zone

## PostgreSQL Constraints
* Constraints are a special rule that we can apply to a column that allows postgres to check if a value is valid before we insert or update it e.g. NOT NULL

* Types of constraints include:
  * **PRIMARY KEY:** uniquely identifies a row in a column or group of columns
  * **FOREIGN KEY:** specifies that value in a col or group of cols must match value in row of another table (its PRIMARY KEY)
  * **NOT NULL:** col must never accept a null value; never used as a table-level constraint
  * **CHECK:** most generic constraint type; used to specify that a val in column must satisfy a condition (Boolean expression)

    ```
    -- Example of CHECK constraint
    CREATE TABLE dogs(
      dog_id serial PRIMARY KEY,
      name varchar(255) NOT NULL,
      age integer NOT NULL,
      weight integer CHECK(weight > 0) NOT NULL
    );
    ```

  * **UNIQUE:** ensures that data in a column or group of cols is unique among all rows in a table

* Column-level constraints vs Table-level constraints:
  ```
  -- column-level constraints
  CREATE TABLE users(
    user_id serial PRIMARY KEY,
    username varchar(255) UNIQUE NOT NULL,
    password varchar(255) NOT NULL
  );

  -- UNIQUE table-level constraint
  CREATE TABLE users(
    user_id serial PRIMARY KEY,
    username varchar(255) NOT NULL,
    password varchar(255) NOT NULL,
    UNIQUE(username)
  );
  ```

# <a name="create-database"></a>Create Database
* Syntax:
  ```
  CREATE DATABASE database_name;
  ```

* Example:
  ```
  CREATE DATABASE petshop;
  ```

# <a name="create-table"></a>Create Table
* Syntax:
  ```
  CREATE TABLE table_name(column_name datatype CONSTRAINT);
  ```

* Example:
  ```
  CREATE TABLE dogs(
    dog_id serial PRIMARY KEY,
    name varchar(255) NOT NULL,
    age integer NOT NULL,
    weight integer NOT NULL
  );
  ```
