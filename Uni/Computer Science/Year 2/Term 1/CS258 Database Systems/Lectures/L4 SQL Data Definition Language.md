
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