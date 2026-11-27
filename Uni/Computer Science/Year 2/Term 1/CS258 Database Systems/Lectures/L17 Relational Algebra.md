
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

## Selection ($\sigma$)

![[Pasted image 20261117210205.png]]

## Algebraic Properties

![[Pasted image 20261117210222.png]]

## Demonstrating Commutativity of $\sigma$
![[Pasted image 20261117210249.png]]

## Demonstrating Sequencing of $\sigma$
![[Pasted image 20261117210807.png]]

## Projection $\pi$

- Selection chooses Tuples
- Projection chooses Attributes
- $\pi<attribute\_list>(R)$
- Where attribute_list is the desired subset of attributes from the attributes of R.
- $\pi_{Lname,Fname,Salary}$(EMPLOYEE)

## Algebraic Properties of $\pi$ 

- If the attribute list does not include keys, result might contain duplicates:
- But in RA, duplicates are not allowed, so are eliminated
- Set (RA) vs Bag(SQL) semantics
![[Pasted image 20261117211921.png]]

- If list1 is a proper subset of list2![[Pasted image 20261117211951.png]]
- If list2 is a superset of list1![[Pasted image 20261117212008.png]]


## Renaming

- Relation Renaming
	- $p_{s}(R)$ , where s is the new name of R
- Attribute Renaming
	- $p_{B_{1},\dots,B_{n}}(R)$ , where $B_i$ are the new attribute names
- General Renaming
	- $p_{s}(B_{1},\dots,B_{n})(R)$, where you are renaming both relation and attributes
- Related SQL: SELECT T.Salary AS sal FROM TABLE T

## Relational Algebra Expressions

Describe complex operations on relations in a succint way
- Single expression
	- $\pi_{Fname,Lname,Salary}(\sigma_{Dno=5}(EMPLOYEE))$
	
Sequence with intermediate results
- DEP5_EMP5 $\gets \sigma_{Dno=5}(EMPLOYEE)$ 
- RESULT $\gets \pi_{Fname,Lname,Salary}(DEP5\_EMP5)$

Same as abpve but with renaming
- TEMP $\gets \sigma_{Dno=5}(EMPLOYEE)$
- R(First_name,Last_name,Salary) $\gets \pi_{Fname,Lname,Salary}(TEMP)$

## Set-Theoretic Operations

RA uses set semantics for relations
- so set-theoretic operations are directly applicable
Set theoretic operations require type-compatibility
- Same number of attributes, adn each attribute must type in the other relation, or fomrally:
	- Two relations, R($A_{1},\dots,A_{m}$) and S($B_{1},\dots,B_{n}$) are type compatible if 
	- m = n and dom($A_{i}$) = dom($B_{i}$) for 1 < i < n
![[Pasted image 20261126175148.png]]

Convention: resultant relations have the same attributes as R

## Examples
![[Pasted image 20261126175212.png]]

![[Pasted image 20261126175648.png]]

![[Pasted image 20261126175712.png]]

![[Pasted image 20261126175732.png]]

## Cross Join

The result of $R(A_{1},\dots,A_{m}) \times S(B_{1},\dots,B_{n})$ is a relation $Q(A_{1},\dots,A_m,B_{1},\dots,B_{n})$
such taht each tuple in Q is a combination of:
- an m-tuple from R and 
- an n-tuple from S
![[Pasted image 20261126180211.png]]

## Cross Join followed by Selection
![[Pasted image 20261127180054.png]]

# Joins $\bowtie$ 

Cross products typically meaningless unless accompanied by selection
- So create a new JOIN operator to encapulate them both

The JOIN of two relations $R(A_{1},\dots,A_{m})$ and $S(B_{1},\dots,B_{n})$ written 
## $$ R_{\bowtie<\text{join condition>}} S$$
Gives a relation with:
- Attributes: Q($A_1,\dots,A_m,B_1,\dots,B_n)$
- Tuples: consist of an m-tuple from R followed by an n-tuple from S, such that the combination satisfies the join condition
- Tupels not satisfying the condition are left out

### Join condition

The join condition can be of the form:
- $\text{<condition>}$ AND ... AND $\text{<condition>}$
- where condition is :
	- of the shape $A_{i}\theta B_{j}$, dom($A_{i}$) = dom($B_{j}$) and $\theta \in\{=,<,\leq,>,\geq,\neq\}$
Use of joins clarifies queries
- JOIN conditions clearer than Selection conditions after a Cross Join
JOIN conditions often have $\theta$ as '=' (e.g. of the form a = b)
- These are called Equijoins

## Equijoins

