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