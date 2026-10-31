
<b> JOINs allow us to query data that is combined from multiple tables simultaneously.</b>

# Products and Natural Joins

The Cartesian product is obtained through 
``` MySQL
R CROSS JOIN S
```
This is the exact same as R,S 

## Natural JOIN

``` MySQL
R NATURAL JOIN S
```

This forms the cartesian product of R and S however, this time it looks for attributes of R having the same name type and value as S and keeps it.

## Theta JOINs and JOIN... ON

Theta joins are extensions to natural joins, they combine product and selections into one operation.
``` MySQL
R JOIN S ON <condition>
```

condition uses a comparison operator, {=,<,<=,>,>=}
if using = it is an equi-join.

## INNER JOINS

Default operator is called INNER JOIN

<b>INNER JOIN = JOIN = , </b>

## Non-EquiJoins

![[Pasted image 20261030234435.png]]![[Pasted image 20261030234651.png]]

## More than two tables e.g
![[Pasted image 20261030235032.png]]

## Other Key Aspects 

- Boolean expression in ON doesn't have to use matching column names
- Instead they can be referred to with quantification and aliasing
- Boolean expressions don't always have to be =
- JOINs can be chained together 

## Inner Join vs Outer Joins

Inner Joins can 'lose' information
- A tuple that doesn't join with any tuple from the other relation doesn't appear in the result 
- For a LEFT OUTER JOIN, if there is no matching tuple on the right, it is padded with NULLs
- Same for a RIGHT OUTER JOIN instead the LEFT table (first table) is padded
## FULL OUTER JOIN

FULL OUTER Joins union the LEFT and RIGHT OUTER Joins. Essentially padding eithe side depending on which one is missing values.

## Join Syntax

![[Pasted image 20261031011947.png]]

## NATURAL OUTER JOINs

![[Pasted image 20261031012341.png]]

## USING

Keyword can be used instead of ON
Specifies attributes to match on equality 
Attribute must exist in both tables
Can be used for multiple attributes
Like Natural Join the result won't contain duplicate column names