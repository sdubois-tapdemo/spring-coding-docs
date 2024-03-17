



# Spring Project RestAPI
xxx
[Spring Framework Documentation](https://docs.spring.io/spring-framework/reference/) 

## Annotations

| Annotation | Example | Description |
| --- | --- | --- |
| @RequestMapping | @RequestMapping("/api/v3") | annotation to map requests to controllers methods |
| @GetMapping | xxx | will generate a constructor for only required fields which have @NotNull annotation |
| @PostMapping | xxx | Annotation for mapping HTTP POST requests onto specific handler methods |
| @PutMapping | xxx | Annotation for mapping HTTP PUT requests onto specific handler methods |
| @DeleteMapping | xxx | Annotation for mapping HTTP DELETE requests onto specific handler methods |
| @PatchMapping | xxx | Annotation for mapping HTTP PATCH requests onto specific handler methods |

## Ressource Properties
Various properties can be specified inside your application.properties file, inside your application.yaml file, or as command line switches. 
[Common Application Properties](https://docs.spring.io/spring-boot/docs/current/reference/html/application-properties.html)
```
server.port=8585	## Server Port for HTTP server
```

## Simple RestController

```
@RestController
@RequestMapping("/api/v3")
public class FunRestController {

    @GetMapping("/")
    public String HelloWorld() {
        return "Hello World";
    }
}
```
Compile and test our application 
```
curl http://localhost:8080/api/V3/
```

# OpenAPI's for tesing 
## OpenWeather (openweathermap.org) 
```
api.openweathermap.org/data/2.5/weather?q={city name}
api.openweathermap.org/data/2.5/weather?q={city name},{country code}
```
## Open Government Data (opendata.swiss) 
[Open Government Data](https://www.meteoschweiz.admin.ch/service-und-publikationen/service/open-government-data.html)

[opendata.swiss Documentation](https://handbook.opendata.swiss/de/content/nutzen/api-nutzen.html)

```
curl https://ckan.opendata.swiss/api/3/action/package_search?fq=tags:economy | jq
curl curl 'https://ckan.opendata.swiss/api/3/action/package_search?fq=organization:bundesamt-fur-meteorologie-und-klimatologie-meteoschweiz' | jq -r 
```

# Data Binding
- Sometimes called Mapping Serialization / Deserialization Marshalling / Unmarshalling

## JSON Data Binding with Jackson
[The Jackson Project](https://github.com/FasterXML/jackson-databind)
- Spring uses the Jackson Project behind the scenes
- Jackson handles data binding between JSON and Java POJO
