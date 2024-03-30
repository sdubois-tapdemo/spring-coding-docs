# Spring Data REST
Spring Data REST is part of the umbrella Spring Data project and makes it easy to build hypermedia-driven REST web services on top of Spring Data repositories. Spring Data REST builds on top of Spring Data repositories, analyzes your application’s domain model and exposes hypermedia-driven HTTP resources for aggregates contained in the model.
[Spring Data REST](https://spring.io/projects/spring-data-rest), [Introduction to Spring Data REST](https://www.baeldung.com/spring-data-rest-intro)

| HTTP Methode | Mapping | Description | 
| --- | --- | --- |
| POST | /entity | Create a new Entity |
| GET |  /entity | Get a list of Entites |
| GET |  /entity/{id} | Get a single Entity |
| PUT |  /entity | Update an Entity |
| DELETE | /entity/{id} | Delete an Entity |

## Spring HATEOAS
Spring HATEOAS provides some APIs to ease creating REST representations that follow the HATEOAS principle when working with Spring and especially Spring MVC. The core problem it tries to address is link creation and representation assembly.
[Spring HATEOAS](https://spring.io/projects/spring-hateoas)
- Spring Data REST endpoints are HATEOAS compliant HATEOAS: 
	- HypermediaastheEngineofApplicationState
- Hypermedia-driven sites provide information to access REST interfaces 
	- Think of it as meta-data for REST data

