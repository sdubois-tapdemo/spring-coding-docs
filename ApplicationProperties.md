# Application Properties
Various properties can be specified inside your application.properties file, inside your application.yaml file, or as command line switches.
[Common Application Properties](https://docs.spring.io/spring-boot/docs/current/reference/html/application-properties.html)

## Properties Groups

| Group | Description |
| --- | --- |
| Core | un |
| Web | un |
| Security | un |
| Data | un |
| Actuator | un |
| Integration | un |
| DwvTools | un |
| Testing | un |

## Core Properties
```
# Log levels severity mapping (TRACE,DEBUG,INFO,WARN,ERROR,FATAL,OFF)
logging.level.org.springframework=DEBUG
logging.level.org.hibernate=TRACE
logging.level.com.luv2code=INFO
logging.level.root=warn

# Turn off the Spring Boot banner
spring.main.banner-mode=off

# Log file name
logging.file.name=my-crazy-stuff.log
logging.file.path=c:/myapps/demo

# Lazy Initialization - Global configuration, All beans are lazy, no beans are created until needed
spring.main.lazy-initialization=true
```

## Web Properties
```
# HTTP server port
server.port=7070

# Context path of the application
server.servlet.context-path=/my-silly-app

# Default HTTP session time out
server.servlet.session.timeout=15m
```

## Security Properties
```
# Default user name
spring.security.user.name=admin
# Password for default user
spring.security.user.password=topsecret
```

## Data Properties
```
# JDBC URL of the database
spring.datasource.url=jdbc:mysql://localhost:3306/ecommerce

# Login username of the database
spring.datasource.username=scott

# Login password of the database
spring.datasource.password=tiger
```

## Actuator Properties
```
# Use wildcard '*' to expose all endpoints or expose individuell endpoints with a comma delimited list
management.endpoints.web.exposure.include=health,info.beans,mappings
management.endpoints.web.exposure.include=*

# Exclude individual endpoints with a comma-delimited list
management.endpoints.web.exposure.exclude=health

# Configure the Info Endpoints
management.info.env.enabled=true

# Base path for actuator endpoints
management.endpoints.web.base-path=/actuator
```

## Integration Properties
## DwvTools Properties
## Testing Properties

# Using Properties
## Read Application Properties in Java
```
public class myClass {
    public String HelloWorld() {

    public String HelloWorld() throws IOException {
        String rootPath = Thread.currentThread().getContextClassLoader().getResource("").getPath();
        String appConfigPath = rootPath + "application.properties";

        Properties appProps = new Properties();
        try {
            appProps.load(new FileInputStream(appConfigPath));
        } catch (FileNotFoundException ex) {
            System.out.println("Optional file " + appConfigPath + " was not found.");
        }

        String myTeam = appProps.getProperty("socker.team");

        System.out.println("Message (rootPath)   " + rootPath);
        System.out.println("Message (myTeam)     " + myTeam);

        return "Hello World";
    }
}
```

## Read Application Properties in Spring
```
public class myClass {
    @Value("${socker.team}")        // read socker.team variable from application.properties
    private String sockerTeam;

    public String HelloWorld() {
        System.out.println("Message (sockerTeam) " + sockerTeam);

        return "Hello World";
    }
}
```
