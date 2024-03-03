# SpringBoot
Spring Boot makes it easy to create stand-alone, production-grade Spring based Applications that you can "just run".  We take an opinionated view of the Spring platform and third-party libraries so you can get started with minimum fuss. Most Spring Boot applications need minimal Spring configuration.

### Features
- Create stand-alone Spring applications
- Embed Tomcat, Jetty or Undertow directly (no need to deploy WAR files)
- Provide opinionated 'starter' dependencies to simplify your build configuration
- Automatically configure Spring and 3rd party libraries whenever possible
- Provide production-ready features such as metrics, health checks, and externalized configuration
- Absolutely no code generation and no requirement for XML configuration
- Help to resolve dependency conflicts (Maven or Gradle)

## Spring Initializer
[Spring Initializer](http://start.spring.io)












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

## Java Bean Spezification
- A curated list of Maven dependencies
- A collection of dependencies grouped together
- Tested and verified by the Spring Development team
- Makes it much easier for the developer to get started with Spring
- Reduces the amount of Maven configuration


