
# Set Comparisons 

Can apply principles similar to IN for other comparisons across sets
Apply (operation) against values in subquery. 

Keywords:
- ALL = True for all comparisons
- ANY / SOME = True for at least one comparison

Remember scalar subqueries 
``` SQL
SELECT <attList> FROM <tableList>
WHERE <attName/attTuple> <OP> ALL/ANY <subQuery>
```

![[Pasted image 20261029010407.png]]

## Correlated Subqueries

So far, the subqueries have been independent of the outer query. The subqueries are evaluated once then the results are used in the outer query.

Often a nested query refers to attributes of tuples in the relations of the outer query, the nested query need to be evaluated per tuple of the outer query.

# Exists Operator

- Allows us to conduct emptiness testing
- Presence of any value evaluates to TRUE
- NULL will make it evaluate to TRUE aswell

![[Pasted image 20261029011017.png]]

## Non-Emptiness and Scope

The example above showed:
- Inner query referred to an attribute from the outer query
- These queries are correlated
- The nested inner query is evaluated once per tuple in the outer query
- Scope principles apply to the nested queries, E can be skipped
- EXISTS can be used to test for emptiness

![[Pasted image 20261029012229.png]]

## Correlated Subqueries vs Subqueries

Normally, a subquery can be evaluated first (independently of the outer query). With correlated subqueries this is not possible because the evaluation depends on the values from the outer query.

# INSERTion by Query 

You can INSERT INTO tables with the same principles 
``` SQL 
CREATE TABLE example(source1 INT PRIMARY KEY, source2 INT);
INSERT INTO example VALUES (1,2),(3,4),(8,10);
CREATE TABLE example2(copy1 INT PRIMARY KEY, copy2 INT);
INSERT INTO example2 SELECT source1, source2
FROM example WHERE source1 > 2;
```

# Set Operators and Subqueries

You can view queries as results that can use set operators, the following syntax for this is:
- (subquery1) UNION (subquery2)
- (subquery1) INTERSECT (subquery2)
- (subquery1) EXCEPT (subquery2)

These work exactly how you think they work, set semantics.

# Controlling Set vs Bag Semantics

Force results to be a set with 
``` SQL
SELECT DISTINCT ...
```

Force results to be a bag with 
``` SQL 
UNION ALL 
EXCEPT ALL
INTERSECT ALL
```
![[Pasted image 20261029014335.png]]