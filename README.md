# System-Design-Must-know-Concepts.
Collection of some broad system design concepts, I update whenever I read some new concepts.


### Database

* Lost Update
* ACID property of relational DB
* Why isolation?
    * Dirty Read - A Dirty read is the situation when a transaction reads a data that has not yet been committed. 
    * Non Repeatable read - Non Repeatable read occurs when a transaction reads same row twice, and get a different value each time.
    * Phantom Read - Phantom Read occurs when two same queries are executed, but the rows retrieved by the two, are different.
* Isolation levels of databases (Isolation guarantees increases in below order, but at the same time system becomes slower and slower), these are different levels your 
    * Read Uncommitted 
    * Read Committed 
    * Snapshot
    * Serializable.
Slower -> means utilization of your rest.

* Transaction states in DB

