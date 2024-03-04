# Spring Boot Actuator
Spring Boot Actuator is a module that provides production-ready features to monitor and manage your Spring Boot application. It offers various endpoints and metrics that can be used for monitoring, health checks, auditing, and managing your application.

## Spring Boot Starter Parent
- Exposes endpoints to monitor and manage your application
- You easily get DevOps functionality out-of-the-box
- Simply add the dependency to your POM file
- REST endpoints are automatically added to your application

## Actuator Types
Endpoints are prefixed with: /actuator. Here is a list of standard actuators

| Endpoingt | Default | Description |
| --- | --- |
| /actuator/health | {"status":"UP"} | Health information about your application |
| /actuator/info | {} | The /info endpoint can provide information about your application |

## Spring Boot Actuator dependancy in pom.xml
```
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```

## Ressource Properties
Various properties can be specified inside your application.properties file, inside your application.yaml file, or as command line switches.
[Common Application Properties](https://docs.spring.io/spring-boot/docs/current/reference/html/application-properties.html)
```
management.endpoints.web.exposure.include=health,info   // define what endpoints should be exposed
management.info.env.enabled=true 			// exposes /actuator/info
```


