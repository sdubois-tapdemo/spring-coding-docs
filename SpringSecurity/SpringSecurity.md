# Spring Security
Spring Security is a powerful and highly customizable authentication and access-control framework. It is the de-facto standard for securing Spring-based applications.
Spring Security is a framework that focuses on providing both authentication and authorization to Java applications. Like all Spring projects, the real power of Spring Security is found in how easily it can be extended to meet custom requirements
[Spring Security Documentaiton](https://spring.io/projects/spring-security)
[Spring Security Getting Started](https://docs.spring.io/spring-security/reference/servlet/getting-started.html)
[Spring Boot REST Security with JPA/Hibernate Tutoria](https://www.luv2code.com/bonus-lecture-spring-boot-rest-security-jpa-hibernate-bcrypt-pdf)
[Spring Boot REST Security with JPA/Hibernate Tutoria Source Code](Spring Boot REST Security with JPA/Hibernate Tutoriahttps://www.luv2code.com/bonus-lecture-spring-boot-rest-security-jpa-hibernate-bcryptcode)

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

## Application Properties
```
logging.level.org.springframework.security=DEBUG
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

## Spring MVC Integration
[Spring MVC Integration](https://docs.spring.io/spring-security/reference/servlet/integrations/mvc.html)

# Configuration Migration
In Spring Security 5.8, the antMatchers, mvcMatchers, and regexMatchers methods were deprecated in favor of new requestMatchers methods. The new requestMatchers methods were added to authorizeHttpRequests, authorizeRequests, CSRF configuration, WebSecurityCustomizer and any other places that had the specialized RequestMatcher methods. The deprecated methods are removed in Spring Security 6.
[Configuration Migration](https://docs.spring.io/spring-security/reference/5.8/migration/servlet/config.html)

# Encrypted Passwords
## BCrypt to hash passwords
[Why you should use BCrypt to hash passwords](https://danboterhoven.medium.com/why-you-should-use-bcrypt-to-hash-passwords-af330100b861) - [Detailed bcrypt algorithm analysis](https://en.wikipedia.org/wiki/Bcrypt) - [Password hashing - Best Practices](https://crackstation.net/hashing-security.htm)

### How to Get a Bcrypt password
You have a plaintext password and you want to encrypt using bcrypt
- Option 1: Use a website utility to perform the encryption
- Option 2: Write Java code to perform the encryption [Generate BCrypt Passwords](https://www.bcryptcalculator.com/)

## Custom Authentification and Authorisation Tables
- Tell Spring how to query your custom tables
- Provide query to find user by user name
- Provide query to find authorities / roles by user name







