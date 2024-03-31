# Spring Data REST
Spring Data REST is part of the umbrella Spring Data project and makes it easy to build hypermedia-driven REST web services on top of Spring Data repositories. Spring Data REST builds on top of Spring Data repositories, analyzes your application’s domain model and exposes hypermedia-driven HTTP resources for aggregates contained in the model.
[Spring Data REST](https://spring.io/projects/spring-data-rest), [Introduction to Spring Data REST](https://www.baeldung.com/spring-data-rest-intro), [Spring Data REST Reference Guide](https://docs.spring.io/spring-data/rest/docs/4.2.0-M2/reference/html)

| HTTP Methode | Mapping | Description | 
| --- | --- | --- |
| POST | /entity | Create a new Entity |
| GET |  /entity | Get a list of Entites |
| GET |  /entity/{id} | Get a single Entity |
| PUT |  /entity | Update an Entity |
| DELETE | /entity/{id} | Delete an Entity |

## Spring Data REST advanced features
- Pagination, sorting and searching
- Extending and adding custom queries with JPQL 
- Query Domain Specific Language (Query DSL)

## Maven Dependancy
the Dependancy name used on start.spring.io is 'Rest Repositories - Exposing Spring Data repositories over REST via Spring Data REST.'
```
    <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-data-rest</artifactId>
    </dependency>
```

## REST Endpoints
- By default, Spring Data REST will create endpoints based on entity type 
- Simple pluralized form
	- First character of Entity type is lowercase 
	- Then just adds an "s" to the entity

## Annotations
| Annotation | Description |
| --- | --- |
| @RepositoryRestResource(path="members") | Choose a different entity name for the REST endpoint |

Example: 
```
@RepositoryRestResource(path="members")
public interface EmployeeRepository extends JpaRepository<Employee, Integer> {
``` 

## Application Properties
[Spring Data REST Applicaiton Properties](https://docs.spring.io/spring-data/rest/docs/4.2.0-M2/reference/html/#getting-started.changing-other-properties), [Common Application Properties](https://docs.spring.io/spring-boot/docs/current/reference/html/application-properties.html#appendix.application-properties) 
| Property | Description |
| --- | --- |
| spring.data.rest.base-path | Base path used to expose repository resources |
| spring.data.rest.default-page-size | Default size of pages |
| spring.data.rest.max-page-size | Maximum size of pages |
```   
# Spring Data REST Properties
spring.data.rest.base-path=/magic-api
```   

### Pagination
By default, Spring Data REST will return the first 20 elements Page size = 20. You can navigate to the different pages of data using query param
```
http://localhost:8080/employees?page=0
http://localhost:8080/employees?page=1
```

### Sorting
```
http://localhost:8080/employees?sort=lastName 			// Sort by last name (ascending is default)
http://localhost:8080/employees?sort=firstNAme,desc		// Sort by first name, descending
http://localhost:8080/employees?sort=lastName,firstName,asc	// Sort by last name, then first name, ascending
```

# Spring HATEOAS
Spring HATEOAS provides some APIs to ease creating REST representations that follow the HATEOAS principle when working with Spring and especially Spring MVC. The core problem it tries to address is link creation and representation assembly.
[Spring HATEOAS](https://spring.io/projects/spring-hateoas), [Hypertext Application Language (HAL)](https://en.wikipedia.org/wiki/Hypertext_Application_Language)
- Spring Data REST endpoints are HATEOAS compliant HATEOAS: 
	- HypermediaastheEngineofApplicationState
- Hypermedia-driven sites provide information to access REST interfaces 
	- Think of it as meta-data for REST data

## Example for all employee (HATEOAS/HAL): GET /employees
```
{
    "_embedded": {
        "employees": [
            {
                "firstName": "Leslie",
                "lastName": "Andrews",
                "email": "leslie@luv2code.com",
                "_links": {
                    "self": {
                        "href": "http://localhost:8080/employees/1"
                    },
                    "employee": {
                        "href": "http://localhost:8080/employees/1"
                    }
                }
            },
            {
                "firstName": "Emma",
                "lastName": "Baumgarten",
                "email": "emma@luv2code.com",
                "_links": {
                    "self": {
                        "href": "http://localhost:8080/employees/2"
                    },
                    "employee": {
                        "href": "http://localhost:8080/employees/2"
                    }
                }
            },
            {
                "firstName": "Avani",
                "lastName": "Gupta",
                "email": "avani@luv2code.com",
                "_links": {
                    "self": {
                        "href": "http://localhost:8080/employees/3"
                    },
                    "employee": {
                        "href": "http://localhost:8080/employees/3"
                    }
                }
            },
            {
                "firstName": "Yuri",
                "lastName": "Petrov",
                "email": "yuri@luv2code.com",
                "_links": {
                    "self": {
                        "href": "http://localhost:8080/employees/4"
                    },
                    "employee": {
                        "href": "http://localhost:8080/employees/4"
                    }
                }
            },
            {
                "firstName": "Juan",
                "lastName": "Vega",
                "email": "juan@luv2code.com",
                "_links": {
                    "self": {
                        "href": "http://localhost:8080/employees/5"
                    },
                    "employee": {
                        "href": "http://localhost:8080/employees/5"
                    }
                }
            }
        ]
    },
    "_links": {
        "self": {
            "href": "http://localhost:8080/employees?page=0&size=20"
        },
        "profile": {
            "href": "http://localhost:8080/profile/employees"
        }
    },
    "page": {
        "size": 20,
        "totalElements": 5,
        "totalPages": 1,
        "number": 0
    }
}
```
## Example for single employee (HATEOAS/HAL): GET /employees/1
```
{
  "firstName": "Leslie",
  "lastName": "Andrews",
  "email": "leslie@luv2code.com",
  "_links": {
    "self": {
      "href": "http://localhost:8080/employees/1"
    },
    "employee": {
      "href": "http://localhost:8080/employees/1"
    }
  }
}
```
## Example for all employee: GET /api/employees
```
[
    {
        "id": 1,
        "firstName": "Leslie",
        "lastName": "Andrews",
        "email": "leslie@luv2code.com"
    },
    {
        "id": 2,
        "firstName": "Emma",
        "lastName": "Baumgarten",
        "email": "emma@luv2code.com"
    },
    {
        "id": 3,
        "firstName": "Avani",
        "lastName": "Gupta",
        "email": "avani@luv2code.com"
    },
    {
        "id": 4,
        "firstName": "Yuri",
        "lastName": "Petrov",
        "email": "yuri@luv2code.com"
    },
    {
        "id": 5,
        "firstName": "Juan",
        "lastName": "Vega",
        "email": "juan@luv2code.com"
    }
]
```
## Example for single employee: GET /api/employees/1
```
{
  "id": 1,
  "firstName": "Leslie",
  "lastName": "Andrews",
  "email": "leslie@luv2code.com"
}
```

