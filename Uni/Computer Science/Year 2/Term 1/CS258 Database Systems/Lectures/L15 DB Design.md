# Relation Database Design

- Aim: Develop a good model of the data
	- Easily understood, queried and manipulated
- How to define the best relations
	- How to group attributes together to form relations
	- How to be sure a grouping has desirable properties
- What is a good design? 
	- How good is it?
	- What are the problems with it?
	- What 'normal form' is it in?
- We need some guidelines to help decide this..

## Guideline 1: Easy to Understand

Data should be easy to understand
- Each tuple in a relation should represent one entity or relationship instance (student is enrolled on course)
	-  Attributes of different entities should not be in the same table
- Only refer to different entities with foreign keys
What not to do.. (why not?)

![[Pasted image 20261113194701.png]]

## Guideline 2: Remove Redundancy

Problems caused by Redundancy
- Storage costs - no point storing the same thing twice when we can refer to it with a foreign key
Consistency costs and potential anomalies
- If redundant data needs to be updated, need to update all affected rows
	- Costs(processing/ network time)
- Could cause inconsistencies... (what could go wrong?)

### Update Anomalies 

Redundancy causes potential update anomalies
What happens if 'Computer Science' course renamed to 'Computing'?
- Two rows updated, but what if one fails?
- Database is now in an inconsistent state
- This is an update anomaly
- Could have 100s of students on the same course with different values for CourseName 
![[Pasted image 20261113195550.png]]

### Insert Anomalies

Redundancy causes potential insert anomalies
- How should we introduce a new course?
	- {CourseID: 3, CourseName:Engineering}
	- There are no students yet
- How should we introduce a new student?
	- {StudentID: 4, SName: G. Perkins}
	- We might not know what course
- Could use NULL values? Bad idea- we will see later
### Delete Anomalies
Redundancy causes potential delete anomalies
- Delete a course, lose all information about students on that course too
	- May or may not be desirable (similar to CASCADE deletes)
- If all students on a course are deleted, all information about that course is also lost

Grouping students and courses in a single relation is undesirable, can lose information

## Guideline 2 Revisited

More formally it is:
- Design relation schemas such that no insertion, deletion and update anomalies are present
We could use TRIGGERs, etc. to maintain the 'redundant' information if we wanted to
- That would eliminate some of the problems
- But it is still 'wasteful'
	- Would use procedural techniques, processing/network/storage
More important to concentrate on good design of the base relations

## Guideline 3: No NULLs

NULL values are harmful and should be avoided
- They waste storage space
- Complicate semantics of joins, selection, aggregation
NULLs are useful for N/A, or Unknown
But if it's often NULL, why store it in the main table?
![[Pasted image 20261114220449.png]]

## Decomposition

To avoid anomalies, a bad relational schema must be decomposed into smalelr relation schemas
Need to be able to join decomposed relations
- When joining, we need exactly the original information
- No less - we don't want to lose information
- No more - we don't want extra (incorrect) information - 'spurious tuples'

## Guideline 4: No Spurious Tuples

The following design has redundancy problems 
- Why store SName multiple times?
![[Pasted image 20261114222349.png]]
Maybe break it into two - how about?
- R1(StudentID,ModuleID,Building)
- R2(SName,Building)
When we join them, we want exactly R back

e.g
![[Pasted image 20261114222415.png]]

![[Pasted image 20261114222435.png]]

## Why Functional Dependencies?

So far, we've talked about informal guidelines for a good DB design
FDs are used to specify formal measures of the "goodness" of the relational designs
Will be used to define keys
- Essential to define normal forms for relations
Then we can prove how good a relational schema design is

FD's are constraints
- Derived from the meaning and interrelationships of the data attributes of a relation schema R
- Constrains possible values different attributes may have as they depend on other attributes 
Given a set attributes X and a set of attributes Y from a relation schema R, we say:
- X functionally determines Y
	- X -> Y
	- Values of the Y component of a tuple of r(R) depend on (are uniquely determined by) the values of the X component of the tuple
- We say that the value of X determines a unique value for Y

Formally, given:
- A relation schema R
- A relation instance r(R)
- Sets of attributes X and Y (subsets of R)
X -> Y if for any tuples t1 and t2 in any relation instance r(R) it holds that:
- if t1[X] = t2[X], then t1[Y] = t2[Y]
X -> Y in R, specifies a constaint on all relation instances r(R) of R

FDs are derived from the real-world constraints on the attributes
By inspecting a given r(R)
- We can only say if a FD does not hold
- We cannot conclude if an FD holds

### Example
![[Pasted image 20261115000349.png]]

![[Pasted image 20261115000959.png]]

## Functional Dependency Overview

Let X, Y be sets of attributes of a relation schema R. A functional dependency (of Y on X), written X -> Y, is a constraint on the allowable states r of R.

- The constraint states:
	- for any t1,t2 in r, if t1[X] = t2[X] then t1[Y] = t2[Y]

![[Pasted image 20261115001521.png]]

- Schema property reflecting the semantics of attributes
- Cannot be read off a particular relation state, but can be refuted this way

- Some FD's for the example:
	- FD1: {SSN, PNumber} -> Hours
	- FD2: SSN -> Ename
	- FD3: PNumber -> {Pname,PLocation}

## (Dis)proving FDs By Inspection


Provable, there is no FD Dnumber -> Ename
- For Dnumber = 1, there are two tuples with different values of Ename
I cannot prove or disprove that Bdate -> Ename
- Each Bdate currently maps to a single Ename, but I do not know if a new tuple with an existing bdate but different ename could be added, two employees could have the same bdate
An FD is a property of the relation schema NOT of the relation state

The following can reasonably be defined as FDs:
- SSN determines employee name
- Project number determines project name and location
- Employee SSN and project number determines the hours per week the employye works on the project
- If K is a key of R, then K functionally determines all attributes in R : K -> R
	- By definition, never two distinct tuples with 
	- t1[K] = t2[K]

## FDs and the Relation Model

- Discovering and avoiding redundancy fundamentally depends on the notion of functional dependencies
- FDs specify which attributes can become keys

## Relation DBs and Normalisation

- Normalisation theory
	- Ensures it's easy for users to understand and retrieve information
	- Helps avoid storing (and needing to maintain) redundant information
- Relations with certain properties are more effective in inserting, updating and deleting data than other sets of relations containing the same data

## RDB Design and Normalisation

- Start from a "universal" all attribute listing relation
	- Progressively remove redundant data from tables
	- And thus avoid anomalies
- We can quantify how efficient a database design is:
	- Normal Forms 
	- Can use algorithms to convert from one Normal Form to another
- Normalisation generally decomposes an existing table into multiple tables
	- Re-join each time we query - so no information lost
- Using Lossless (or non-additive) joins and dependency preservation 

## Normal Forms

- First Normal Form (1NF)
- Second Normal Form (2NF)
- Third Normal Form (3NF)
- Boyce-Codd Normal Form (BCNF)
- Fourth Normal Form (4NF)
- Fifth Normal Form (5NF)
- Sixth Normal Form (6NF)

If R is of normal form i, it is also of normal form j, j < i
Typically, 3NF or BCNF will suffice 
All normal forms up to BCNF depend on FDs

## Keys and FDs - recall definitions

- Superkey - any group of attributes that server as a key
	- e.g. all attributes of a relation
- Candidate key - a minimal superkey
	- There might be > 1 candidate key
- (Primary) Key - the chosen candidate key 
- A prime (or key) attribute
	- An attribute that is part of the primary key
	- Must be a member of some candidate key
- Person(SSN,Name,HomeAddress,HomeTel,Birthplace,PassportNumber)

## Some Set Theory Definitions

Imagine we have attributes {A,B,C}
Subset: {A,B,C}, {A,B}, {B,C}, {A,C}, {A}, {B}, {C}, {}
Proper Subset: {A,B}, {B,C}, {A,C}, {A}, {B}, {C}, {}
Superset: {A,B,C}, {A,B,C,D}
Proper Superset: {A,B,C,D}
Think of "superkey" as a "superset" of a key (either it is a key itself with no extra attributes, or it is a "proper superset" with extra attributes)

## Keys and FDs 

A superkey K of relation schema R must be:
- Composed of attributes (subset of R) required so that:
	- The superkey uniquely determines each tuple in a relation
	- For any tuples t1,t2 of a relation instance r(R) 
		- If t1 != t2, then t1[K] != t2[K]
So superkeys uniquely identify/constrain tuples
FDs uniquely identify attribute values of tuples
- If A -> B and we know A, we will uniquely identify B
If K is a superkey of R, then K -> R

### Example

- With FDs, we can express constraints that can't be expressed with keys
	- BorrowLoan (CustomerID, LoanNumber, LoanAmount, LoanType)
	- If we want to have unique loan type per loan number, then define:
	- LoanNumber -> LoanType

## Normalisation: Decomposing

- As mentioned, normalisation progressively breaks large relation schemas into smaller ones
	- But not all decompositions are good - recall spurious tuples
- The following properties are important:
	- Lossless or non-additive decomposition
		- a.k.a Lossless-join or non-additive join property
		- Critical
	- Dependency preservation property
		- To be defined later
		- Desirable, but sometimes sacrificed for other factors

## Lossless Join Decomposition

- A.K.A Non-additive Join Decomposition
- Given a relation schema R and a set F of FDs for R:
	- {R1,...,Rk} is a lossless-join decomposition of schema R, if for every legal relation instance r of R 

![[Pasted image 20261116013009.png]]

pi is a projection, the bowtie symbol represents a multiplication symbol (joins results)
Start with these many projections and when combined it should form r.

- If reconstructing (JOINing) all these smaller projections, we want to get back all the tuples we started with 

### Example
![[Pasted image 20261116015047.png]]

### Example 2









