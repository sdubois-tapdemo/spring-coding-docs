# Application Properties
Various properties can be specified inside your application.properties file, inside your application.yaml file, or as command line switches.
[Common Application Properties](https://docs.spring.io/spring-boot/docs/current/reference/html/application-properties.html)

## Properties Examples
```
server.port=8585	## Server Port for HTTP server
socker.team=FC Basel	## Custom Property
```

## Directory Structore
```
project
  |__ pom.xml
  |__ src
  |    |__ main
  |    |    |__ java
  |    |    |__ resources
  |    |           |__ application.properties
  |    |
  |    |__ test
  |         |__ java
  |
  |__ target

```

## Java read Application Properties
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

## Spring read Application Properties
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
