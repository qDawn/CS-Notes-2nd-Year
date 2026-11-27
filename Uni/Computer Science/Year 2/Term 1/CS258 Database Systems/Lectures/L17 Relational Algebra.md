
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

![[Pasted image 20261127182552.png]]

## Natural Join ($\ast$)

- Join attributes must have the same name
- Join condition is specified implicitly
- Duplicate columns are omitted 
- Often preceded by a rename
	- to make sure the tables have the appropriate matching headings
 ![[Pasted image 20261127182951.png]]

![[Pasted image 20261127183007.png]]

![[Pasted image 20261127183016.png]]

![[Pasted image 20261127183043.png]]

- Dnumber is present in both DEPARTMENT AND DEPT_LOCATIONS
- So we can do a natural join without renaming first
![[Pasted image 20261127183125.png]]

## Completeness

- For expressivity, we need not consider all of the operations
- Some are included for convenience or brevity
- An example complete set of operations would be
	- $\{\sigma,\pi,p,\cup,-,\times \}$
	- Other operations can be expressed in terms of this set of operations
	- For example, from the above complete set we can make
	- $R\cap S\equiv (R\cup S)-((R-S)\cup(S-R))$
	- $R\bowtie_{\text{<condition>}}S \equiv \sigma_{\text{<condition>}}(R\times S)$

# Division

## The Division Operator

If the Product (Cross Join) operator looks like $\times$
- What would an operator that looks like $\div$ do to a pair of relations
- What would it mean? Would it be useful?

![[Pasted image 20261127183546.png]]![[Pasted image 20261127183555.png]]

![[Pasted image 20261127183654.png]]

## SQL Approach to Division

![[Pasted image 20261127183722.png]]

## Creating Division R $\div$ S

![[Pasted image 20261127183749.png]]

## Division: R(Z) $\div$ S(X)

- S(X) be relations such that X$\subseteq$ Z
	- i.e., S is a 'Skinny' relation. S attributes is a subset of R
- Let Y = Z - X
- R(Z) $\div$ S(X)
	- is a relation T(Y) such that t belogns to T(Y) if and only if, for every $t_{s} \in S$, there exists $t_{R}\in R$ such that 
		- $t_R[Y] = t$
		- $t_{R}[X] = t_{s}$
![[Pasted image 20261127191222.png]]

## NULL

- Technically, NULL isn't in the purest form of Relational Algebra
	- Using only first-order logic and set theory
	- No room for NULLs
- Want to represent that 23456 hasn't chosen a topic yet
	- Why store them in the topics table at all?![[Pasted image 20261127191649.png]]

![[Pasted image 20261127191746.png]]

![[Pasted image 20261127191752.png]]


## Finding a max with RA

![[Pasted image 20261127191823.png]]![[Pasted image 20261127191832.png]]


# Extension to Relational Algebra

## Outer Joins

- These deal with NULL
	- Left Outer Join
	- Right Outer Join
	- ![[Pasted image 20261127191925.png]]

## Generalised Projection

![[Pasted image 20261127191939.png]]

## Aggregate Functions

- Group tuples by values of some attributes and apply functions separately to each group
- $\text{<grouping attributes>} \beta \text{<function list>(R)}$ 
- $\text{<grouping attributes>}$ is a list of attributes of R
- $\text{<function list>}$ is a list of $\text{<<function><attribute>>}$ pairs where 
	- $\text{<function>}$ is typically one of SUM,AVERAGE,MAXIMUM,MINIMUM,COUNT
	- $\text{<attribute>}$ is an attribute of R
## Example

### List names of employees with $\geq$ 2 dependents

![[Pasted image 20261127192255.png]]

### Employees on all projects controlled by Department 5
![[Pasted image 20261127192317.png]]