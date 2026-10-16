
SQL is a Data Manipulation Language(DML)
- Querying and Updates
A modification command is NOT a query 
- Doesn't return anything, changes the DB

3 Kinds of modification:
- Insert tuples
- Delete tuples
- Update values of existing tuples

# Insertion 

``` SQL
INSERT INTO <table> VALUES (<val_1>,<val_2>,...,<val_n>)
```
Each value belongs to the attribute in the corresponding position of the schema

Can specify the attribute order through writing the attribute names after the table name. 

``` SQL
INSERT INTO <table> (catergory, price) VALUES (<val_1>,<val_2>,...,<val_n>)
```

No output message, though you can get error lines or lines affected

## Inserting Partial Records
``` SQL
INSERT INTO <table> (<A_1>, <A_2>, ..., <A_n>) VALUES (<val_1>, <val_2>, ..., <val_n>)
```

Values not assigned get set to their default or given NULL if no default defined

# Deletion

``` SQL
DELETE FROM <table> WHERE <expression>
```

When condition is True, all tuples satisfying the expression is deleted

Might be prevented by referential integrity checks

``` SQL
DELETE FROM Products
```
would delete all rows, same as saying WHERE True at the end.

Key thing to note it doesn't delete the table it deletes all the tuples, schema kept intact.

## Complex Deletes

``` SQL
DELETE FROM Products p
WHERE EXISTS(SELECT product_name FROM Products WHERE
category = p.category AND product_name <> p.product_name);
```

This will delete all duplicates leaving the unique category products behind.

# Updating DB Tuple(s)

``` SQL
UPDATE <table>
SET <list of (attribute assignment) pairs>
WHERE <condition on tuples>
```

e.g 

``` SQL
UPDATE products 
SET unit_price = 2.20
WHERE product_name = 'Bread';
```

Can use set to NULL, Default and use arithmetic expressions and function to update values.