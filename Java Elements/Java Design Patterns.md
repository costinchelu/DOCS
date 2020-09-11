## Design Patterns

In software engineering, a design pattern is a general repeatable solution to a commonly occurring problem in software design. A design pattern isn't a finished design that can be transformed directly into code. It is a description or template for how to solve a problem that can be used in many different situations.

**CREATIONAL** design patterns are all about class instantiation. This pattern can be further divided into class-creation patterns and object-creational patterns. While class-creation patterns use inheritance effectively in the instantiation process, object-creation patterns use delegation effectively to get the job done.

**Abstract Factory**
Creates an instance of several families of classes  
**Builder**
Separates object construction from its representation  
**Factory Method**
Creates an instance of several derived classes  
**Object Pool**
Avoid expensive acquisition and release of resources by recycling objects that are no longer in use  
**Prototype**
A fully initialized instance to be copied or cloned  
**Singleton**
A class of which only a single instance can exist  

**STRUCTURAL** design patterns are all about Class and Object composition. Structural class-creation patterns use inheritance to compose interfaces. Structural object-patterns define ways to compose objects to obtain new functionality.

**Adapter**
Match interfaces of different classes  
**Bridge**
Separates an object’s interface from its implementation  
**Composite**
A tree structure of simple and composite objects  
**Decorator**
Add responsibilities to objects dynamically  
**Facade**
A single class that represents an entire subsystem  
**Flyweight**
A fine-grained instance used for efficient sharing  
**Private Class Data**
Restricts accessor/mutator access  
**Proxy**
An object representing another object  

**BEHAVIORAL** design patterns are all about Class's objects communication. Behavioral patterns are those patterns that are most specifically concerned with communication between objects.

**Chain of responsibility**
A way of passing a request between a chain of objects  
**Command**
Encapsulate a command request as an object  
**Interpreter**
A way to include language elements in a program  
**Iterator**
Sequentially access the elements of a collection  
**Mediator**
Defines simplified communication between classes  
**Memento**
Capture and restore an object's internal state  
**Null Object**
Designed to act as a default value of an object  
**Observer**
A way of notifying change to a number of classes  
**State**
Alter an object's behavior when its state changes  
**Strategy**
Encapsulates an algorithm inside a class  
**Template method**
Defer the exact steps of an algorithm to a subclass  
**Visitor**
Defines a new operation to a class without change  


## What major patterns do the Java APIs utilize? Where exactly?

Design patterns are used and supported extensively throughout the Java APIs. Here are some examples:

- The **Model-View-Controller** design pattern is used extensively throughout the Swing API.
- The getInstance() method in java.util.Calendar is an example of a simple form of the **Factory Method** design pattern.
- The classes java.lang.System and java.sql.DriverManager are examples of the **Singleton pattern**, although they are not implemented using the approach recommended in the GoF book but with static methods.
- The **Prototype pattern** is supported in Java through the clone() method defined in class Object and the use of java.lang.Cloneable interface to grant permission for cloning.
- The Java Swing classes support the **Command pattern** by providing an Action interface and an AbstractAction class.
- The Java 1.1 event model is based on the **Observer pattern**. In addition, the interface java.util.Observable and the class java.util.Observer provide support for this pattern.
- The **Adapter pattern** is used extensively by the adapter classes in java.awt.event.
- The **Proxy pattern** is used extensively in the implementation of Java's Remote Method Invocation (RMI) and Interface Definition Language (IDL) features.
- The structure of Component and Container classes in java.awt provide a good example of the **Composite pattern**.
- The **Bridge pattern** can be found in the separation of the components in java.awt (e.g., Button and List), and their counterparts in java.awt.peer.