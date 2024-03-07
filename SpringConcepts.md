# Inversion of Control (IoC)
The approach of outsourcing the construction and management of objects.

## Spring Container
### Primary functions
- Create and manage objects (Inversion of Control)
- Inject object dependencies (Dependency Injection)

### Configuring Spring Container
- XML configuration file (legacy)
- Java Annotations (modern)
- Java Source Code (modern)

## Spring Dependency Injection
Dependency Injection (DI) is a design pattern. It promotes loose coupling and modularity by providing dependencies at runtime and separates the concern of object creation from business logic. Spring provides a dependency injection container which abstracts away the logic for object creation. To manage any object by Spring, we annotate the class as @Component or @Service.
The dependency inversion principle.
- The client delegates to another object
- the responsibility of providing its dependencies.

### Injection Types
There are multiple types of injection with Spring. [Setter injection versus constructor injection](https://spring.io/blog/2007/07/11/setter-injection-versus-constructor-injection-and-the-use-of-required).

We will cover the two recommended types of injection
- Constructor Injection
- Setter Injection

### Constructor Injection
In constructor injection, Spring provides the dependencies of a class through its constructor at the time of initializing the object. [Spring Boot Constructor Injection Example](https://www.javaguides.net/2023/01/spring-boot-constructor-injection.html).
- Use this when you have required dependencies
- Generally recommended by the spring.io development team as first choice
- Use this when you have required dependencies
- Generally recommended by the spring.io development team as first choice§

When Spring creates an instance of the class, it passes the required dependencies as arguments to the constructor. In Spring, we achieve constructor injection by annotating the constructor with @Autowired.
```
public class MyClass { 
  private final Book book;

  @Autowired
  public MyClass(Book book) {        
    this.book = book;    
  }
}
```

If thera are multiple beans that qualify for injection, an error message apears and the application won't start
```
Parameter 0 of constructor in com.luv2code.springcoredemo.rest.DemoController
required a single bean, but 4 were found:
```
The solution is to use the @Qualifier annotation to specify which one to use.
```
  @Autowired
  public DemoController(@Qualifier("cricketCoach") Coach theCoach) {
    myCoach = theCoach;
  }
```
INPORTANT: Specify the bean id: cricketCoach Same name as class, first character lower-case


### Setter Injection
- Use this when you have optional dependencies
- If dependency is not provided, your app can provide reasonable default logic
- Use this when you have optional dependencies
- If dependency is not provided, your app can provide reasonable default logic

```
@RestController
public class DemoController {
  private Coach myCoach;

  @Autowired
  public void setCoach(Coach theCoach) {
    myCoach = theCoach;
  }
}
```

If thera are multiple beans that qualify for injection, an error message apears and the application won't start
```
Parameter 0 of constructor in com.luv2code.springcoredemo.rest.DemoController
required a single bean, but 4 were found:
```
The solution is to use the @Qualifier annotation to specify which one to use.
```
  @Autowired
  public void setCoach(@Qualifier("cricketCoach") Coach theCoach) {
    myCoach = theCoach;
  }
```
INPORTANT: Specify the bean id: cricketCoach Same name as class, first character lower-case


### Field Injection
In field injection, Spring directly sets the dependencies into the fields of a class, which you annotate as @Autowired. When Spring creates an instance of the class, it uses reflection to iterate over the fields and injects dependencies after creating the instance.
- In the early days, field injection was popular on Spring projects
- In recent years, it has fallen out of favor
- In general, it makes the code harder to unit test
- As a result, the spring.io team does not recommend field injection
- However, you will still see it being used on legacy projects

```
public class MyClass {

    @Autowired    
    private Book book;

}
```

### @Primary Annotation
Instead of specifying a coach by name using @Qualifier, the @Primary Annotation can be set on the Bean itself to specify the Primary Bean to be used. 

```
@Primary
@Component
public class CricketCoach implements Coach {

    private Coach myCoach;

    @Override
    public String getDailyWorkout() {
        return "Practice fast bowling for 15min\n";
    }
}
```

### Lazy Initialization
Instead of creating all beans up front, we can specify lazy initialization
- A bean will only be initialized in the following cases:
	- It is needed for dependency injection
	- Or it is explicitly requested
- Add the @Lazy annotation to a given class

## Spring AutoWiring
For dependency injection, Spring can use autowiring

- Spring will look for a class that matches
- matches by type: class or interface
- Spring will inject it automatically … hence it is autowired

## Annotations
### @Component annotation
- @Component marks the class as a Spring Bean
- A Spring Bean is just a regular Java class that is managed by Spring
- @Component also makes the bean available for dependency injection

### @Autowired annotation 
The @Autowired annotation tells Spring to inject a dependency

# Annotation Interface 
## SpringBootApplication (org.springframework.boot.autoconfigure.SpringBootApplication)
Package: [org.springframework.boot.autoconfigure](https://docs.spring.io/spring-boot/docs/current/api/org/springframework/boot/autoconfigure/SpringBootApplication.html) 

| Annotation | Description |
| --- | --- |
| @EnableAutoConfiguration | Enables Spring Boot's auto-configuration support |
| @ComponentScan | Enables component scanning of current package Also recursively scans sub-packages |
| @Configuration | Able to register extra beans with @Bean or import other configuration classes |

### Component Scanning
Explicitly list base packages to scan
```
@SpringBootApplication(
scanBasePackages={"com.luv2code.springcoredemo",
   "com.luv2code.util",
   "org.acme.cart",
   "edu.cmu.srs"})

public class SpringcoredemoApplication {
```

