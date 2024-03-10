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
## method reference operator / Double colon (::) operator
The double colon (::) operator, also known as method reference operator in Java, is used to call a method by referring to it with the help of its class directly. They behave exactly as the lambda expressions. The only difference it has from lambda expressions is that this uses direct reference to the method by name instead of providing a delegate to the method
```
<Class name>::<method name>
```

## Abstract Classes
- We define an abstract class with the abstract modifier preceding the class keyword
- An abstract class can be subclassed, but it can’t be instantiated
- If a class defines one or more abstract methods, then the class itself must be declared abstract
- An abstract class can declare both abstract and concrete methods
- A subclass derived from an abstract class must either implement all the base class’s abstract methods or be abstract itself## Abstract Classes

### Difference between Abstract Class and Interface in Java
Abstract class and interface are both used to define contracts in object-oriented programming, but there are some key differences between them. [Difference between abstract class and interface](https://www.geeksforgeeks.org/difference-between-abstract-class-and-interface-in-java/)

- Type of methods: Interface can have only abstract methods. Whereas, an abstract class can have abstract method and concrete methods. From Java 8, it can have default- and static methods also. From Java 9, it can have private concrete methods as well. 
- Final Variables: Variables declared in a Java interface are by default final. An abstract class can contain non-final variables.
- Type of variables: Abstract class can have final, non-final, static and non-static variables. The interface has only static and final variables.
- Implementation: Abstract class can provide the implementation of the interface. Interface can’t provide the implementation of an abstract class.
- Inheritance vs Abstraction: A Java interface can be implemented using the keyword “implements” and an abstract class can be extended using the keyword “extends”.
- Multiple implementations: An interface can extend one or more Java interfaces; an abstract class can extend another Java class and implement multiple Java interfaces.
- Multiple Inheritance:  Multiple inheritance can be partially achieved by the use of interfaces , whereas the same can’t be done by the use of abstract classes. Because in Java, one class can implement multiple Interfaces, but one class cannot extend from multiple other classes because that’s just not possible in java as that would lead to the diamond problem. 
- Accessibility of Data Members: Members(variables) of a Java interface are final by default. A Java abstract class can have class members like private, protected, etc.

| Definition | An abstract class is a class that cannot be instantiated and can contain both abstract and non-abstract methods. An interface, on the other hand, is a contract that specifies a set of methods that a class must implement. |
| --- | --- |

| Inheritance | A class can inherit from only one abstract class, but it can implement multiple interfaces. This is because an abstract class represents a type of object, while an interface represents a set of behaviors. |
| --- | --- |

## Concrete methods
Concrete methods are those methods which has their complete definition but they can also be overriden in the inherited class. However, if we make the concrete method as “FINAL” it cannot be overrided in the inherited class because declaring a method as final means  – its implementation is complete.

## Abstract methods
Abstract methods are those types of methods that don’t require implementation for its declaration. These methods don’t have a body which means no implementation. A few properties of an abstract method are:
- An abstract method in Java is declared through the keyword “abstract”.
- While the declaration of the abstract method, the abstract keyword has to be placed before the name of the method.
- There is no body in an abstract method, only the signature of the method is present. 
- An abstract method in Java doesn’t have curly braces, but the end of the method will have a semicolon (;)

### Abstract method in an abstract clas
```
//abstract class
abstract class Sum{
   /* These two are abstract methods, the child class
    * must implement these methods
    */
   public abstract int sumOfTwo(int n1, int n2);
   public abstract int sumOfThree(int n1, int n2, int n3);
	
   //Regular method 
   public void disp(){
	System.out.println("Method of class Sum");
   }
}
//Regular class extends abstract class
class Demo extends Sum{

   /* If I don't provide the implementation of these two methods, the
    * program will throw compilation error.
    */
   public int sumOfTwo(int num1, int num2){
	return num1+num2;
   }
   public int sumOfThree(int num1, int num2, int num3){
	return num1+num2+num3;
   }
   public static void main(String args[]){
	Sum obj = new Demo();
	System.out.println(obj.sumOfTwo(3, 7));
	System.out.println(obj.sumOfThree(4, 3, 19));
	obj.disp();
   }
}
```
Output:
```
10
26
Method of class Sum
```


### Abstract method in interface
```
//Interface
interface Multiply{
   //abstract methods
   public abstract int multiplyTwo(int n1, int n2);
   
   /* We need not to mention public and abstract in interface
    * as all the methods in interface are 
    * public and abstract by default so the compiler will
    * treat this as 
    * public abstract multiplyThree(int n1, int n2, int n3);
    */
   int multiplyThree(int n1, int n2, int n3);

   /* Regular (or concrete) methods are not allowed in an interface
    * so if I uncomment this method, you will get compilation error
    * public void disp(){
    *    System.out.println("I will give error if u uncomment me");
    * }
    */
}

class Demo implements Multiply{
   public int multiplyTwo(int num1, int num2){
      return num1*num2;
   }
   public int multiplyThree(int num1, int num2, int num3){
      return num1*num2*num3;
   }
   public static void main(String args[]){
      Multiply obj = new Demo();
      System.out.println(obj.multiplyTwo(3, 7));
      System.out.println(obj.multiplyThree(1, 9, 0));
   }
}
```
Output:
```
21
0
```





# Java Lambda Expression
## Functional Interfaces
```
parameter -> expression
(parameter1, parameter2) -> expression
(parameter1, parameter2) -> { code block }

```
# Functional Interfaces
In Java, a functional interface is an interface that contains only one abstract method. It acts as a blueprint for a lambda expression or a method reference. The single abstract method represents a single unit of computation, making it ideal for functional programming paradigms. But what exactly is functional programming.
``` 
public interface Drawable {
    void draw(int width);
}

@SpringBootApplication
public class LambdaDemo {

	public static void main(String[] args) {
            SpringApplication.run(LambdaDemo.class, args);
	}

	public CommandLineRunner commandLineRunner(String[] args) {
	    // without lambda, Drawable implementation using anonymous class  
            Drawable d = new Drawable() {
                @Override
                public void draw(int width) {
                    System.out.println("Drawing "+width);
                }
            };
            d.draw(10);

	    // with lambda  
            DrawableLambda dLambda = (width) -> System.out.println("Drawing "+ width);
            dLambda.draw(11);
        }
}

``` 







