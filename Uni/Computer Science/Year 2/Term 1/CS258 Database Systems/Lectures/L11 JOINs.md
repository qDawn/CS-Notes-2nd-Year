
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