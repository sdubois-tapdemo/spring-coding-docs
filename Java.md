# Java

## Java Bean
A Java Bean is a reusable software component in Java. It is a class that encapsulates many objects into a single object (the bean), and can be instantiated the same way as a normal Java class, public class MyBean { //getters, setters, and methods for the class}. It’s a way to create reusable components for your Java applications.

### Creating a Java Bean
To create a Java Bean, you need to follow some rules. A Java Bean is a class that:

- Is serializable (implements the Serializable interface).
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
