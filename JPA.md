# Jakarta Persistence API (JPA)

- Standard API for Object-to-Relational-Mapping (ORM)
- Only a specification [JPA Specification](https://www.jcp.org/en/jsr/detail?id=338)
	- Defines a set of interfaces [Jakarta Persistence](www.luv2code.com/jpa-vendors)
	- Requires an implementation to be usable (ie Hybernate, EclipseLink or DataNucleus)

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

### Retreive Objects by id
```
int theId = 1;
Student myStudent = entityManager.find(Student.class, theId);
```

### Retreive Objects List by Query
```
TypedQuery<Student> theQuery = entityManager.createQuery("from Student", Student.class);
List<Student> students= theQuery.getResultList();
```
## JPA Query Language

# JPA/Hibernate CRUD Apps
Create, Read, Update and Delete Objects (CRUD)

# Databases

## MySQL Database
### MySQL Database Server
- The MySQL Database Server is the main engine of the database
- Stores data for the database
- Supports CRUD features on the data

### MySQL Workbench
- MySQL Workbench is a client GUI for interacting with the database
- Create database schemas and tables
- Execute SQL queries to retrieve data
- Perform insert, updates and deletes on data
- Handle administrative functions such as creating users

### Install MySQL on the local Machine
Download and install the Software from https://dev.mysql.com/downloads/mysql.
```
https://dev.mysql.com/downloads/mysql/
```

### Run MySQL as Docker Container
```
```

## PostgreSQL
### Run MySQL as Docker Container (Docker Compose)
The configuration of the PostgresSQL database along with port, user and password are stored in the 'docker-compose' file. Make sure that docker desktop is installed and running on your machine.

File: docker-compose'
```
version: "3.9"

volumes:
  postgres:
    driver: local

services:
  postgres:
    image: postgres:14
    restart: always
    environment:
      - POSTGRES_DB=subscription
      - POSTGRES_USER=user
      - POSTGRES_PASSWORD=pgappuser
    ports:
      - '5432:5432'
```

To run the Database Container just execute the following commands:
```
$ docker-compose up -d
$ Recreating user-profile-database_postgres_1 ... done

$ docker ps
CONTAINER ID   IMAGE                        COMMAND                  CREATED         STATUS         PORTS                    NAMES
7ee2317eba81   postgres:14                  "docker-entrypoint.s…"   3 seconds ago   Up 2 seconds   0.0.0.0:5432->5432/tcp   user-profile-database_postgres_1
```

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

File: application.properties
```
spring.datasource.url=jdbc:mysql://127.0.0.1:3306/student_tracker
spring.datasource.username=springstudent
spring.datasource.password=springstudent

# Turn off the Spring Boot banner
spring.main.banner-mode=off

logging.level.root=warn
```



# JPA interfaces
When using Spring Data JPA, developers typically work with two fundamental interfaces: JpaRepository and EntityManager. While both interfaces provide similar functionality for interacting with a database, there are some important differences to be aware of.

- EntityManager Interface
- JPA Repository Interface

## CRUD Repository

## Differences between JpaRepository and EntityManager
- Level of abstraction: JpaRepository provides a higher level of abstraction than EntityManager, which makes it easier to work with common database operations like CRUD operations.
- Query methods: JpaRepository provides a set of predefined methods for querying the database, which can be easily extended and customized by developers. EntityManager, on the other hand, requires developers to write raw SQL queries or use the Criteria API to perform queries.
- Transaction management: JpaRepository provides transaction management out of the box, which simplifies the process of managing database transactions. EntityManager, on the other hand, requires developers to manually manage transactions using the begin(), commit(), and rollback() methods.
- Entity lifecycle management: EntityManager provides more fine-grained control over the lifecycle of persistent entities, including managing detached and transient entities.
Performance: JpaRepository can be more performant than EntityManager in certain situations, as it provides a higher level of caching and optimization for common database operations.

## EntityManager
An EntityManager is a lower-level interface that is part of the Java Persistence API (JPA). It provides a set of methods for managing the lifecycle of persistent entities, including creating, updating, and deleting entities.

### Use Cases
- Need low-level control over the database operations and want to write custom queries
- Provides low-level access to JPA and work directly with JPA entities
- Complex queries that required advanced features such as native SQL queries or stored procedure calls
- When you have custom requirements that are not easily handled by higher-level abstractions
- If you need low-level control and flexibility, use EntityManager

### Annotatoins
| annotation |  Description |
| --- | --- |
| @Repository | Ingerits from @Component and Applied to DAO implementations. Spring will automatically register the DAO implementation (thanks of component scanning) and also provides translation of any JDBC related exceptions |
| @Transactional | Automagically begin and end a transaction for your JPA code |

## JPA Repository
A JpaRepository is a high-level interface that is a part of the Spring Data JPA framework. It provides a set of methods for performing common CRUD (Create, Read, Update, Delete) operations on a database table.
### Use Cases
- If you want high-level of abstraction, use JpaRepository
- Spring Data JPA has a JpaRepository interface
- This provides JPA database access with minimal coding


# @Embeddable and @Embedded
https://www.baeldung.com/jpa-embedded-embeddable
## @Embeddable
JPA provides the @Embeddable annotation to declare that a class will be embedded by other entities.
## @Embedded

## Embeddable Records in Hibernate 6.0 bis 6.1
https://www.heise.de/hintergrund/Persistenz-in-Java-Neues-seit-Hibernate-ORM-6-9651063.html

## JPA Query Language (JPQL)
- Query language for retrieving objects
- Similar in concept to SQL
- where, like, order by, join, in, etc…
- However, JPQL is based on entity name and entity fields
- JPQL Named Parameters are prefixed with a colon : ie. lastName=:theData

```
// JPQL Query Examples
TypedQuery<Student> theQuery = entityManager.createQuery("FROM Student", Student.class);
TypedQuery<Student> theQuery = entityManager.createQuery( "FROM Student WHERE lastName=‘Doe’", Student.class);
TypedQuery<Student> theQuery = entityManager.createQuery( "FROM Student WHERE lastName=‘Doe’ OR firstName=‘Daffy’", Student.class);
TypedQuery<Student> theQuery = entityManager.createQuery( "FROM Student WHERE email LIKE ‘%luv2code.com’", Student.class);

// JPQL Name Parameters are prefixed with a column ':', theData is a placeholder
TypedQuery<Student> theQuery = entityManager.createQuery("FROM Student WHERE lastName=:theData", Student.class);
theQuery.setParameter("theData", name);

List<Student> students = theQuery.getResultList();
```

IMPORTANT: All JPQL syntax is based on
entity name and entity fields

### find Onject by Id
``
public interface StudentDAO {
  void update(Student theStudent);
  public Student findById(Integer id);
}

@Repository
public class StudentDOAImpl implements StudentDAO{
  @Override
  public Student findById(Integer id) {
    return entityManager.find(Student.class, id);
  }
}

public class CruddemoApplication {
  public static void main(String[] args) {
    SpringApplication.run(CruddemoApplication.class, args);
  }

  @Bean
  public CommandLineRunner commandLineRunner(StudentDAO studentDAO) {
    return runner -> {

      int studentId = 1;
      Student myStudent = studentDAO.findById(studentId);
    }
  }
}
```

### Query for Objects
``
public interface StudentDAO {
  void update(Student theStudent);
  List<Student> findAll();
}

@Repository
public class StudentDOAImpl implements StudentDAO{
  @Override
  public List<Student> findAll() {
    // create query asc=ascending, desc=descending
    // TypedQuery<Student> theQuery = entityManager.createQuery("FROM Student ORDER BY lastName desc", Student.class);
    TypedQuery<Student> theQuery = entityManager.createQuery("FROM Student ORDER BY lastName desc", Student.class);

    // return query results
    return theQuery.getResultList();
  }
}

public class CruddemoApplication {
  public static void main(String[] args) {
    SpringApplication.run(CruddemoApplication.class, args);
  } 

  @Bean
  public CommandLineRunner commandLineRunner(StudentDAO studentDAO) {
    return runner -> {
      
      // get a list of students
      List<Student> theStudent = studentDAO.findAll();

      // ForEach (Lambda)
      theStudent.forEach(obj -> System.out.println("Objects: " + obj));

      // For Loop
      for (Student obj : theStudent) {
          System.out.println("Objects: " + obj);
      }
    }
  }
}
```

### Update Onject
```
public interface StudentDAO {
   void update(Student theStudent);
   public Student findById(Integer id);
}

@Repository
public class StudentDOAImpl implements StudentDAO{
  @Override
  @Transactional
  public void update(Student theStudent) {
    entityManager.merge(theStudent);
  }

  @Override
  public Student findById(Integer id) {
    return entityManager.find(Student.class, id);
  }
}

public class CruddemoApplication {
  public static void main(String[] args) {
    SpringApplication.run(CruddemoApplication.class, args);
  }

  @Bean
  public CommandLineRunner commandLineRunner(StudentDAO studentDAO) {
    return runner -> {

      int studentId = 1;
      Student myStudent = studentDAO.findById(studentId);

      // Update a Single Object
      myStudent.setFirstName("Scooby");
      studentDAO.update(myStudent);
    }
  }
}
```

### Delete by Name
``
public interface StudentDAO {
  List<Student> findAll();
  int deleteByName(String name);
}

@Repository
public class StudentDOAImpl implements StudentDAO{
  @Override
  @Transactional
  public int deleteByName(String name) {
    Query theQuery = entityManager.createQuery("DELETE FROM Student WHERE lastName=:theData");
    theQuery.setParameter("theData", name);

    return theQuery.executeUpdate();
  }
}

public class CruddemoApplication {
  public static void main(String[] args) {
    SpringApplication.run(CruddemoApplication.class, args);
  }

  @Bean
  public CommandLineRunner commandLineRunner(StudentDAO studentDAO) {
    return runner -> {

      int cnt = studentDAO.deleteByName("Public");
      System.out.println("Deleted rows: " + cnt);
    }
  }
}
```

## Delete all
``
public interface StudentDAO {
  int deleteAll();
}

public class StudentDOAImpl implements StudentDAO{
  @Override
  @Transactional
  public int deleteAll() {
    retuen entityManager.createQuery("DELETE FROM Student").executeUpdate();
  }
}

public class CruddemoApplication {
  public static void main(String[] args) {
    SpringApplication.run(CruddemoApplication.class, args);
  }

  @Bean
  public CommandLineRunner commandLineRunner(StudentDAO studentDAO) {
    return runner -> {

      int cnt = studentDAO.deleteAll();
      System.out.println("Deleted rows: " + cnt);
    }
  }
}
```



# JPA Entity
## JPA Identity - Primary Key

Identifiers in Hibernate represent the primary key of an entity. This implies the values are unique so that they can identify a specific entity, that they aren’t null and that they won’t be modified. There is a greate site regarding [An Overview of Identifiers in](https://www.baeldung.com/hibernate-identifiers)
### ID Generation Strategies

| Name | Flag | Description |
| --- | --- | --- |
| AUTO Generation | GenerationType.AUTO | Pick an appropriate strategy for the particular database |
| IDENTITY Generation | GenerationType.IDENTITY | Assign primary keys using database identity column |
| SEQUENCE Generation | GenerationType.SEQUENCE | Assign primary keys using a database sequence |
| TABLE Generation | GenerationType.TABLE | Assign primary keys using an underlying database table to ensure uniqueness |
| Custom Generation | - | define a custom generator by implementing the IdentifierGenerator interface |

```
@Entity
@Table(name="student")
public class Student {
@Id
@GeneratedValue(strategy=GenerationType.IDENTITY)
@Column(name="id")
private int id;
…
}
```

