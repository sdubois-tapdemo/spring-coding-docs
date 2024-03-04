# Spring Security
Spring Security is a powerful and highly customizable authentication and access-control framework. It is the de-facto standard for securing Spring-based applications.
Spring Security is a framework that focuses on providing both authentication and authorization to Java applications. Like all Spring projects, the real power of Spring Security is found in how easily it can be extended to meet custom requirements

[Spring Security Documentaiton](https://spring.io/projects/spring-security)

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
| /threaddump | {} | List of threads running in your application |

## Spring Boot Actuator dependancy in pom.xml
```
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-security</artifactId>
</dependency>
```

## Install the JSON Formatter in chrome
Navigate to the page https://www.luv2code.com/chrome-json-formatter and install the plugin

## Ressource Properties
Various properties can be specified inside your application.properties file, inside your application.yaml file, or as command line switches.
[Common Application Properties](https://docs.spring.io/spring-boot/docs/current/reference/html/application-properties.html)
```
# Use wildcard '*' to expose all endpoints or expose individuell endpoints with a comma delimited list
management.endpoints.web.exposure.include=health,info.beans,mappings
management.endpoints.web.exposure.include=*

# Configure the Info Endpoints
management.info.env.enabled=true
info.app.name=My Super Cool App
info.app.description=A crazy and fun app, yoohoo!
info.app.version=1.0.0
```

### Secured Endpoints with generated Passwords
Login as user 'user' and take a generated password shown in the console
```
Using generarated security password: atlk900s-2d32-11d3-212d-sl49fh56
```

### Secured Endpoints with predefined user and password
Specify a 'user' and 'password' in the application.properties file
```
spring.security.user.name=sdubois
spring.security.user.password=mypassword
```

