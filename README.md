# System-Design-And-Clean-Code-Concepts
Collection of some broad system design and clean coding concepts to adhere for becoming a better software engineer.
Improving one day at a time.

Open to collaborate, kindly make a pull request if you found anything wrong.

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
* **Single responsibility principle** - Each class must should be responsible for only single task, like let’s say we have a Class

```swift

class CurrencyConverter { 
   func fetchRates(sourceCurrency:String, requiredCurrency:String, completionBlock:@escaping (Double, Error?)->Void) {}
   func save(rate:Double, souceCurrency:String, targetCurrency:String) throws {}
   func convert(amount:Double, sourceCurrency:String, targetCurrency:String) -> Double {}
}

``` 

So to make this class to follow single responsibility principle, it should be splitted  to multiple classes like :-

```swift

class CurrencyConverter { 
   func convert(amount:Double, sourceCurrency:String, targetCurrency:String) -> Double {}
}

class WebService { 
   func fetchRates(sourceCurrency:String, requiredCurrency:String, completionBlock:@escaping (Double, Error?)->Void) {}
} 

class LocalPersistence { 
   func save<T>(key:T) 
}

```

So that each class is responsible for doing a single task.
   
* **Open closed principle** - 
  * Entities should be open for extension but closed for modification.
  * Add new behavior without modifying existing code.
  * Relies on object oriented concepts like inheritance, composition and polymorphism.
  
* **Liskov Substitution Principle** - Ability to replace references to base classes with objects of derived classes.
* **Interface segregation principle**  - 
  * Deals with the problem of fat interface.
  * Clients shouldn’t depend upon the interfaces they don’t use.
  
* **Dependency Inversion Principle** - 
  * Deals with reusability.
  * Avoids high-level -> low-level module dependency,  our high level classes should depend on low level abstractions.
  * Modules should depend on abstractions.
  * Abstractions should not depend on details, but details should depends on abstraction.
  
This Persistence class below is tightly coupled with the logger class. So that if anything changes in the Logger class then the persistence class will also needs to be changed.

```swift
class Persistence {
    private var logger:Logger = Logger()
    
    func save(data: Data, to url: URL) throws {
        do {
            try data.write(to: url)
        }catch {
            logger.log("\(error)", severity: 10)
        }
    }
}
class Logger {
    func log(_ message: String, severity: Int) {
        print("error: \(message)")
    }
}
```

We can remove this tight coupling by having this logging functionality exposed via an interface/protocol so that the only logger class is being affected.

```swift
protocol Logging {
    func log(_ message: String, severity: Int)
}
class Persistence {
    private var logger:Logging!
    
    init(logger: Logging) {
        self.logger = logger
    }
    
    func save(data: Data, to url: URL) throws {
        do {
            try data.write(to: url)
        }catch {
            logger.log("\(error)", severity: 10)
        }
    }
}
class Logger: Logging {
    func log(_ message: String, severity: Int) {
        print("error: \(message) - severity: \(severity)")
    }
}
```



