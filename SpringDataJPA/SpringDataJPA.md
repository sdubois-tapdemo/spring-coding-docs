# Spring Data JPA
Spring Data JPA, part of the larger Spring Data family, makes it easy to easily implement JPA-based (Java Persistence API) repositories. It makes it easier to build Spring-powered applications that use data access technologies.

Implementing a data access layer for an application can be quite cumbersome. Too much boilerplate code has to be written to execute the simplest queries. Add things like pagination, auditing, and other often-needed options, and you end up lost.

Spring Data JPA aims to significantly improve the implementation of data access layers by reducing the effort to the amount that’s actually needed. As a developer you write your repository interfaces using any number of techniques, and Spring will wire it up for you automatically. You can even use custom finders or query by example and Spring will write the query for you!

[Spring Data JPA](https://spring.io/projects/spring-data-jpa), [JavaDoc Interface JpaRepository](https://docs.spring.io/spring-data/jpa/docs/current/api/org/springframework/data/jpa/repository/JpaRepository.html), [JPA Query Methods](https://docs.spring.io/spring-data/jpa/reference/jpa/query-methods.html#jpa.query-methods.at-query)


Advanced features available for
- Extending and adding custom queries with JPQL 
- Query Domain Specific Language (Query DSL) 
- Defining custom methods (low-level coding)
[JPA Query Methods](https://docs.spring.io/spring-data/jpa/reference/jpa/query-methods.html#jpa.query-methods.at-query)

## Spring HATEOAS
Spring HATEOAS provides some APIs to ease creating REST representations that follow the HATEOAS principle when working with Spring and especially Spring MVC. The core problem it tries to address is link creation and representation assembly.
[Spring HATEOAS](https://spring.io/projects/spring-hateoas)
- Spring Data REST endpoints are HATEOAS compliant HATEOAS: 
	- HypermediaastheEngineofApplicationState
- Hypermedia-driven sites provide information to access REST interfaces 
	- Think of it as meta-data for REST data

