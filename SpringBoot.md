# SpringBoot
Spring Boot makes it easy to create stand-alone, production-grade Spring based Applications that you can "just run".  We take an opinionated view of the Spring platform and third-party libraries so you can get started with minimum fuss. Most Spring Boot applications need minimal Spring configuration.

### Features
- Create stand-alone Spring applications
- Embed Tomcat, Jetty or Undertow directly (no need to deploy WAR files)
- Provide opinionated 'starter' dependencies to simplify your build configuration
- Automatically configure Spring and 3rd party libraries whenever possible
- Provide production-ready features such as metrics, health checks, and externalized configuration
- Absolutely no code generation and no requirement for XML configuration
- Help to resolve dependency conflicts (Maven or Gradle)

# Spring Initializer
[Spring Initializer](http://start.spring.io)

## Spring Boot Starters
A full list of the Spring Boot Starters can be found here [Spring Boot Starters](https://docs.spring.io/spring-boot/docs/current/reference/htmlsingle/#using.build-systems.starters).
- A curated list of Maven dependencies
- A collection of dependencies grouped together
- Tested and verified by the Spring Development team
- Makes it much easier for the developer to get started with Spring
- Reduces the amount of Maven configuration

| Spring Starter | Description |
| --- | --- |
| Spring Boot Starter | Core starter, including auto-configuration support, logging and YAML |
| Spring Web | Build web, including RESTful, applications using Spring MVC. Uses Apache Tomcat as the default embedded container. | 
| Spring Boot Starter Test | Starter for testing Spring Boot applications with libraries including JUnit Jupiter, Hamcrest and Mockito |
|  Spring Boot Starter Actuator | Starter for using Spring Boot's Actuator which provides production ready features to help you monitor and manage your application |
| Spring Boot Starter AOP | Starter for aspect-oriented programming with Spring AOP and AspectJ |
| Spring Boot Starter Data JPA | Starter for using Spring Data JPA with Hibernate |
| Spring Boot Starter Security | org.springframework.boot » spring-boot-starter-security | 
| Spring Boot Starter Validation | Starter for using Java Bean Validation with Hibernate Validator |
| Spring Boot Starter Data Redis | Starter for using Redis key-value data store with Spring Data Redis and the Lettuce client |
| Spring Boot Starter JDBC | Starter for using JDBC with the HikariCP connection pool | 
| Spring Boot Starter Log4j2 | Starter for using Log4j2 for logging. An alternative to spring-boot-starter-logging |
| Spring Boot Starter WebFlux | Starter for building WebFlux applications using Spring Framework's Reactive Web support |
| Spring Boot Starter Logging | org.springframework.boot » spring-boot-actuator |
| Spring Boot Starter Mail | Starter for using Java Mail and Spring Framework's email sending support |

See Spring Starters dependancies in IntelliJ under View > Tool Windows > Maven Projects > Dependencies.

# Spring Boot Application

## Spring Boot Command Line App

```
import org.springframework.boot.CommandLineRunner;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.context.annotation.Bean;

@SpringBootApplication
public class CruddemoApplication implements CommandLineRunner{

  public static void main(String[] args) {
    SpringApplication.run(CruddemoApplication.class, args);
  }

  @Override
  public void run(String... args) throws Exception {
    System.out.println("this is a test\n");
  }
}
```

```
import org.springframework.boot.CommandLineRunner;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.context.annotation.Bean;

@SpringBootApplication
public class CruddemoApplication {
  public static void main(String[] args) {
    SpringApplication.run(CruddemoApplication.class, args);
  }

  @Bean
  public CommandLineRunner commandLineRunner(String[] args) {
    return runner -> {
      System.out.println("Hello world");
    };
  }
}
```

