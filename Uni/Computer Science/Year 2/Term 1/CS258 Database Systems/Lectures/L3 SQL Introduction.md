
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

## Mutli - Select 

![[Pasted image 20261008233125.png]]

In the example above, price is selected to be changed to the priceIn$ so when fetching the price it will automatically convert. 

## Constant Expressions 

![[Pasted image 20261008233848.png]]

need to look into this

## Conditions in WHERE clauses

Conditions in WHERE can use AND OR NOT and parentheses in the usual way 
e.g 
![[Pasted image 20261008234539.png]]

## Strings in WHERE

Must use LIKE before 
![[Pasted image 20261008235117.png]]

% is zero or more characters
and _ represents exactly one character 


## NULL Values

NULL's are not real values and can mean :
- Unknown
- Unavailable
- Inapplicable

Each NULL value is considered different from another NULL value.

for logic involving NULL SQL uses TRUE, FALSE and UNKNOWN.

for truth tables, if it depends on the value of unknown then the output is unknown.

to query NULL use (IS NULL) or (IS NOT NULL)