
## Analytical Queries

E.g :
- SUM
- AVG
- COUNT
- MIN
- MAX

Apply to a column in a SELECT to produce that aggregation 

COUNT(\*) counts the number of tubles
COUNT DISTINCT coutns the number of tuples after removing duplicates

## Aggregate Functions

![[Pasted image 20261031013132.png]]

## NULL

Null will never contribute to a sum,average or count and cannot be the minimum or maximum.
If all values are NULL, then Count will be 0 and the rest will be NULL.

## Group Aggregations with GROUP BY

We can add GROUP BY (attribute) to a query
The result is grouped according to the values of the "groupy by" attributes
Any aggregation is applied only within each

``` SQL
SELECT <attNameGroup>, agg_func1(<attName>) ... FROM <tableList>
GROUP BY <attNameGroup>
```

If attNameGroup is NULL it counts as a distinct group
![[Pasted image 20261031014057.png]]

![[Pasted image 20261031014126.png]]

## Filtering Groups

WHERE clauses are applied before aggregation
HAVING (condition) can be added after the GROUP BY
If so, the condition applies to each group 

![[Pasted image 20261031021613.png]]