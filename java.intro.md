## Java crash course

### History
Java was originally developed by Sun Microsystems by the name of Oak, and was made to create an environment for embedded systems, which is what Sun Microsystems mainly makes today.
 - Java was designed to be:
  - Simple
  - Object-oriented
  - Distributed
  - Multi-threaded
  - Platfor neutral
  - Robust
  - Secure
  - Scaleable


And many other buzzwords.

### The virtual machine
Java is both compiled and interpreted. The source code you write is compiled into Java ___bytecode___, which is then intreperted by the ___Java Virtual Machine___, which means that the bytecode is machine code for the JVM. Because Java is compiled __and__ interpreted separately, compiled Java bytecode can be run on any JVM, regardless of platform.

Networking and Distribution are also built into the core of java, so you don't have to add them in as API's. This makes Java adept at creating networked applications, and server side components.

### The JVM and you
The JVM has plenty of features to help you out:
- Java manages your memory for you, so you don't have to worry about it!
  - But this also means that you can't control the allocation of memory :(
  - But also makes the application use less memory by managing it well
- The JVM also has a ___Just In Time Compiler___, which optimizes running code to improve performance.

### Object-Oriented Programming
Java is an object oriented programming language, so understanding how object oriented languages is important to understanding Java. OOP has several concepts that are used in Java:

- Abstract Types (or classes)
- Encapsulation (to hide information)
- Aggregation
- Inheritance
- Polymorphism

#### What is object oriented programming?
OOP is modeling real-world objects in software, which makes it a lot easier to structure and understand your code. It also groups things so that it is easier to maintain and use them. We usually structure object oriented programs by creating a series of functions, and then creating a data structure for those functions to manipulate. 
