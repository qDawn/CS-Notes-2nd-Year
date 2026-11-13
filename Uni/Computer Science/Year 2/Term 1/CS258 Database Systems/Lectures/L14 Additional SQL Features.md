
## Outline:

- Window functions
- Time/ Date conversions
- Procedural


## Converting Times to INTEGERs

Timestamp contains multiple components that can be extracted

In where now() gives 
e.g 
year FROM now() - the year your are currently in
epoch FROM now() - the time you are currently in


``` SQL
SELECT CAST(extract(epoch from now()) AS INTEGER);
```

This command performs the same thing as epoch from now() however it strips away the decimal places by converting it into an Integer.

## Window Functions

- Window functions calculate over a set of related rows
- These are partitioned over a particular window (group)

![[Pasted image 20261113011342.png]]

![[Pasted image 20261113012307.png]]

- It can also refer to the previous row with LAG
- And the next row tihe LEAD
![[Pasted image 20261113012518.png]]

## Two Tier Architecture

![[Pasted image 20261113012640.png]]

Multiple clients, using different software, connected to (and sharing) many databases

## For DB Programming

- Client applications use 