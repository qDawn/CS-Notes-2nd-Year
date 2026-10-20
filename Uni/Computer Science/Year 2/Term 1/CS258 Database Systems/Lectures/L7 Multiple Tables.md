## Selecting From Multiple Tables

``` SQL 
SELECT * FROM students,courses;
```

![[Pasted image 20261020175454.png]]

This command gives us the Cartesian product, concatenating each row from R with each row from S, size of result R x S

Think of it like scanning through using a nested loop, as we are looping through two tables.

## Why Multi-table queries?

Information spread across different tables about entities
- e.g all <name, course name> pairs of students and their courses

Although the Cartesian product contains superfluous/wrong information. We need to restrict the result to a subset, 

![[Pasted image 20261020175810.png]]

You can use a WHERE block to restrict the rows, to fix this specific problem you can do the following :

``` SQL 
SELECT * FROM students, courses
WHERE students.courseID = courses.courseID;
```

## More on Multi-Relation Queries

If attributes have the same name we can distinguish them with the following 
``` SQL
<relation>.<attribute>
```

![[Pasted image 20261020180249.png]]

## Explicit Tuple Variables
![[Pasted image 20261020180416.png]]

In event of a Self Join these restrictions are good for removing the usually unwanted rows.

## CROSS JOIN

CROSS JOIN can be used in place of a comma when referencing multiple tables. R,S == S,R. 
However, the order would be different. In SQL if you want a specific order, use ORDER BY.

