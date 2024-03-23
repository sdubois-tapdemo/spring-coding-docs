# Spring Security
Spring Security is a powerful and highly customizable authentication and access-control framework. It is the de-facto standard for securing Spring-based applications.
Spring Security is a framework that focuses on providing both authentication and authorization to Java applications. Like all Spring projects, the real power of Spring Security is found in how easily it can be extended to meet custom requirements

[Spring Security Documentaiton](https://spring.io/projects/spring-security)

## Spring Security Features
- Comprehensive and extensible support for both Authentication and Authorization
- Protection against attacks like session fixation, clickjacking, cross site request forgery, etc
- Servlet API integration
- Optional integration with Spring Web MVC

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

