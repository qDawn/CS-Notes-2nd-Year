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