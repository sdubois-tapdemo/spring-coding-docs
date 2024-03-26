# Java Data Types
As explained in the previous chapter, a variable in Java must be a specified [Data Types](https://www.w3schools.com/java/java_data_types.asp).

## Primitive Data Types
A primitive data type specifies the size and type of variable values, and it has no additional methods.  There are eight primitive data types in Java:

| Data Type | Size | Description |
| --- | --- | --- |
| byte | 1 byte | Stores whole numbers from -128 to 127 |
| short | 2 bytes | Stores whole numbers from -32,768 to 32,767 |
| int | 4 bytes | Stores whole numbers from -2,147,483,648 to 2,147,483,647 |
| long | 8 bytes | Stores whole numbers from -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807 |
| float | 4 bytes | Stores fractional numbers. Sufficient for storing 6 to 7 decimal digits |
| double | 8 bytes | Stores fractional numbers. Sufficient for storing 15 decimal digits |
| boolean | 1 bit | Stores true or false values |
| char | 2 bytes | Stores a single character/letter or ASCII values |

## Non-Primitive Data Types
Non-primitive data types are called reference types because they refer to objects. The main difference between primitive and non-primitive data types are:
- Primitive types are predefined (already defined) in Java. Non-primitive types are created by the programmer and is not defined by Java (except for String).
- Non-primitive types can be used to call methods to perform certain operations, while primitive types cannot.
- A primitive type has always a value, while non-primitive types can be null.
- A primitive type starts with a lowercase letter, while non-primitive types starts with an uppercase letter.

Examples of non-primitive types are Strings, Arrays, Classes, Interface, etc. 

# Java Conditions
## Java Conditions
- [Java Conditions and If Statements](https://www.w3schools.com/java/java_conditions.asp)
- [Short Hand If...Else](https://www.w3schools.com/java/java_conditions_shorthand.asp)
- [Java Switch Statements](https://www.w3schools.com/java/java_switch.asp)
- [Loops](https://www.w3schools.com/java/java_while_loop.asp)
- [Java For Loop](https://www.w3schools.com/java/java_for_loop.asp)
- [For-Each Loop](https://www.w3schools.com/java/java_foreach_loop.asp)
# Stop / Continue
- [Java Break](https://www.w3schools.com/java/java_break.asp)
## Arrays
- [Java Arrays](https://www.w3schools.com/java/java_arrays.asp)
- [Loop Through an Array](https://www.w3schools.com/java/java_arrays_loop.asp)
- [Multidimensional Arrays](https://www.w3schools.com/java/java_arrays_multi.asp)
## Java Methods
- [Java Methods](https://www.w3schools.com/java/java_methods.asp)
- [Java Method Parameters](https://www.w3schools.com/java/java_methods_param.asp)
- [Java Method Overloading](https://www.w3schools.com/java/java_methods_overloading.asp)
## Java Scope
- [Java Scope](https://www.w3schools.com/java/java_scope.asp)
- [Java Recursion](https://www.w3schools.com/java/java_recursion.asp)
## Java Classes and Objects
- [ava Classes and Objects](https://www.w3schools.com/java/java_classes.asp)
- [Java Class Attributes](https://www.w3schools.com/java/java_class_attributes.asp)
- [Java Class Methods](https://www.w3schools.com/java/java_class_methods.asp)
- [Java Constructors](https://www.w3schools.com/java/java_constructors.asp)
- [Java Inner Classes](https://www.w3schools.com/java/java_inner_classes.asp)
- [Java Polymorphism](https://www.w3schools.com/java/java_polymorphism.asp)
- [Abstract Classes and Methods](https://www.w3schools.com/java/java_abstract.asp)
- [Java Interface](https://www.w3schools.com/java/java_interface.asp)
- [Java Enums](https://www.w3schools.com/java/java_enums.asp)
## Java Modifiers
- [Java Modifiers](https://www.w3schools.com/java/java_modifiers.asp)
## Java Encapsulation
- [Java Encapsulation](https://www.w3schools.com/java/java_encapsulation.asp)
## Java Packages & API
- [Java Packages & API](https://www.w3schools.com/java/java_packages.asp)
## Java Inheritance
- [Java Inheritance](https://www.w3schools.com/java/java_inheritance.asp)

# Java Type Casting
Type casting is when you assign a value of one primitive data type to another type.
In Java, there are two types of casting:

- Widening Casting (automatically) - converting a smaller type to a larger type size (byte -> short -> char -> int -> long -> float -> double)
- Narrowing Casting (manually) - converting a larger type to a smaller size type (double -> float -> long -> int -> char -> short -> byte)

### Widening Casting (automatically)
Widening casting is done automatically when passing a smaller size type to a larger size type:
```
public class Main {
  public static void main(String[] args) {
    int myInt = 9;
    double myDouble = myInt; // Automatic casting: int to double

    System.out.println(myInt);      // Outputs 9
    System.out.println(myDouble);   // Outputs 9.0
  }
```

### Narrowing Casting (manually)
Narrowing casting must be done manually by placing the type in parentheses in front of the value:
```
public class Main {
  public static void main(String[] args) {
    double myDouble = 9.78d;
    int myInt = (int) myDouble; // Manual casting: double to int

    System.out.println(myDouble);   // Outputs 9.78
    System.out.println(myInt);      // Outputs 9
  }
```
# Access Specifier 
In Java, access specifiers are used to defining the visibility and accessibility of class members such as variables, methods, and inner classes. Java has four access specifiers: public, private, protected, and default (also known as package-private). The following table shows the scope of each access specifier in Java:

| Access Specifier | Within Class | Within Package | Outside Package by Subclass only | Outside Package |
| --- | --- | --- | --- | --- |
| Private | Y | N | N | N |
| Default | Y | Y | N | N |
| Protected | Y | Y | Y | N |
| Public | Y | Y | Y | Y |
| Sealed | * | * | * | * |

* Sealing allows classes and interfaces to define their permitted subtypes


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

# Java Generics
A generic type is a generic class or interface that is parameterized over types. The following Box class will be modified to demonstrate the concept.
[The Basics of Java Generics](https://www.baeldung.com/java-generics)
[Java Generics Example Tutorial - Generic Method, Class, Interface](https://www.digitalocean.com/community/tutorials/java-generics-example-method-class-interface)

| E | Element (used extensively by the Java Collections Framework) |
| X | Key |
| N | Number |
| T | Type |
| V | Value |
| S,U,V |  2nd, 3rd, 4th types |
| --- | --- |

```
/**
 * Generic version of the Box class.
 * @param <T> the type of the value being boxed
 */
public class Box<T> {
    // T stands for "Type"
    private T t;

    public void set(T t) { this.t = t; }
    public T get() { return t; }
}
```

## Type Inference
[Type Inference](https://docs.oracle.com/javase/tutorial/java/generics/genTypeInference.html)

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
## ForEach Methode
```
        List<Student> studentList = new ArrayList<Student>();

        studentList.add(new Student("Paul", "Doe", "paul1@luv2code.com"));
        studentList.add(new Student("Paul", "Doe", "paul2@luv2code.com"));
        studentList.add(new Student("Paul", "Doe", "paul3@luv2code.com"));

        studentList.forEach(obj -> studentDAO.save(obj));
```

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
            Drawable d = (width) -> System.out.println("Drawing "+ width);
            d.draw(11);
        }
}

## Generic Functional Interfaces
[Generic Functional Interfaces](https://howtodoinjava.com/java/stream/generic-functional-interfaces/)
```
@FunctionalInterface
public interface ArgumentsProcessor<X>
{
    X process(X arg1, X arg2);
}
```


``` 
// Generic Functional Interface with ArgumentsProcessor<Integer>
ArgumentsProcessor<Integer> intProc = new ArgumentsProcessor<Integer>() {
  @Override
  public Integer process(Integer arg1, Integer arg2) {
    return arg1 * arg2;
  }
};

System.out.println(intProc.process(2,3));  	//6

// Generic Functional Interface (Lambda) with ArgumentsProcessor<Integer>
ArgumentsProcessor<Integer> intProcLambda;
intProcLambda = (x,y) -> (x+y);
System.out.println(intProcLambda.process(12,3));

// Generic Functional Interface (Lambda) with ArgumentsProcessor<Strings>
ArgumentsProcessor<String> strProcLambda;
strProcLambda = (x,y) -> (x+y);
System.out.println(strProcLambda.process("hallo ","Sacha"));
``` 

# Interceptors

# Builder Design Pattern
[Builder Design Pattern in Java](https://www.digitalocean.com/community/tutorials/builder-design-pattern-in-java)

# superclass, Subclasses
In Java, as in other object-oriented programming languages, classes can be derived from other classes. The derived class (the class that is derived from another class) is called a subclass. The class from which its derived is called the superclass.

# Builder Class? / 
Builder is a static inner class of the AlertDialog class.

# Mested Class (Embedded or Inner Class)
In object-oriented programming, an inner class or nested class is a class declared entirely within the body of another class or interface. It is distinguished from a subclass.

[Nested Classes](https://docs.oracle.com/javase/tutorial/java/javaOO/nested.html)
- Nested classes are divided into two categories: non-static and static
- Nested classes that are declared static are called static nested classes.
- A nested class is a member of its enclosing class.

# Method Chaining
Method Chaining is the practice of calling different methods in a single line instead of calling other methods with the same object reference separately. Under this procedure, we have to write the object reference once and then call the methods by separating them with a (dot.).

Method chaining in Java is a common syntax to invoke multiple methods calls in OOPs. Each method in chaining returns an object. It violates the need for intermediate variables. In other words, the method chaining can be defined as if we have an object and we call methods on that object one after another is called method chaining.
[Method Chaining](https://www.geeksforgeeks.org/method-chaining-in-java-with-examples/)

Syntax:
```
obj.method1().method2().method3();  
```
## Example 1
```
class A {
 
    private int a;
    private float b;
 
    A() { System.out.println("Calling The Constructor"); }
 
    public A setint(int a)
    {
        this.a = a;
        return this;
    }
 
    public A setfloat(float b)
    {
        this.b = b;
        return this;
    }
 
    void display()
    {
        System.out.println("Display=" + a + " " + b);
    }
}
 
// Driver code
public class Example {
    public static void main(String[] args)
    {
        // This is the "method chaining".
        new A().setint(10).setfloat(20).display();
    }
}
```



# Java Objects
## Collections

[![Collections](https://media.geeksforgeeks.org/wp-content/uploads/20240305183037/Collections-in-Java-768.webp)

| Object | Description |
| --- | --- | --- |
| List | java.util.list | It is an ordered collection of objects in which duplicate values can be stored.  |
| Set | java.util.Set | It is an ordered collection of objects in which duplicate values can be stored, but does not allow to store duplicate elements |
| Map <K,V> | java.util.Map | Map stores data in form of key-value pair it does not allow to store duplicate keys but allows duplicate values in java. |

### HashMap implements Map <K,V>
A HashMap is a hash table-based implementation of the Map interface. It permits null keys and values. Also, this class does not maintain any order among its elements and especially, it does not guarantee that the order will remain constant over time.
``` 
        Map<String, Integer> vehicles = new HashMap<>();
 
        // Add some vehicles.
        vehicles.put("BMW", 5);
        vehicles.put("Mercedes", 3);
        vehicles.put("Audi", 4);
        vehicles.put("Ford", 10);
 
        System.out.println("Total vehicles: " + vehicles.size());
 
        // Iterate over all vehicles, using the keySet method.
        for (String key : vehicles.keySet())
            System.out.println(key + " - " + vehicles.get(key));
        System.out.println();
 
        String searchKey = "Audi";
        if (vehicles.containsKey(searchKey))
            System.out.println("Found total " + vehicles.get(searchKey) + " " + searchKey + " cars!\n");
 
        // Clear all values.
        vehicles.clear();
 
        // Equals to zero.
        System.out.println("After clear operation, size: " + vehicles.size());
``` 

### ArrayList implements Lists<E>
Similar to a List, the size of the ArrayList is increased automatically if the collection grows or shrinks if the objects are removed from the collection. Java ArrayList allows us to randomly access the list. ArrayList can not be used for primitive types, like int, char, etc.
```
        // Creating an ArrayList of String type
        // Type safe ArrayList
        ArrayList<String> al = new ArrayList<String>();
 
        // Adding elements to above object created
        // Custom input elements
        al.add("Geeks");
        al.add("for");
        al.add("Geeks");
 
        // Print and display the elements of ArrayList
        System.out.println(al);
 
        // adding element at index where
        // element is already present
        al.add(1, "Hi");
 
        // Print and display the elements of ArrayList
        System.out.println(al);
```


# Code Examples
## Loop's
### Iterating Over a Collection
```
// Iterating Over a Collection with Lambda
theStudent.forEach(obj -> System.out.println("XXXX: " + obj));

// Iterating Over a Collection
for (Student obj : theStudent) {
    System.out.println("XXXX: " + obj);
}
```

## Strings
### Replace String
```
String query_str = "FROM Student WHERE lastName='<string>'";
query_str.replace("<string>", name);
```






Reference: https://www.w3schools.com/java/java_operators.asp
