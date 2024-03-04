# Spring Boot Actuator
Spring Boot Actuator is a module that provides production-ready features to monitor and manage your Spring Boot application. It offers various endpoints and metrics that can be used for monitoring, health checks, auditing, and managing your application. A full list of the Spring Actuators can be found here [Spring Actuators](https://docs.spring.io/spring-boot/docs/current/reference/htmlsingle/#actuator.endpoints)

## Spring Boot Actuators Features
- Exposes endpoints to monitor and manage your application
- You easily get DevOps functionality out-of-the-box
- Simply add the dependency to your POM file
- REST endpoints are automatically added to your application

## Actuator Types
Endpoints are prefixed with: /actuator ie. http://localhost:8080/actuator. Here is a list of standard actuators

| Endpoingt | Default | Description |
| --- | --- | --- |
| /health | {"status":"UP"} | Health information about your application |
| /info | {} | The /info endpoint can provide information about your application |
| /auditevents | {} | Audit events for your application |
| /beans | {} | List of all beans registered in the Spring application context |
| /mappings | {} | List of all @RequestMapping paths |

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
# Actuator Endpoints Definition (selective or just '*' for all)
management.endpoints.web.exposure.include=health,info.beans,mappings
management.endpoints.web.exposure.include=*

# Configure the Info Endpoingt
management.info.env.enabled=true
info.app.name=My Super Cool App
info.app.description=A crazy and fun app, yoohoo!
info.app.version=1.0.0
```

### Health Endpoint
```
{
  "status": "UP"
}
```

### Info Endpoint
Properties starting with info defined in the application.properties files, will be used by /info
```
{
  "app": {
    "name": "My Super Cool App",
    "description": "A crazy and fun app, yoohoo!",
    "version": "1.0.0"
}
```


