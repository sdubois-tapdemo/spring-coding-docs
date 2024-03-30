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
  |    |    |           |__ service                      
  |    |    |           |     |__ EmployeeService.java         // Employee Service Interface
  |    |    |           |     |__ EmployeeServiceImpl.java     // Employee Service implementation 
  |    |    |           |__ rest                      
  |    |    |           |     |__ EmployeeRestController.java  // RestAPI Controller
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

## Service Layer
### Employee Service Interface (EmployeeService.java)    
```
package com.luv2code.springboot.cruddemo.service;
import com.luv2code.springboot.cruddemo.entity.Employee;
import java.util.List;
import java.util.Optional;

public interface EmployeeService {
    List<Employee> findAll();

    Employee findById(int employeeId);

    Employee save(Employee employee);

    void deleteById(int employeeId);
```

### Employee Service Implementation Class (EmployeeServiceImpl.java)
```
package com.luv2code.springboot.cruddemo.service;
import com.luv2code.springboot.cruddemo.DAO.EmployeeRepository;
import com.luv2code.springboot.cruddemo.entity.Employee;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;
import org.springframework.transaction.annotation.Transactional;
import java.util.List;
import java.util.Optional;

@Service
public class EmployeeServiceImpl implements EmployeeService{
    private EmployeeRepository employeeRepository;

    @Autowired
    public EmployeeServiceImpl(EmployeeRepository theEmployeeRepository) {
        this.employeeRepository = theEmployeeRepository;
    }

    @Override
    public List<Employee> findAll() {
        return employeeRepository.findAll();
    }


    @Override
    public Employee findById(int employeeId) {
        Optional<Employee> result = employeeRepository.findById(Integer.valueOf(employeeId));
        Employee theEmployee = null;

        if (result.isPresent()) {
            theEmployee = result.get();
        } else {
            // we did not find the employee
            throw new RuntimeException("Did not find employee id - " + employeeId);
        }

        return theEmployee;
    }

    @Override
    public Employee save(Employee employee) {
        return employeeRepository.save(employee);
    }

    @Override
    public void deleteById(int employeeId) {
        employeeRepository.deleteById(employeeId);
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

## Rest Controller
### Rest Controller Class (EmployeeRestController.java)
```
package com.luv2code.springboot.cruddemo.rest;
import com.luv2code.springboot.cruddemo.entity.Employee;
import com.luv2code.springboot.cruddemo.service.EmployeeService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.transaction.annotation.Transactional;
import org.springframework.web.bind.annotation.*;

import java.util.List;
import java.util.Optional;

@RestController
@RequestMapping("/api")
public class EmployeeRestController {
    private EmployeeService employeeService;
    @Autowired
    public EmployeeRestController(EmployeeService theEmployeeService){
        this.employeeService = theEmployeeService;
    }

    @GetMapping("/employees")
    public List<Employee> findAll() {
        return employeeService.findAll();
    }

    @GetMapping("/employees/{employeeId}")
    public Employee getEmployee(@PathVariable int employeeId) {
        Employee dbEmployee = employeeService.findById(employeeId);

        if (dbEmployee == null) {
            throw new RuntimeException("Employer Id not found - " + employeeId);
        }

        return dbEmployee;
    }

    @PostMapping("/employees")
    public Employee addEmployee(@RequestBody Employee employee) {
        System.out.println("FirstName: " + employee.getFirstName());
        System.out.println("LastName:  " + employee.getLastName());
        System.out.println("Email:     " + employee.getEmail());

        // Make sure 'id=0' if another values is passed in the JSON
        employee.setId(0);

        Employee dbEmployee = employeeService.save(employee);

        return dbEmployee;
    }

    @PutMapping("/employees")
    public Employee updateEmployee(@RequestBody Employee employee) {
        Employee dbEmployee = employeeService.save(employee);

        return dbEmployee;
    }

    @DeleteMapping("/employees/{employeeId}")
    public String deleteEmployee(@PathVariable int employeeId) throws Exception {
        Employee tempEmployee = employeeService.findById(employeeId);
        if (tempEmployee == null) {
            throw new RuntimeException("Employee Id not found - " + employeeId);
        }

        employeeService.deleteById(employeeId);

        return "Deleted employee id - " + employeeId;
    }
}
```

