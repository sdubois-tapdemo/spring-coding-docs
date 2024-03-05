# Maven

## How to find dependany coordinates
## Lookup on the Maven Repository (search.maven.org)
Navigate to search.maven.org and search ie. for hibernate, choose a version and the page shows you a list of Maven dependancies you need to add in your POM.xml file.
## Spring dependancies on (start.spring.io) 
The best place to find Spring dependancies is on https://start.spring.io/, select your Java and Spring Version and click on 'dependancyes^ and add one or more of your spring projects. Then hit <Explore> instead of <Generate>. This will show you the required Maven dependancoies for your Spring projects.

## Spring Boot Starter Parent
- Default Maven configuration: Java version, UTF-encoding etc
- Dependency management
- Use version on parent only
- spring-boot-starter-* dependencies inherit version from parent
- Default configuration of Spring Boot plugin

```
        <parent>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-starter-parent</artifactId>
                <version>3.2.3</version>
                <relativePath/> <!-- lookup parent from repository -->
        </parent>
```

## Maven Plugins
A list of Maven Plugins can be found under https://maven.apache.org/plugins.

| Plugin | Description |
| --- | --- |
| spring-boot-maven-plugin | Provides: mvn spring-boot:run |

## Spring Boot Maven Plugin
The [Spring Boot Maven Plugin](https://docs.spring.io/spring-boot/docs/2.0.1.RELEASE/maven-plugin/index.html)  provides Spring Boot support in Maven, allowing you to package executable jar or war archives and run an application “in-place”.




## Spring Boot Dev Tools
Automatically restarts your application when code is updated. More details [Spring Boot Dev Tools](https://www.baeldung.com/spring-boot-devtools). Add the following lines to the pom.xml 
```
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-devtools</artifactId>
</dependency>
```
To enable it in IntelliJ CE, navigate to: 
- IntelliJ -> Settings -> Build, Execution, Deployment -> Compiler and enable "Build project automatically"
- IntelliJ -> Settings -> Advanced Settings -> Allow auto-make to start even deployed application is already running (enable)

## Maven Project Directory Structure
```
project
  |__ pom.xml
  |__ src
  |    |__ main
  |    |    |__ java 
  |    |    |__ resources 
  |    |           |__ application.properties      // Application Properties
  |    |           |__ static                      // HTML Files, CSS, JavaScript, imges, etc.
  |    |           |__ templates                   // Auto Configuration Templates (Mustache, FreeMarker, Thymeleaf)
  |    |    
  |    |__ test
  |         |__ java 
  |
  |__ target

```


## Maven Commands

## mvn Package
This command is used to execute all Maven phases until the package phase. The mvn package compiles, verifies, and builds the project.

Additionally, the mvn package creates the JAR file and places it in a specific folder under a specific folder.
```
mvn package
```

## mvn clean install
This Maven command line aids in executing a clean build lifecycle and installs the build phase in the default build cycle. This build lifecycle may have its build phases, and there are different build goals within each build.
```
mvn package
```
Moreover, the mvn clean install command ensures that the build target is removed for a new build and adds the mvn clean install target.

## mvn compile
The Maven command: mvn compile is used to compile the source code. Additionally, the mvn compile compiles the classes stored at a particular target or a class.

The mvn compile is similar to the previous mvn compiler: compile command, but it runs the entire Maven life cycle up to compile. You can transform the Java files into class files along with the maven compiler plugin itself.
```
mvn compile
```






| mvn compile | xxx |
| mvn clean compile test | xxx |
| mvn sprint-boot:run | xxx |
| --- | --- | 



### Compile App
```
mvn clean compile test
mvn spring:run 
```
```
mvn clean compile test
mvn spring-boot:run -Dspring-boot.run.profiles=local

```

