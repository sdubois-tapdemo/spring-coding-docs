# Spring Project Lombok
Encapsulating object properties via public getter and setter methods is such a common practice in the Java world, and lots of frameworks rely on this “Java Bean” pattern extensively (a class with an empty constructor and get/set methods for “properties”).

## Annotations

| Annotation | Description |
| --- | --- |
| @NoArgsConstructor | will generate a default constructor without any parameter |
| @AllArgsConstructor | will generate a constructor with all parameters in the sequence, they are present in class |
| @RequiredArgsConstructor | will generate a constructor for only required fields which have @NotNull annotation |

### Further Reading
[Bealdung - Spring Project Lombok](https://www.baeldung.com/intro-to-project-lombok)
[Lombok @AllArgsConstructor, @NoArgsConstructor and @RequiredArgsConstructor](http://www.javabyexamples.com/delombok-allargsconstructor-noargsconstructor-and-requiredargsconstructor)

## Getters/Setters, Constructors

### Native Java

```
public class Contacts {
    private String firstName;
    private String lastName;
    private String email;
    private String phone;

    // Constructor
    public Contacts(String firstName, String lastName, String email, String phone) {
        this.firstName = firstName;
        this.lastName = lastName;
        this.email = email;
        this.phone = phone;
    }

    // Getter and Setter for firstName
    public String getFirstName() {
        return firstName;
    }

    public void setFirstName(String firstName) {
        this.firstName = firstName;
    }

    // Getter and Setter for lastName
    public String getLastName() {
        return lastName;
    }

    public void setLastName(String lastName) {
        this.lastName = lastName;
    }

    // Getter and Setter for email
    public String getEmail() {
        return email;
    }

    public void setEmail(String email) {
        this.email = email;
    }

    // Getter and Setter for phone
    public String getPhone() {
        return phone;
    }

    public void setPhone(String phone) {
        this.phone = phone;
    }
```

### Class definitions with Lombok

By adding the @Getter and @Setter annotations, we told Lombok to generate these for all the fields of the class. @NoArgsConstructor will lead to an empty constructor generation.

```
import lombok.Getter;
import lombok.NoArgsConstructor;
import lombok.Setter;
import org.springframework.stereotype.Component;

@Component
@Getter @Setter @NoArgsConstructor
public class Contacts {
    private String firstName;
    private String lastName;
    private String email;
    private String phone;

    // Constructor
    public Contacts(String firstName, String lastName, String email, String phone) {
        this.firstName = firstName;
        this.lastName = lastName;
        this.email = email;
        this.phone = phone;
    }
}
```
### Lazy-loading
A common pattern is to retrieve this data only when it’s first needed. In other words, we only get the data when we call the corresponding getter the first time. We call this lazy-loading.



