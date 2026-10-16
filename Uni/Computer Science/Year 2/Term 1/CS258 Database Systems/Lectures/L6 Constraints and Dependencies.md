
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
Primary Key atrributes cannot be NULL 
Because PK values uniquely identify individual tuples
If PK is a composite key of several attributes that means no NULL in any of these. 

Non-key attributes can also be declared NOT NULL, this would be a domain constraint.

## Referential Integrity Constraints
