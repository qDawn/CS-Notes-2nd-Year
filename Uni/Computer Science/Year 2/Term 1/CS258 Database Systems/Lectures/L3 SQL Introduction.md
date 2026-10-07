
## Basic Retrieval Queries

SELECT <att.> FROM <table.> WHERE <condition.>

SELECT - FROM - WHERE 
- returns a set of tuples 
- <att.> 
	- attributes of tuples to be retrieved (column)
- <table.> 
	- table where attributes are found
- <condition.>
	- only return tuples with attribute values satisfying condition

## Example 

![[Pasted image 20261006234027.png]]

SELECT DISTINCT price 
FROM Products

Returns unique prices

![[Pasted image 20261006234150.png]]

![[Pasted image 20261006234240.png]]

If multiple tables have the same attribute names you can use AS (nickname) to selectively choose from tables 

## More SQL

## <b> SQL is case insensitive (FROM = from) except for inside strings</b>

![[Pasted image 20261006235524.png]]

single quotes for strings as double quotes are used for columns

## Wildcards 

![[Pasted image 20261007013241.png]]

Sorting attributes through ORDER BY <attr.> (ASC | DESC)