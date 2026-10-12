
## Creating Tables

CREATE TABLE <Table_Name> (attributes)
e.g 

![[Pasted image 20261009001015.png]]

![[Pasted image 20261009001216.png]]

## Attribute Data Types 
![[Pasted image 20261009001042.png]]

![[Pasted image 20261009001149.png]]

## Specifying Constraints

SQL has 3 basic constraints 

## SQL Constrains

- Key : A key value is unique
- Entity Integrity : Primary key value cannot be null
- Referential Integrity : Foreign key must have a value that is present as a primary key

## Attribute Constraints 

- NULL not permitted
- Default value ( DEFAULT <value_>)
- e.g AccountBalance REAL NOT NULL DEFAULT 0.0

CHECK clause
- AGE INT NOT NULL CHECK ( Age > 0 AND Age < 125)
- Allows attribute constraints based on application semantics

 PRIMARY KEY clause
 - Specifies one or more attributes that make the primary key of a relation
 - Dnumber INT PRIMARY KEY; 

 UNIQUE clause 
 - Specifies alternate (secondary) keys called candidate keys in the relational model
 - Dname VARCHAR(15) UNIQUE;
 
![[Pasted image 20261009002814.png]]

## Referential Integrity Constraints

- FOREIGN KEY adds constraint to check/ handle during updates
	- Usually prevents violations
	- Also, make a referential triggered action :
		- SET NULL
		- SET DEFAULT
		- CASCADE
	- Can define a different action for different types of update
		- ON DELETE and ON UPDATE
![[Pasted image 20261009010755.png]]

### If a supervisor's row is deleted the tuple referencing it will have the super_id set to NULL


![[Pasted image 20261009010909.png]]

![[Pasted image 20261009011303.png]]

## Constraints - PRIMARY KEY syntax

###  <attName_> <attType_> PRIMARY KEY

Identifies an attribute as a primary key, this means that it is unique

e.g
``` SQL
StudentID INT Primary Key
```

## UNIQUE syntax

<attName_> <attType_> UNIQUE

defines a unique/secondary key
e.g
``` SQL
StudentID INT UNIQUE
```

attributes defined as UNIQUE can be NULL unless explicitly defined as NOT NULL

## Foreign Key

``` SQL

FOREIGN KEY <attName1> REFERENCES <table>(<attname2>)

```
Refers attributes across tables

![[Pasted image 20261013003621.png]]

Foreign Key doesn't have to reference an attribute of same name, only cares about the values

FK's impose a fixed order to operations, before adding a student on courseID = 3 you must add the course to the course table.

## Attribute Constraints


``` SQL
<attName> <attType> CHECK (boolean expression)
```


Check can be defined either next to the definition of the attribute or at the end of the create table.
![[Pasted image 20261013004333.png]]

can also name constraints 

``` SQL
CONSTRAINT <constraintName> <constraint>
```
### Default values

courseID INT DEFAULT 1;
sets default value for attributes to 1 if not assigned 

## Syntax for RI actions

![[Pasted image 20261013004609.png]]

## Drop table

DROP TABLE <tablename_>

deletes the schema and data