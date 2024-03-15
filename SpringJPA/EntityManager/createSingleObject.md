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

## Create Object by Id

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
package com.luv2code.cruddemo.dao;
import com.luv2code.cruddemo.entity.Student;
import java.util.List;

public interface StudentDAO {
  void save(Student theStudent);
```

### StudentDOAImpl Class (StudentDOAImpl.java) 
```
package com.luv2code.cruddemo.dao;
import com.luv2code.cruddemo.entity.Student;
import jakarta.persistence.EntityManager;
import jakarta.persistence.Query;
import jakarta.persistence.TypedQuery;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Repository;
import org.springframework.transaction.annotation.Transactional;
import java.util.List;

@Repository
public class StudentDOAImpl implements StudentDAO{
  @Override
  @Transactional
  public void save(Student theStudent) {
    entityManager.persist(theStudent);
  }
}
```

### CruddemoApplication Class (CruddemoApplication.java) 
```
package com.luv2code.cruddemo;
import com.luv2code.cruddemo.dao.StudentDAO;
import com.luv2code.cruddemo.dao.StudentDOAImpl;
import com.luv2code.cruddemo.entity.Student;
import org.springframework.boot.CommandLineRunner;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.context.annotation.Bean;
import java.util.*;

public class CruddemoApplication {
  public static void main(String[] args) {
    SpringApplication.run(CruddemoApplication.class, args);
  }

  @Bean
  public CommandLineRunner commandLineRunner(StudentDAO studentDAO) {
    return runner -> {
    
      // create the student object
      System.out.println("Creating new Student Object ...");
      Student tempStudent = new Student("Paul", "Doe", "paul@luv2code.com");

      // save the student object
      System.out.println("Saving the new Student ....");
      studentDAO.save(tempStudent);

      // display id of the saved student
      System.out.println("Save Student . Generated Id: " + tempStudent.getId());
    }
  } 
}
```

