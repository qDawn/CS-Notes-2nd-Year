
# Definitions

Schema of a Relation:
- Denoted by R(A1,A2,...,An)
- R is the name of the relation
- Attributes of the relation are A1,A2,...,An

Example:
- CUSTOMER(CustID,CustName,Address,PhoneNum)
	- Customer is the relation name
	- Defined over the 4 attributes
- Each attribute has a domain:

A duple is a sequence of values, each value is derived from an appropriate domain
A relation is a set of such tuples(rows)

A domain has a logical definition in real world. Such as UK phone numbers where the domain is 11 decimal digits 

The state of a relation is the set of tuples currently in the relation
It is therefore a subset of the Cartesian Product of the domains of its attributes

Given R(A1,A2,...,An) 

# More on the Relational Model 

- Order is not important for the tuples in a relation and attributes in a tuple 
- Collection of relation schemas (intension)
- Corresponding relation instances/states (extension)
- Metadata : includes schema

# Why Relations? 

Very simple model 
- Often a good way to think about data and access it
Abstract Model but 
- enriched with declarative languages like SQL 
Model is set-oriented
- Sets of attributes in a tuple 
- Sets of tuples in a relation

# Relational DB Constraints

- Constraints determine permissible states of relation instances
- Four types of constraints in R-DBMSs
	- Key constraints 
		- Each tuple 
	- Entity integrity constraints
		- Ensure primary key attributes are never NULL
	- Referential integrity constraints
		- Ensure foreign key values refer to existing tuples in the referenced relation
	- Domain constraints
		- Attribute values of a tuple must come from the domain of that attribute and follow any other restrictions for that attribute. (coule be NULL if allowed)
## Key Constraints

Superkey of R: a subset of attributes of R, such that:
- In any valid state for R, r(R):
	- For any two distinct tuples t1 and t2 in r(R)
	- t1[SK] != t2[SK] 

## Candidate Keys

A candidate key is a minimal superkey
- Any key K is a minimal superkey if:
	- Removal of any attribute from K results in a set of attributes that is no longer a superkey
- If a relation has several candidate keys, one is chosen arbitrarily to be a primary key

## Entity Integrity Constraints
Primary Key attributes cannot be NULL 
Because PK values uniquely identify individual tuples
If PK is a composite key of several attributes that means no NULL in any of these. 

Non-key attributes can also be declared NOT NULL, this would be a domain constraint.

## Referential Integrity Constraints

A logical DB design spreads information across multiple tables 
Following good DB design practices spreading queryable info across tables is warranted
- Need to consider how to link tables with Foreign Key relationships

## Referential Integrity
When one table references a primary key, need to be careful 
- What if the referenced row is deleted
- What if the referenced row has its key value changed

A set of attributes FK from relation R1 is a foreign key that references relation R2 if
- Attribute(s) in FK from R1 have same domain as the attribute(s) in the primary key PK of R2, and 
- A value of FK in a tuple t1 of R1 must either:
	- Refer to a value of the PK of some tuple t2 in R2
	- Or, be NULL
- Formally:
	- t1 in R1 references t2 in R2
		- if R1.t1[FK] = R2.t2[PK],or
		- R1.t1[FK] is NULL
- For instance, if Students(StudentID,Name,DoB) contains only:
- (1,'AB','2/5/2007')
- (2, 'BC', '3/7/2007')
	- Enrollments can only contain StudentID values of 1, 2 or NULL

## More about Constraints

- In SQL, use CREATE TABLE to describe: 
	- Keys
	- Permissibility of NULL values
	- Candidate Keys(Unique)
	- Foreign Keys
	- Referential Integrity behaviour
- There are also semantic attribute integrity constraints
	- Depending on application semantics:
		- Employee salary < Manager Salary
		- Student can't be registered twice on the same module
		- Module Organiser must be a member of 'Teaching' staff