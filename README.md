# System-Design-Must-know-Concepts.
Collection of some broad system design concepts, I update this content whenever I read any new concepts.


### Databases

* Lost Update
* ACID(Atomicity, Consistency, Isolation, Durability) property of relational DB.
* Why isolation?
    * Dirty Read - A Dirty read is the situation when a transaction reads a data that has not yet been committed. 
    * Non Repeatable read - Non Repeatable read occurs when a transaction reads same row twice, and get a different value each time.
    * Phantom Read - Phantom Read occurs when two same queries are executed, but the rows retrieved by the two, are different.
* Isolation levels of databases (Isolation guarantees increases in below order, but at the same time system becomes slower and slower), these are different levels of sql databases :-
    * Read Uncommitted 
    * Read Committed 
    * Snapshot
    * Serializable. -> Slower.
    
    ```Good Read for isolation
    (http://highscalability.com/blog/2011/2/10/database-isolation-levels-and-their-effects-on-performance-a.html)```

* Transaction states in DB

