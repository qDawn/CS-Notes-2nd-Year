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

