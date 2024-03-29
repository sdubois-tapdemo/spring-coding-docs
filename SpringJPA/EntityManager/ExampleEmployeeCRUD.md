# SpringJPA - Employee JPA/RestAPI Example Application 

## JPA Project Setup
```
project
  |__ pom.xml
  |__ src
  |    |__ main
  |    |    |__ java
  |    |    |      |__ com.tanzu.cruddemo
  |    |    |           |__ CruddemoApplication.java           // Application Properties
  |    |    |           |__ service                      
  |    |    |           |     |__ EmployeeService.java         // Employee Service Interface
  |    |    |           |     |__ EmployeeServiceImpl.java     // Employee Service implementation 
  |    |    |           |__ rest                      
  |    |    |           |     |__ EmployeeRestController.java  // RestAPI Controller
  |    |    |           |__ doa                        
  |    |    |           |     |__ EmployeeDAO.java             // Data Access Object (DOA) Interface
  |    |    |           |     |__ EmployeeDAOJpaImpl.java      // Define DAO implementation for Student
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

public interface EmployeeService {
    List<Employee> findAll();
    Employee findById(int employeeId);

    Employee save(Employee employee);

    void deleteById(int employeeId);
}
```

### Employee Service Implementation Class (EmployeeServiceImpl.java)
```
@Service
public class EmployeeServiceImpl implements EmployeeService{
    private EmployeeDAO employeeDAO;

    @Autowired
    public EmployeeServiceImpl(EmployeeDAO theEmployeeDAO) {
        this.employeeDAO = theEmployeeDAO;
    }

    @Override
    public List<Employee> findAll() {
        return employeeDAO.findAll();
    }


    @Override
    public Employee findById(int employeeId) {
        return employeeDAO.findById(employeeId);
    }

    @Transactional
    @Override
    public Employee save(Employee employee) {
        return employeeDAO.save(employee);
    }

    @Transactional
    @Override
    public void deleteById(int employeeId) {
        employeeDAO.deleteById(employeeId);
    }
}
```

## Data Access Object (DAO)
### Employee DAO Class (EmployeeDAO.java) 
```
package com.luv2code.springboot.cruddemo.dao;
import com.luv2code.springboot.cruddemo.entity.Employee;
import java.util.List;

public interface EmployeeDAO{
    List<Employee> findAll();
    Employee findById(int employeeId);

    Employee save(Employee employee);

    void deleteById(int employeeId);
}
```

### Employee DAO Implementation Class (EmployeeDAOJpaImpl.java) 
```
package com.luv2code.springboot.cruddemo.dao;
import com.luv2code.springboot.cruddemo.entity.Employee;
import jakarta.persistence.EntityManager;
import jakarta.persistence.TypedQuery;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Repository;
import java.util.List;

@Repository
public class EmployeeDAOJpaImpl implements EmployeeDAO{
    // define field for entitymanager
    private EntityManager entityManager;

    // Constructor Intejector
    @Autowired
    public EmployeeDAOJpaImpl(EntityManager entityManager) {
        this.entityManager = entityManager;
    }

    @Override
    public List<Employee> findAll() {
        // create query asc=ascending, desc=descending
        TypedQuery<Employee> theQuery = entityManager.createQuery("FROM Employee", Employee.class);

        // execute quoery and get result list
        List<Employee> employees = theQuery.getResultList();

        // return query results
        return employees;
    }

    /**
     * Find a Employee Object from the Database based on the employeeId
     *
     * @param employeeId  represent the primary key of the Employee entity
     * @return Employee
     */
    @Override
    public Employee findById(int employeeId) {
        // Opetion-1: Delete object with by JPQL Query
        // Query theQuery = (entityManager.createQuery("SELECT * FROM Employee WHERE Id=:theData"));
        // theQuery.setParameter("theData", Integer.valueOf(employeeId).toString());
        // theQuery.executeUpdate();

        // Opetion-2: Find object with entityManager.find(), delete object entityManager.remove()
        Employee theEmployee = entityManager.find(Employee.class, employeeId);

        return theEmployee;
    }

    /**
     * Update a Employee Object from the Database based on the employeeId
     *
     * @param employee  represent the primary key of the Employee entity
     */
    @Override
    public Employee save(Employee employee) {
        // save or update employee => if id==0 then save/insert else update)
        Employee dbEmployee = entityManager.merge(employee);

        return dbEmployee;
    }

    /**
     * Delete a Employee Object from the Database based on the employeeId
     *
     * @param employeeId  represent the primary key of the Employee entity
     */
    @Override
    public void deleteById(int employeeId) {
        /*  Delete object with by JPQL Query => not prefered as db is update outsidw of JPA
            Query theQuery = (entityManager.createQuery("DELETE FROM Employee WHERE Id=:theData"));
            theQuery.setParameter("theData", Integer.valueOf(employeeId).toString());
            theQuery.executeUpdate();
        */

        // Find object with entityManager.find(), delete object entityManager.remove()
        Employee dbEmployee = entityManager.find(Employee.class, employeeId);
        entityManager.remove(dbEmployee);
    }
}
```

## Rest Controller
### Rest Controller Class (EmployeeRestController.java)
```
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

