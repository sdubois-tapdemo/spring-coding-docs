# Spring Security
Spring Security is a powerful and highly customizable authentication and access-control framework. It is the de-facto standard for securing Spring-based applications.
Spring Security is a framework that focuses on providing both authentication and authorization to Java applications. Like all Spring projects, the real power of Spring Security is found in how easily it can be extended to meet custom requirements
[Spring Security Documentaiton](https://spring.io/projects/spring-security)

## Spring Security Features
- Comprehensive and extensible support for both Authentication and Authorization
- Protection against attacks like session fixation, clickjacking, cross site request forgery, etc
- Servlet API integration
- Optional integration with Spring Web MVC

## Spring Security Overview
- Secure Spring Boot REST APIs
- Define users and roles
- Protect URLs based on role
- Store users, passwords and roles in DB (plain-text -> encrypted)
[Spring Security](https://docs.spring.io/spring-security/reference/)

## Spring Security dependancy in pom.xml
```
<!-- ADDING SUPPORT FOR SPRING SECURITY -->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-security</artifactId>
</dependency>
```

### Secured Endpoints with generated Passwords
Login as user 'user' and take a generated password shown in the console
```
Using generarated security password: atlk900s-2d32-11d3-212d-sl49fh56
```

### Secured Endpoints with predefined user and password
Specify a 'user' and 'password' in the application.properties file
```
spring.security.user.name=myuser
spring.security.user.password=mypassword
```

## Spring Security Model
- Spring Security defines a framework for security
- Implemented using Servlet filters in the background
- Two methods of securing an app: declarative and programmatic
### Spring Security with Servlet Filters
- Servlet Filters are used to pre-process / post-process web requests
- Servlet Filters can route web requests based on security logic
- Spring provides a bulk of security functionality with servlet filters
### Declarative Security
- Define application’s security constraints in configuration
- All Java config: @Configuration
- Provides separation of concerns between application code and security
### Programmatic Security
- Spring Security provides an API for custom application coding
- Provides greater customization for specific app requirements
### Authentication and Authorization
- In-memory
- JDBC
- LDAP
- Custom / Pluggable
- OIDC (Okta, KeyCloak)


