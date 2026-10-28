
## Sub queries / Nested queries

A parenthesised SELECT-FROM_WHERE statement can be used as a value at
- the FROM (to select results from a subquery)
- the WHERE (to compare rows with values from a subquery)

Instead of naming a table in the FROM clause, provide a subquery instead
- This nested query will return a new table, call it tempTable
- So the above is equivalent to having created a table, using its name, tempTable in the FROM clause
- Useful to use a tuple-variable to name tuples of the result of the nested query
![[Pasted image 20261028234727.png]]