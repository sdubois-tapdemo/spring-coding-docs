# SpringJPA Examples - Student Application 

## JPA Project Setup
```
project
  |__ pom.xml
  |__ src
  |    |__ main
  |    |    |__ java
  |    |    |      |__ com.tanzu.cruddemo
  |    |    |               |__ CruddemoApplication.java   // Application Properties
  |    |    |               |__ doa                        //
  |    |    |                     |__ StudentDOA.java      // Data Access Object (DOA) Interface
  |    |    |                     |__ StudentDOAImpl.java  // Define DAO implementation for Student
  |    |    |               |__ entity                     //
  |    |    |                     |__ Student.java         // JPA Entity for Student
  |    |    |__ resources
  |    |           |__ application.properties              // Application Properties
  |    |           |__ static                              // HTML Files, CSS, JavaScript, imges, etc.
  |    |           |__ templates                           // Auto Configuration Templates (Mustache, FreeMarker, Thymeleaf)
  |    |
  |    |__ test
  |         |__ java
  |
  |__ target

```

## Read all Student Objects

### Student Class (Student.java) 
```
package com.luv2code.cruddemo.entity;

import jakarta.persistence.*;
import org.hibernate.annotations.GeneratedColumn;
import org.hibernate.annotations.ValueGenerationType;

@Entity
@Table(name="student")
public class Student {

    // define fields
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    @Column(name = "Id")
    private int Id;

    @Column(name = "first_name")
    private String firstName;

    @Column(name = "last_name")
    private String lastName;

    @Column(name = "email")
    private String email;

    // define constructors
    public Student() {

    }

    public Student(String firstName, String lastName, String email) {
        this.firstName = firstName;
        this.lastName = lastName;
        this.email = email;
    }

    // define getters/setters
    public String getFirstName() {
        return firstName;
    }

    public void setFirstName(String firstName) {
        this.firstName = firstName;
    }

    public String getLastName() {
        return lastName;
    }

    public void setLastName(String lastName) {
        this.lastName = lastName;
    }

    public String getEmail() {
        return email;
    }

    public void setEmail(String email) {
        this.email = email;
    }

    public int getId() {
        return Id;
    }

    public void setId(int id) {
        Id = id;
    }

    // define toString() method

    @Override
    public String toString() {
        return "Student{" +
                "Id=" + Id +
                ", firstName='" + firstName + '\'' +
                ", lastName='" + lastName + '\'' +
                ", email='" + email + '\'' +
                '}';
    }
}

```

### StudentDAO Class (StudentDAO.java) 
```
public interface StudentDAO {
  List<Student> findAll();
}
```

### StudentDOAImpl Class (StudentDOAImpl.java) 
```
public class StudentDOAImpl implements StudentDAO{
  @Override
  public List<Student> findAll() {
    // create query asc=ascending, desc=descending
    TypedQuery<Student> theQuery = entityManager.createQuery("FROM Student ORDER BY lastName desc", Student.class);

    // return query results
    return theQuery.getResultList();
  }
}
```

### CruddemoApplication Class (CruddemoApplication.java) 
```
public class CruddemoApplication {
  public static void main(String[] args) {
    SpringApplication.run(CruddemoApplication.class, args);
  }

  @Bean
  public CommandLineRunner commandLineRunner(StudentDAO studentDAO) {
    return runner -> {

      // get a list of students
      List<Student> theStudent = studentDAO.findAll();

      // Option-1: ForEach (Lambda)
      theStudent.forEach(obj -> System.out.println("Objects: " + obj));

      //Option-2:  For Loop
      for (Student obj : theStudent) {
          System.out.println("Objects: " + obj);
      }
    }
  }
}
```

