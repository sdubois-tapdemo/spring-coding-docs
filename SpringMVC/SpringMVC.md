# SpringMVC
xxx
[Thymeleaf](www.thymeleaf.org)

## Components of a Spring MVC Application
- A set of web pages to layout UI components
- A collection of Spring beans (controllers, services, etc…)
- Spring configuration (XML, Annotations or Java)

## View Technologies
The use of view technologies in Spring MVC is pluggable. Whether you decide to use Thymeleaf, Groovy Markup Templates, JSPs, or other technologies is primarily a matter of a configuration change. This chapter covers view technologies integrated with Spring MVC. We assume you are already familiar with View Resolution.
[SpringMVC View Technologies](https://docs.spring.io/spring-framework/reference/web/webmvc-view.html)

- Thymeleaf
- FreeMarker
- Groovy Markup
- Script Views
- JSP and JSTL
- RSS and Atom
- PDF and Excel
- Jackson
- XML Marshalling
- XSLT Views

## Annotations

| Annotation | Description |
| --- | --- |
| @RequestMapping | will support any HTTP request (GET, POST etc.) |
| @GetMapping | Requests data from given resource |
| @PostMapping | Submits data to given resource |

## HTTP Request / Response
### Handling Form Submission
- This mapping handles ALL HTTP methods
- GET, POST, etc …
```
@RequestMapping("/processForm")
public String processForm(...) {
}
```
Constrain the Request Mapping - GET
- This mapping ONLY handles GET method
- Any other HTTP REQUEST method will get rejected
```
@RequestMapping(path="/processForm", method=RequestMethod.GET)
public String processForm(...) {
}
```

### Sending Data with GET method
- Form data is added to end of URL as name/value pairs
- theUrl?field1=value1&field2=value2…
```
<form th:action=“@{/processForm}” method="GET" …>
…
</form>
```

Annotation Short-Cut
- @GetMapping: this mapping ONLY handles GET method
- Any other HTTP REQUEST method will get rejected
```
@GetMapping("/processForm")
public String processForm(...) {
...
}
```

### Sending Data with POST method
- Form data is passed in the body of HTTP request message
```
<form th:action=“@{/processForm}” method="POST" …>
…
</form>
```
Constrain the Request Mapping - POST
- This mapping ONLY handles POST method
- Any other HTTP REQUEST method will get rejected
```
@RequestMapping(path="/processForm", method=RequestMethod.POST)
public String processForm(...) {
...
}
```

Annotation Short-Cut
- @PostMapping: This mapping ONLY handles POST method
- Any other HTTP REQUEST method will get rejected
...
@PostMapping("/processForm")
public String processForm(...) {
...
}
...

## Spring MVC Form Validation
- Java has a standard Bean Validation API
- Defines a metadata model and API for entity validation
- Spring Boot and Thymeleaf also support the Bean Validation API
(Jakarta Bean Validation)[https://beanvalidation.org/] (Jakarta Bean Validation specification
)[https://jakarta.ee/specifications/bean-validation/3.0/jakarta-bean-validation-spec-3.0.html#constraintsdefinitionimplementation]

## Java’s Standard Bean Validation API
- Java has a standard Bean Validation API
- Defines a metadata model and API for entity validation
- Spring Boot and Thymeleaf also support the Bean Validation API
(Jakarta Bean Validation)[https://beanvalidation.org/] (Jakarta Bean Validation specification
)[https://jakarta.ee/specifications/bean-validation/3.0/jakarta-bean-validation-spec-3.0.html#constraintsdefinitionimplementation]

| Annotation | Description |
| --- | --- |
| @NotNull | Checks that the annotated value is not null |
| @Min | Must be a number >= value |
| @Max | Must be a number <= value |
| @Size | Size must much the given size |
| @Pattern | Must match a regular expresseion pattern |
| @Future / @Past | Data must be in future or past of given date |






