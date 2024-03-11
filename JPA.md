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

# JPA Entity
## JPA Identity - Primary Key
Identifiers in Hibernate represent the primary key of an entity. This implies the values are unique so that they can identify a specific entity, that they aren’t null and that they won’t be modified. There is a greate site regarding [An Overview of Identifiers in](https://www.baeldung.com/hibernate-identifiers)
### ID Generation Strategies

| Name | Description |
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

