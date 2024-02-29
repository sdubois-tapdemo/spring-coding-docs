# Maven

## How to find dependany coordinates
## Lookup on the Maven Repository (search.maven.org)
Navigate to search.maven.org and search ie. for hibernate, choose a version and the page shows you a list of Maven dependancies you need to add in your POM.xml file.
## Spring dependancies on (start.spring.io) 
The best place to find Spring dependancies is on https://start.spring.io/, select your Java and Spring Version and click on 'dependancyes^ and add one or more of your spring projects. Then hit <Explore> instead of <Generate>. This will show you the required Maven dependancoies for your Spring projects.

## Maven Plugins
A list of Maven Plugins can be found under https://maven.apache.org/plugins.

## Directory Structore
```
project
  |__ pom.xml
  |__ src
  |    |__ main
  |    |    |__ java 
  |    |    |__ resources 
  |    |    
  |    |__ test
  |         |__ java 
  |
  |__ target

```


## Maven Commands

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
mvn spring:run 
```

