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

