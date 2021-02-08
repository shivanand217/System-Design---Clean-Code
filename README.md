# System-Design-And-Clean-Code-Concepts
Collection of some broad system design and clean coding concepts to adhere for becoming a better software engineer.
Improving one day at a time.

### Databases.

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
    
    ##### Good Read for isolation
    (http://highscalability.com/blog/2011/2/10/database-isolation-levels-and-their-effects-on-performance-a.html)

* Transaction states in DB

### Clean Code Principles.

Signs of bad code design:
* Rigidity
    * Cascading code changes(Change in one part of the code, requires some other part to be modified).
* Fragility
    * Fixing one problem breaks something else.
* Immobility
    * Hard to reuse some part of the code due to tight coupling.
    
Good Design (SOLID):
* Single responsibility principle - Each class must should be responsible for only single task, like let’s say we have a ``class CurrencyConverter { func fetchRates(), func save(), func convert() )``. So to make this class to take responsibility of only one thing, it should be splitted  to multiple classes like class CurrencyConverter { func convert() }, class WebService { func fetchRates() } and class LocalPersistence { func save<T>(key:T) }. So that each class is responsible for doing a separate task.
   
* Open closed principle - 
  * Entities should be open for extension but closed for modification.
  * Add new behavior without modifying existing code.
  * Relies on object oriented concepts like inheritance, composition and polymorphism.
  
* Liskov Substitution Principle - Ability to replace references to base classes with objects of derived classes.
* Interface segregation principle  - 
  * Deals with the problem of fat interface.
  * Clients shouldn’t depend upon the interfaces they don’t use.


