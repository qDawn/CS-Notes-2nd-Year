## Overview:

- 1NF: All attributes are atomic, and there is a key
	- "the key"
- 2NF: Non-key attributes are dependent on the full key (actually, any candidate key)
	- "the whole key"
- 3NF: Non-key attributes are only dependent on the key (actually, any candidate key)
	- "nothing but the key"
- BCNF: Every determinant (of a non-trivial FD) is a superkey

## Unnormalised Relation(0NF/UNF)

- First step is to convert data into a two dimensional table (relation)
- In unnormalised relations, the same type of data may need multiple columns, might need to repeat similar attribute names (Author1,Author2,...)
- ![[Pasted image 20261117145744.png]]
- This makes queries slightly tricky
	- If we want to find a lecturer's office, need to do string manipulation
	- Can't represent students on $\geq$ 3 modules
- This defeats the whole point of a database
	- So we must normailse it

## First Normal Form (1NF)
- All attributes are atomic 
	-  Have no repeating groups
	- Attributes cannot have a substructure
		- Multi-valued attributes (e,g,, comma separated list, "MB3.21,MB3.23")
		- Composite attributes (e.g., address: Department of Computer Science, University of Warwick, CV4 7AL)
	- Formally, the domains of attributes must be atomic
	- Data can be queried, search and updated more easily (without string manipulation)
- There is a key defined ("the key")
	- Therefore, there are no duplicate rows

## From 0NF to 1NF

![[Pasted image 20261117150855.png]]

## Now choose the key

Assume:
- Students can take many modules
- Modules can have many students

Think of FDs
- StudentID $\to$ {SName}
- ModuleID $\to$ {ModuleName,Lecturer}
- Lecturer $\to$ LecturerOffice

{StudentID,ModuleID}$^+$ determines all 6 attributes
- ModuleID $\to$ Lecturer $\to$ LecturerOffice
- {StudentId,ModuleID} $\to$ {SName,ModuleID,ModuleName,Lecturer,LecturerOffice}
- {StudentID,ModuleID} is a minimal superkey $\therefore$ candidate key
![[Pasted image 20261117173204.png]]

## 1NF: Storage Anomalies

Insertion
- New student hasn't chosen a module yet, can't insert them
- Can't represent a new module without having a student enrolled on it

Update
- If you have a lecturer change, have to update multiple rows

Delete
- Deleting a student might delete all information about module (if the only student)
	- e.g., if Bob is deleted, we lose existence of CS140
- Deleting a tuple can remove facts about multiple entities at once

U(StudentID, SName, ModuleID, ModuleName, Lecturer, LecturerOffice)

## Second Normal Form (2NF)

- A relation is said to be in 2NF if 
	- It is in 1NF, and
	- Every non-key attribute is fully functionally dependent on any key
		- If the key is a single attribute and is 1NF.. 2NF is automatically satisfied
- So, for every key K of R, for every non-key attribute A of R:
	- K $\to$ is irreducible
		- i.e it's impossible to break K into a smaller subset
- No proper subset of the key functionally determines a non-key attribute
- "The whole key"

- 2NF improves data integrity
	- Prevents update, insert and delete anomalies
- Consider:
	- R(A,B,C,D)
	- FDs: AB $\to$ C, A $\to$ D
	- Is this in 2NF?
- 2NF Criteria
	- For every K of R and every nonkey attribute A of R:K $\to$ {A} is irreducible
- What's the problem here?
	- A $\to$ D is a "partial dependency" - it only depends on part of the key

## 1NF to 2NF

U(StudentID, SName, ModuleID, ModuleName, Lecturer, LecturerOffice)
Think of FDs
- StudentID $\to$ {SName}
- ModuleID $\to$ {ModuleName,Lecturer}
- Lecturer $\to$ LecturerOffice

The first two FDs violate 2NF, so decompose into relations based on those FDs (extracting out the RHS attributes)
- Student(StudentID,SName)
- Module(ModuleID,ModuleName,Lecturer,LecturerOffice)

Which leaves
- Enrolment(StudentID,ModuleID)

Note: we need a key, otherwise we'd allow duplicate rows

## 2NF

Now in 2NF:
- StudentID $\to$ (StudentID,SName)
- ModuleID $\to$ (ModuleID, ModuleName,Lecturer, LecturerOffice)
- Enrolment $\to$ (StudentID,ModuleID)
![[Pasted image 20261117174955.png]]

There are no partial dependencies
- Everything depends on "the whole key"

Every non-key attribute is fully functionally dependent on any key
- If the key is a single attribute and is 1NF.. 2NF is automatically satisfied

## Fixed 1NF Anomalies

- Now in 2NF:
	- StudentID $\to$ (StudentID,SName)
	- ModuleID $\to$ (ModuleID, ModuleName,Lecturer, LecturerOffice)
	- Enrolment $\to$ (StudentID,ModuleID)
- We've eliminated the 1NF anomalies
	- INSERT: Can now insert student without module
	- INSERT: Can now insert module without student
	- UPDATE: Can now change lecturer in a single row
	- DELETE: Deleting a student won't delete information about a module

## 2NF - Storage Anomalies

Despite fixing the 1NF anomalies we still have :
- INSERT: Can't represent a Lecturer unless they teach a module
- DELETE: Deleting instances of a module might delete information about a lecturer 
- UPDATE: If a lecturer moves office, we might need to update multiple rows

