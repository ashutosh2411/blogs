# Database Systems
## Introduction
Welcome to the course! I am Ashutosh Upadhye, 
and we would be learning about databases and 
the use of database management systems, primarily
from the viewpoint of the designer,
user and developer of database applications.
## What is a DBMS? 
I'm going to start by describing in
one very long sentence what
a database management system provides for applications.
It provides a means of handling large amounts
of data primarily, but let's looks at a little more detail.
What it provides, is efficient, reliable,
convenient and safe multi-user
storage of and access to
massive amounts of persistent data. 

The data in databases must not get lost in case of hardware or software failures, or activities of malicious users. Apart from safety, the database must have a certain amount of concurrency involved, allowing multiple users to access the data base concurrently. 
## Why use a DBMS?
- Data Independence and efficient access.
- Reduced application development time.
- Data integrity and security.
- Uniform data administration.
- Concurrent access, recovery from crashes.
## Why study DBMS? 
- Shifting from computation to information. 
- Datasets are increasing in diversity and volume.
- DBMS encompasses most of the CS.
## Files vs DBMS
- Application must stage large datasets between main memory and secondary storage (e.g., buffering, page-oriented access, 32-bit addressing, etc.)
- Special code for different queries
- Must protect data from inconsistency due to multiple concurrent users
- Crash recovery
- Security and access control
## Key concepts
- Data Model
- Schema vs Data: *Type and Variable.*
- Data Definition Languages *(DDL)*: *for setting up the schema.*
- Data Manipulation Languages *(DML)*: *for querying and modifying.*
## Key people
- DBMS Implementer: *builds the database.*
- Database designer: *establishes the schema.*
- Database application developer: *programs that operate on database.*
- Database administrator: *loads data, ensures smooth run.*

## Data Models
- A **data model** is a collection of concepts for describing data. 
- A **schema** is a description of a particular collection of data, using the given data model. 
- The **relational model of data** is the most widely used model today. 
	- Main concept: *relation*, basically a table with rows and columns. 
	- Every relation has a *schema*, which describes the column or fields. 
- Other than relational model, hierarchal model, network model, object oriented model, object relation model, etc are also popular.
## Levels of Abstractions
- Many *views*, single *conceptual (logical) schema* and *physical schema*.
	- Views describe how user sees data. 
	- Conceptual schema defines logical structure. 
	- Physical schema describes the files and indexes used. 
- Schema are defined using DDL *(Data definition language)* and data is modified using DML *(Data manipulation  language)*.
### Conceptual schema (logical schema)
- Conceptual schema describe the stored data in terms of the data models of the DBMS. 
-In a relational model, logical schema describes all the relationships
- The process of arriving at a good conceptual schema is called conceptual database design. 
### Physical schema
- The physical schema essentially describes how the relations described in conceptual schema are stored on secondary devices such as disks and tapes. 
- The file organization to be used to speed up data retrieval. 
- The process of arriving at a good physical schema is called physical database design. 
### External schema
- External schema allows *and authorizes* an individual or a group of users to access the database. 
- Every database has exactly one conceptual schema and one physical schema, but a database may have several external schema. 
## Advantages of DBMS
### Data Independence
- Due to three levels of data abstraction, the entire DBMS tends to be data independent. Applications won't be affected from how the data is structured or stored. 
- **Logical data independence**: protection from changes in logical structure of data. 
- **Physical data independence**: protection from changes in physical structure of data.
> One of the most important benefits of using DBMS.  
### Concurrency Control
- Concurrent execution of user programs
is essential for good DBMS performance.
	- Because disk accesses are frequent, and relatively
slow, it is important to keep the CPU humming by
working on several user programs concurrently.
- Interleaving actions of different user programs
can lead to inconsistency: e.g., check is cleared
while account balance is being computed.
- DBMS ensures such problems don’t arise: users
can pretend they are using a single-user system.
### Transaction
- Key concept is ***transaction***, which is an *atomic* sequence of database actions (reads/writes).
- Each transaction, executed completely, must
leave the DB in a ***consistent state*** if DB is
consistent, the transaction begins.
	- Users can specify some simple ***integrity constraints*** on the data, and the DBMS will enforce these constraints.
	- Beyond this, the DBMS does not really understand the semantics of the data. (e.g., it does not understand
how the interest on a bank account is computed).
	- Thus, ensuring that a transaction (run alone) preserves consistency is ultimately the user’s responsibility!  
### Scheduling Transactions
- DBMS ensures that execution of {T1, ... , Tn} is
equivalent to some serial execution T1’ ... Tn’.
	- Before reading/writing an object, a transaction requests a lock on the object, and waits till the DBMS gives it the lock. All locks are released at the end of the transaction. *(Strict 2PL locking protocol.)*
	- Idea: If an action of Ti (say, writing X) affects Tj (which perhaps reads X), one of them, say Ti, will obtain the lock on X first and Tj is forced to wait until Ti completes;
this effectively orders the transactions.
	- What if Tj already has a lock on Y and Ti later requests a lock on Y? **(Deadlock!)** Ti or Tj is *aborted* and restarted!
### Ensuring Atomicity
- DBMS ensures Atomicity property. Even if system crashes in middle of a transaction, the previous configuration of DBMS is restored. 
- ***Idea***: Keep a *log* of all actions carried out by the DBMS while executing a set of transactions. 
	- Before a change is made to the database, the
corresponding log entry is forced to a safe location.
(**WAL protocol**; OS support for this is often inadequate.)
	- After a crash, the effects of partially executed
transactions are undone using the log. (Thanks to WAL, if log entry wasn’t saved before the crash, corresponding change was not applied to database!)






> Written with [StackEdit](https://stackedit.io/).
