# Java Bean
A Java Bean is a reusable software component in Java. It is a class that encapsulates many objects into a single object (the bean), and can be instantiated the same way as a normal Java class, public class MyBean { //getters, setters, and methods for the class}. It’s a way to create reusable components for your Java applications.

| definition - a Java bean is a serializable POJO (plain old Java object), with a no-argument constructor and private fields with getters/setters | 
| --- | 

## Java Bean Spezification
Individual Java Beans will vary in the functionality they support, but the typical unifying features that distinguish a Java Bean are:
- Support for “introspection” so that a builder tool can analyze how a bean works
- Support for “customization” so that when using an application builder a user can customize the appearance and behaviour of a bean.
- Support for “events” as a simple communication metaphor than can be used to connect up beans.
- Support for “properties”, both for customization and for programmatic use.
- Support for persistence, so that a bean can be customized in an application builder and then have its customized state saved away and reloaded later.
- All beans must support either Serialization or Externalization.
[Javabeans specification](http://java.sun.com/javase/technologies/desktop/javabeans/docs/spec.html)


## Creating a Java Bean
To create a Java Bean, you need to follow some rules. A Java Bean is a class that:

- All beans must implement either Serialization or Externalization interface
- Has a public no-argument constructor.
- Provides methods to set and get the values of properties (known as setter and getter methods).

```
import java.io.Serializable;

public class StudentBean implements Serializable {
    private String name;
    private int age;

    public StudentBean() {
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }
```
## Java Beans in JSPs and Servlets

Java Beans can be used effectively in JSPs (JavaServer Pages) and Servlets, two key technologies in the world of Java web applications. They can be used to encapsulate data that can be reused across multiple JSPs or Servlets.

## Exploring Alternatives: POJOs and EJBs
Java offers other concepts that can be used as alternatives to Java Beans, such as POJOs (Plain Old Java Objects) and EJBs (Enterprise JavaBeans). These concepts offer more flexibility and functionality, making them suitable for more complex applications.

### Plain Old Java Objects (POJOs)
A POJO is a simple Java object that doesn’t extend or implement some specialized classes or interfaces in the Java framework. Here’s an example of a POJO:

### Enterprise JavaBeans (EJBs)
EJBs are a part of the Java EE (Enterprise Edition) framework and provide a robust architecture for building large-scale, distributed applications.
```
import javax.ejb.Stateless;

@Stateless
public class StudentEJB {
    public String getStudentDetails() {
        return "John Doe, 22";
    }
```
StudentEJB is a stateless session EJB. It provides a method getStudentDetails() that returns a string. EJBs offer advanced features such as transaction management and security, but they are more complex and heavier than Java Beans and POJOs.

When deciding which concept to use, consider the complexity of your application, the features you need, and the resources you have. Java Beans are great for simple, small-scale applications, while POJOs offer more flexibility and EJBs are suitable for large-scale, enterprise applications.

# Java Conceps
## Abstract Classes
- We define an abstract class with the abstract modifier preceding the class keyword
- An abstract class can be subclassed, but it can’t be instantiated
- If a class defines one or more abstract methods, then the class itself must be declared abstract
- An abstract class can declare both abstract and concrete methods
- A subclass derived from an abstract class must either implement all the base class’s abstract methods or be abstract itself## Abstract Classes
### Difference between Abstract Class and Interface in Java
Abstract class and interface are both used to define contracts in object-oriented programming, but there are some key differences between them. [Difference between abstract class and interface](https://www.geeksforgeeks.org/difference-between-abstract-class-and-interface-in-java/)

| --- | --- |
| Definition | An abstract class is a class that cannot be instantiated and can contain both abstract and non-abstract methods. An interface, on the other hand, is a contract that specifies a set of methods that a class must implement. |
| Inheritance | A class can inherit from only one abstract class, but it can implement multiple interfaces. This is because an abstract class represents a type of object, while an interface represents a set of behaviors. |
| --- | --- |

# Java Lambda Expression
## Functional Interfaces
```
parameter -> expression
(parameter1, parameter2) -> expression
(parameter1, parameter2) -> { code block }

```
# Functional Interfaces
It’s recommended that all functional interfaces have an informative @FunctionalInterface annotation. This clearly communicates the purpose of the interface, and also allows a compiler to generate an error if the annotated interface does not satisfy the conditions. Any interface with a SAM(Single Abstract Method) is a functional interface, and its implementation may be treated as lambda expressions. [Documentation: functional interfaces](https://www.baeldung.com/java-8-functional-interfaces).





