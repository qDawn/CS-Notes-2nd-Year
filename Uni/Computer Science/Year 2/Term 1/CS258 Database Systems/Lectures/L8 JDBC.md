
## DB's with Programming

Many languages can implement DB's. It acts as a host language then the data sub-language would be SQL. Java, Python, Node.js, C... and so on.

## Ways of Accessing Databases

- Interactively
	- Typing SQL commands in a window 
- File / batch
	- Prepare a file consisting of SQL commands
	- At command line type \i <filename_> or @<filename_>
- Application programs
	- Carefully developed programs that use commands to access the DB

## Interfaces to Databases

Embedding SQL commands in an application program

Using a library of DB functions / classes
- Application program makes call to functions and methods e.g:
	- Managing connection to DB
	- Preparing / executing queries
	- receive result, process result tuples, etc..

In the most abstract way, there is the client which has a query and is using a program to interact with a network which talks to the DB server.

![[Pasted image 20261020192448.png]]

Many Clients can interact with this network.

## Client Server Model

Database runs as a server (postgres for this module)
- Listens on a specific port

SQL Programmer uses client software (psql)
- Client connects to port to communicate with the server

Application programs communicate with server over network in the same way as any other client
- We can write Java applications to interact with such DB

## The "Impedance Mismatch" problem

The idea that blending two paradigms together, in this case Java and SQL

Programming models and structures differ:
- Data types in SQL vs Java
Structures to handle query results
- SQL query results are (multi)sets or tuples
- Needs to be converted to Java class where tuples can be accessed
	- Looping over query result with host language constructs
	- Cursor or iterator var.

## DB Programming with SQL

- Java Database Connectivity (JDBC)
	- An API that calls SQL commands from Java
	- Implemented as a Driver for a particular DBMS with methods,objects and classes
- One Java program can have connections to multiple databases
	- Different data sources
	- Maybe different DBMSs (with different drivers)

## JDBC Drivers

The driver manager class is used to handle multiple connections to different DBs
- i.e managing drivers and mapping clients to the correct drivers
- Methods include: getDriver, registerDriver, deregisterDriver

Driver directly translates JDBC calls to the DBMSs protocol and communicates with the DB server through TCP
- Known as a 'Type 4' driver, previous approaches used native libraries on the client side

## JDBC: Main Classes/ Tasks

- Connection Class
	- Connection object needed per DB connection
	- Created using driverManager's getConnection()
	- Has functions to connected to specific DB sources
		- Using URLs
		- It also provides auth to DBMS's
- Statement Class, two sub classes:
	- PreparedStatement and CallableStatement
	- Methods to execute a SQL command
	- Need a statement object per query / update you wish to issue
- ResultSet Class 
	- Query results are returned into objects of this type

Rest is Covered in lab sheets. 