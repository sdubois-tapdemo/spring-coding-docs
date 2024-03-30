# SpringDataJPA - Employee JPA/RestAPI Example with JpaRepository

## JPA Project Setup
```
project
  |__ pom.xml
  |__ src
  |    |__ main
  |    |    |__ java
  |    |    |      |__ com.tanzu.cruddemo
  |    |    |           |__ CruddemoApplication.java           // Application Properties
  |    |    |           |__ doa                        
  |    |    |           |     |__ EmployeeEntity.java          // Data Access Object (DOA) Interface - JPA Reposity
  |    |    |           |__ entity                      
  |    |    |                 |__ Employee.java                // JPA Entity for Student
  |    |    |__ resources
  |    |           |__ application.properties                  // Application Properties
  |    |           |__ static                                  // HTML Files, CSS, JavaScript, imges, etc.
  |    |           |__ templates                               // Auto Configuration Templates (Mustache, FreeMarker, Thymeleaf)
  |    |
  |    |__ test
  |         |__ java
  |
  |__ target

```

## Entity

### Employee Class (Employee.java) 
```
package com.luv2code.springboot.cruddemo.entity;

import jakarta.persistence.*;
import org.springframework.context.annotation.Primary;

@Entity
@Table(name="Employee")
public class Employee {
    // define fields
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    @Column(name="id")
    private int id;
    @Column(name="first_name")
    private String firstName;

    @Column(name="last_name")
    private String lastName;
    @Column(name="email")
    private String email;

    // define constructors
    public Employee() {

    }

    public Employee(int id, String firstName, String lastName, String email) {
        this.firstName = firstName;
        this.lastName = lastName;
        this.email = email;
    }

    // define getters/setters

    public int getId() {
        return id;
    }

    public String getFirstName() {
        return firstName;
    }

    public String getLastName() {
        return lastName;
    }

    public String getEmail() {
        return email;
    }

    public void setId(int id) {
        this.id = id;
    }

    public void setFirstName(String firstName) {
        this.firstName = firstName;
    }

    public void setLastName(String lastName) {
        this.lastName = lastName;
    }

    public void setEmail(String email) {
        this.email = email;
    }

    /// define toString
    @Override
    public String toString() {
        return "Employee{" +
                "id=" + id +
                ", firstName='" + firstName + '\'' +
                ", lastName='" + lastName + '\'' +
                ", email='" + email + '\'' +
                '}';
    }
}
```

## Data Access Object (DAO) - JPA Repisotory
### Employee DAO Class (EmployeeRepository.java)
```
package com.luv2code.springboot.cruddemo.DAO;
import com.luv2code.springboot.cruddemo.entity.Employee;
import org.springframework.data.jpa.repository.JpaRepository;

public interface EmployeeRepository extends JpaRepository<Employee, Integer> {
}
```

