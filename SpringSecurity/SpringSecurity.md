# Spring Security
Spring Security is a powerful and highly customizable authentication and access-control framework. It is the de-facto standard for securing Spring-based applications.
Spring Security is a framework that focuses on providing both authentication and authorization to Java applications. Like all Spring projects, the real power of Spring Security is found in how easily it can be extended to meet custom requirements
[Spring Security Documentaiton](https://spring.io/projects/spring-security)
[Spring Security Getting Started](https://docs.spring.io/spring-security/reference/servlet/getting-started.html)

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
[Spring Security API Documentation](https://docs.spring.io/spring-security/site/docs/current/api/org/springframework/security/)
[Spring Security Source](https://github.com/spring-projects/spring-security/tree/main/config/src/main/java/org/springframework/security)

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

## Cross-Site Request Forgery (CSRF)
- Spring Security can protect against CSRF attacks
- Embed additional authentication data/token into all HTML forms
- On subsequent requests, web app will verify token before processing
- Primary use case is traditional web applications (HTML forms etc …)
### When to use CSRF Protection?
- The Spring Security team recommends
	- Use CSRF protection for any normal browser web requests
	- Traditional web apps with HTML forms to add/modify data
- If you are building a REST API for non-browser clients
	- you may want to disable CSRF protection
- In general, not required for stateless REST APIs
	- That use POST, PUT, DELETE and/or PATCH




