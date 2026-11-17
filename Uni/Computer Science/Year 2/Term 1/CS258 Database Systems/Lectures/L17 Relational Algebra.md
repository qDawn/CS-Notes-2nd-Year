
## Formal Language for DBs
- So far we've discussed SQL
	- A 'practical' language for manipulating tables in relational DB
- But SQL came after formal design of what DBs should theoretically do
- SQL not strictly fully compliant with Relational Algebra
	- Some of these are to make it more user-friendly (less mathematical)

## What should a DB do?

Abstract thinking for RDBs
- Define key concepts and constructs
- Define key operators on the concepts
Enter Relational Algebra
- Key operators on the key RDB concept (relations) and their properties

## Relational Algebra
- An "Algebra" - defines
	- Symbols (variables)
	- Operators
	- Properties
- Operates on "Relations"
- ![[Pasted image 20261117203625.png]]

- Theoretical foundation for query languages
	- What operators can be applied on a relation?
		- What are their semantics and their properties?
		- Their inputs and outputs
		- Closure Property: input relations and output a relation
			- Allows us to nest operators
		- Operators are generic - they apply to all relations 
	- Operators on relations are combined to form algebraic expressions

Relational Algebra is procedural:
- RA expressions define what each operation does,
- Shows how results emerges as output of sequence of operators
	- Like an SQL query
		- Althought SQL is declarative
Significance
- Formally defines operations on relations
- Formally understands relation operators and expressions
- Key to understanding how to optimise query execution in a RBD system
	- query processing (implementation) and optimization
	- hence, the procedural language part

![[Pasted image 20261117204158.png]]

## Examples
![[Pasted image 20261117204804.png]]

![[Pasted image 20261117204816.png]]

![[Pasted image 20261117204825.png]]

![[Pasted image 20261117204909.png]]

## From Specification to SQL

For every project located in Stafford, list the project number, the controlling department number, department manager's last name, address and birthdate

``` SQL
SELECT Pnumber, Dnum, Lname, Address, Bdate
	FROM (SELECT * FROM PROJECT WHERE Plocation='Stafford'
	JOIN DEPARTMENT ON Dnum=Dnumber)
	JOIN EMPLOYEE ON Mgr_ssn=Ssn
```

![[Pasted image 20261117205749.png]]

## The Expression Tree

![[Pasted image 20261117205814.png]]