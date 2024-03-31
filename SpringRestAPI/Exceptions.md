# Exceptions

## HTTP Response - Status Codes
| Code Range | Description |
| --- | --- |
| 100 - 199 | Informational |
| 200 - 299 | Successful |
| 300 - 399 | Redirection |
| 400 - 499 | Client error |
| 500 - 599 | Server Error |


401 Authentication Required
404 File Not Found
500 Internal Server Error

## Annotations
| Name | Description |
| --- | --- |
| @ExceptionHandler | ExceptionHandler |
| @ControllerAdvice | is similar to an interceptor / filter |


## RestAPI Project Setup
```
project
  |__ pom.xml
  |__ src
  |    |__ main
  |    |    |__ java
  |    |    |      |__ com.tanzu.demo
  |    |    |               |__ DemoApplication.java                  // Application Properties
  |    |    |               |__ rest                              
  |    |    |                     |__ DemoRestController.java         // Data Access Object (DOA) Interface
  |    |    |               |__ exception                          
  |    |    |                     |__ ResourceConflictException.java  // Data Access Object (DOA) Interface
  |    |    |                     |__ ResourceNotFoundException.java  // Define DAO implementation for Student
  |    |    |               |__ entity                           
  |    |    |                     |__ Student.java                    // JPA Entity for Student
  |    |    |__ resources
  |    |           |__ application.properties                         // Application Properties
  |    |           |__ static                                         // HTML Files, CSS, JavaScript, imges, etc.
  |    |           |__ templates                                      // Auto Configuration Templates (Mustache, FreeMarker, Thymeleaf)
  |    |
  |    |__ test
  |         |__ java
  |
  |__ target

```

# Exceptions Example

## Exception Handler (NOT_FOUND and BAD_REQUEST)
```
    @GetMapping("/student/{studentId}")
    private Student getStudent(@PathVariable int studentId) {

        // just index into the list
        System.out.println("StudentId: " + studentId);
        System.out.println("theStudents Size: " +  theStudents.size());

        // check student id agains list size
        if ((studentId >= theStudents.size()) || (studentId < 0)) {
            throw new StudentNotFoundException("Student not Found with Id: " + studentId);
        }
        return theStudents.get(studentId);
    }

    @ExceptionHandler
    public ResponseEntity<StudentErrorResponse> HandleException(StudentNotFoundException exc) {
        System.out.println("Handle Exception: StudentNotFoundException");

        // create a studenetErrorRespnse
        StudentErrorResponse error = new StudentErrorResponse();
        error.setMessage(exc.getMessage());
        error.setStatus(HttpStatus.NOT_FOUND.value());
        error.setTimeStamp(System.currentTimeMillis());

        // return a response Entty
        return new ResponseEntity<>(error, HttpStatus.NOT_FOUND);
    }

    // add another exception handler ... to catch any exception (catch all)
    @ExceptionHandler
    public ResponseEntity<StudentErrorResponse> HandleException(Exception exc) {
        System.out.println("Handle All remaining Exceptions: Exception");

        // create a studenetErrorRespnse
        StudentErrorResponse error = new StudentErrorResponse();

        error.setMessage(exc.getMessage());
        error.setStatus(HttpStatus.BAD_REQUEST.value());
        error.setTimeStamp(System.currentTimeMillis());

        // return a response Entty
        return new ResponseEntity<>(error, HttpStatus.BAD_REQUEST);
    }
```

## Global Exception Handling

- @ControllerAdvice is similar to an interceptor / filter 
- Pre-process requests to controllers
- Post-process responses to handle exceptions 
- Perfect for global exception handling

```
@ControllerAdvice
public class StudentRestExceptionHandler {
    // Add an exception Handlewr
    @ExceptionHandler
    public ResponseEntity<StudentErrorResponse> HandleException(StudentNotFoundException exc) {
        System.out.println("Handle Exception: StudentNotFoundException");

        // create a studenetErrorRespnse
        StudentErrorResponse error = new StudentErrorResponse();

        error.setMessage(exc.getMessage());
        error.setStatus(HttpStatus.NOT_FOUND.value());
        error.setTimeStamp(System.currentTimeMillis());

        // return a response Entty
        return new ResponseEntity<>(error, HttpStatus.NOT_FOUND);
    }

    // add another exception handler ... to catch any exception (catch all)
    @ExceptionHandler
    public ResponseEntity<StudentErrorResponse> HandleException(Exception exc) {
        System.out.println("Handle All remaining Exceptions: Exception");

        // create a studenetErrorRespnse
        StudentErrorResponse error = new StudentErrorResponse();

        error.setMessage(exc.getMessage());
        error.setStatus(HttpStatus.BAD_REQUEST.value());
        error.setTimeStamp(System.currentTimeMillis());

        // return a response Entty
        return new ResponseEntity<>(error, HttpStatus.BAD_REQUEST);
    }
}
```



