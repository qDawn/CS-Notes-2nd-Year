
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

- Client applications use Application Program Interface (API) to access server databases via standard interface such as:
	- JDBC: for Java programming access
	- Embedded SQL for C programmic access
- A client program may connect to (the servers of) several DBMSs, sometimes called the data sources
- DB servers provide database (Data Definition and Data Manipulation) services to (potentially different types of) clients

## The Three Tier Architecture for DB Programming 

Between the client and the DB server there is some DB application
![[Pasted image 20261113191324.png]]
e.g Ordering product
- Click browser, converts to action
- Sends request to server, converts to DB logic
- Updates DB


## Separating Application / Business logic from DB

- Good to separate the applicatoin logic from the DB
	- Security purposes:
		- End user interacting with our application rather than directly with DB 
		- Server is only accessible from the middle tier
			- End users can't directly interact with DB 
	- Client is just a web browser connected to web server
- But, good reasons to embed application logic inside DB server
	- Write the application logic in functions/procedures

## Persistent Stored Modules

Persistent Stored Modules
- Stored Procedures/Functions/Triggers
- Logic that is used by multiple clients
	- Keep constraints and business rules on the server
	- Independent of any client application
	- Don't need to keep programmign rules in different clients
- Can be more efficient - send parameters direct to DB server rather than calculating lots of different values and then sending
- Can use procedures to express more complex data models than constraints

## Database Programming Languages

- Declaring and calling stored procedures


























