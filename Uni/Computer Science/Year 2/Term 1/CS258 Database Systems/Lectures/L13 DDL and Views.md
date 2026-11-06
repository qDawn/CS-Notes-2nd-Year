
## Database Schemas

- CREATE SCHEMA studentInfo AUTHORIZATION 'JSmith'
- Not for average user (but for the SysAdmin/DBA)
- SQL stores schemas within a catalogue/dictionary
- Some DBMSs have a special INFORMATION_SCHEMA with the metadata
- Tables are stored within schemas

## Data on Tables/Model

To find out more about a table schema:
- Postgres: \d table_name
- MySQL: DESCRIBE table_name
- Oracle: DESC table_name

Returns detailed schema info for the table, including column names, types, integrity constrains,etc.
![[Pasted image 20261106022755.png]]

## DROP TABLE

Destoroys the table including the schema.

- IF EXISTS: Stops the error thrown if table doesn't exist
- CASCADE: Removes the foreign key constraints of any other table that references the table
- RESTRICT: Drop only if table is not referenced by other elements otherwise error message, is the default 

## ALTER TABLE (Add Column)

``` postgresQL
ALTER TABLE <tableName> ADD <attName> <dataType> <constraint>;
```

Add a new column, with the following
New column is filled initially with DEFAULTs or NULL for each existing row
In theory, order of columns doesn;t matter so new columns are always added to the end

### Drop Column

``` postgresQL
ALTER TABLE <tableName> DROP COLUMN <attName> <dataType> <constraint>;
```

Removes the column/attribute, named <attName\> from the table. It also destroys the data for this column

### Renaming 

Table renaming
``` postgresQL
ALTER TABLE <tableName> RENAME TO <newTableName>;
```

Column renaming
``` postgresQL
ALTER TABLE <tableName> RENAME COLUMN <attName> TO <attNameNew>;
```

### Constraints

Removing constraints
``` postgresQL
ALTER TABLE <tableName> DROP CONSTRAINT <constraintName>;
```

Adding constraints
``` postgresQL
ALTER TABLE <tableName> ADD CONSTRAINT <constraintName><constraints>;
```

Altering
- Impossible, in order to change you must drop and recreate with a new definition

### Alternative to Modifying Tables

- Requirements change over time. so might need to modify tables
- However, modification can be problematic, especially if there are constraints
- Some DBMSs have limitations, e.g. SQLite only allows renaming tables and adding columns
- Alternatively:
	- Create a new table, based on old table plus modifications
	- Copy data across
	- DROP old table
	- RENAME new tabe to match old name

# VIEWs/Virtual Tables

An SQL VIEW is a table derived from other tables

Often use a virtual view
- Doesn't store data
- Effectively a shortcut for a more complex query
Useful for frequently used queries
Useful for authorisation, use VIEWs to present a subset of data, and restrict access to the VIEWs
Can be queired like tables
Automatically updated by DBMS when base relations are updated

Created through:

``` postgresQL
CREATE VIEW <name> AS <query>
```

![[Pasted image 20261106030737.png]]![[Pasted image 20261106030746.png]]

## VIEW Implementation Strategies

- Query modification
	- DBMS translates a virtual view query into a query to address the base tables (very small overhead depending on the complexity of the query)
- View materialisation
	- Create a temporary table (needs storage and incremental updates)
``` PostgreSQL
	  CREATE MATERIALIZED VIEW my_view AS ...
```
- Updates on views
	- Can allow UPDATEs on VIEWs for simple simple views of a single table
	- The update needs to translate unambiguosly to operations on the underlying tables
	- Usually impossible if the VIEW involves:
		- joins,grouping,aggregates,DISTINCT, set operations
![[Pasted image 20261106031119.png]]