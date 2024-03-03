# Application Properties
Various properties can be specified inside your application.properties file, inside your application.yaml file, or as command line switches.
[Common Application Properties](https://docs.spring.io/spring-boot/docs/current/reference/html/application-properties.html)

## Properties Examples
```
server.port=8585	## Server Port for HTTP server
socker.team=FC Basel	## Custom Property
```

## Simple RestController

```
public class myClass {
    @Value("${socker.team}")        // read socker.team variable from application.properties
    private String sockerTeam;

    public String HelloWorld() {
        System.out.println("Message: " + sockerTeam);

        return "Hello World";
    }
}
```
