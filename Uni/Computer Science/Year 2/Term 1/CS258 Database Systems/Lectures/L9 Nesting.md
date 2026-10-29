
## Sub queries / Nested queries

A parenthesised SELECT-FROM_WHERE statement can be used as a value at
- the FROM (to select results from a subquery)
- the WHERE (to compare rows with values from a subquery)

Instead of naming a table in the FROM clause, provide a subquery instead
- This nested query will return a new table, call it tempTable
- So the above is equivalent to having created a table, using its name, tempTable in the FROM clause
- Useful to use a tuple-variable to name tuples of the result of the nested query
![[Pasted image 20261028234727.png]]

## Scalar Subqueries 

It's possible to use arithmetic comparisons if the subquery returns one value. If so it is similar to comparing two numbers, formally it is a relation with one row and one column.

### Example 
From Exam Marks, find the students who got the same mark for CS140 that student 1 got for CS118.

Two Steps :
- Find the mark student 1 got for CS118, treat it as a known value
- Find students who got that mark for CS140

``` SQL 
SELECT studentID FROM ExamMarks
WHERE Module = 'CS140'
AND Mark = (SELECT Mark FROM ExamMarks WHERE studentID = 1 AND Module = 'CS118')
```

## Why Nest?

Allows us to simplify complex SQL queries
- We can use subqueries to break down complex problems into more manageable, understandable steps
- Same query can often be written in many ways, often solutions with JOIN

## Nesting with the IN Operator

The following evaluates to true if and only if the tuple is a member of the relation
tuple IN relation

IN Expressions can appear in WHERE clauses 

![[Pasted image 20261029003411.png]]

![[Pasted image 20261029003428.png]]

## IN matching with Tuples

Also works for matching tuples of values for a query 
``` SQL 
SELECT <attNameList> FROM <tableList>  
WHERE (<attName1>,<attName2>,...,<attNameN>)  
IN  
(SELECT <attName1>,<attName2>,...,<attNameN>  
FROM <tableList> WHERE <expr>);
```

![[Pasted image 20261029004034.png]]

# JOIN vs Subqueries

``` SQL 
SELECT R.a FROM R,S WHERE R.b = S.b;

==

SELECT R.a FROM R WHERE R.b IN (SELECT b FROM S);
```

![[Pasted image 20261029004914.png]]

![[Pasted image 20261029004826.png]]

# Nested Queries and IN 

![[Pasted image 20261029005127.png]]

