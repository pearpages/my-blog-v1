+ Learn to read the code 
+ Mind your dependencies
+ Sharpen your Environment Ax

### Why Test?

Because writing the test is easier then running the application.

**Testing is not like frosting**
The only way to make sure your test code is testable is to write the tests from the very beginning.

### Excuses

The only right one is: **"I DON'T KNOW HOW"**.

We have problems admitting we have problems writing tests. Of course it's going to be hard to write tests.

It's skill like any other skill, it needs practice. How to struture the code to make it testable.

### Write Tests First

Software Engineers
QA
Test Engineers

*The cake has alreaby been baked*. That's the main reason why tests do not work.

**How would you write HARD TO TEST code?**
Global State code! Because it is hard to control.

The tests have to be EASY to read. 

The difficulty of **the TEST it's about the STRUCTURE of the code. Not what the CODE does**.

**Some of the worst case scenarios**
+ Global State aka Singleton
+ Law of Demeter Violation
+ Global reference to time
+ Hard-coded new Operator
+ Lack of Dependency Injection

#### Real Issues

+ Mixing new with logic
+ Looking for things
+ Work in constructor
+ Global state
+ Singletons
+ Static methods
+ Deep inheritance
+ Too many conditionals
+ Mixing Service/Value
+ Mixing Concerns

**Dependency Injection!!**
What are the fundamentals items you need to make your job done.

### Testable Code

+ Good OO
+ Dependency Injection
+ Test Driven Development
+ A whole lot about un-testable code

**There is no secret to writing tests... there are only secrets to writing testable code!**

### Tests

+ Scenario Tests
+ Functional Tests
+ **Unit Tests**

70 : 20 : 10

Tests should be run on every save.

### Unit Testing a Class

Control the dependencies. I am not going to look beyond the class I am testing.

No Global Objects, only objects being past in.

**Friendly (the dependency) does not have to be a mock**

### Glossary

Perforce
CL = Changeless