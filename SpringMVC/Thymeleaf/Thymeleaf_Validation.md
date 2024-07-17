# Thymeleaf Example Project with Validation

## JPA Project Setup
```
src/
├── main/
│   └── java/
|       ├── Application.java
|       ├── controller/
|       |   └── CustomerController.java
|       ├── validation/
|       |   └── CourseCode.java
|       |   └── CourseCodeConstraintValidator.java
|       └── model/
|           └── Customer.java
└── resources/
    |-- messages.properties
    └── application.properties
```

## Model
### Customer (Customer.java)
```
package com.luv2code.springdemo.mvc;

import com.luv2code.springdemo.mvc.validation.CourseCode;
import jakarta.validation.constraints.*;

public class Customer {
    private String firstName;

    @NotNull(message="is required")
    @Size(min=1, message="is required")
    private String lastName;

    @NotNull(message="is required")
    @Min(value=0, message = "must be greater than or equal to zero")
    @Max(value=10, message = "must be less than or equal to 10")
    private Integer freePasses;

    @Pattern(regexp="^[a-zA-Z0-9]{5}", message="only 5 chars/digits")
    private String postalCode;


    @CourseCode(value = "TOP", message = "must start with TOP")
    private String courseCode;

    public String getFirstName() {
        return firstName;
    }

    public void setFirstName(String firstName) {
        this.firstName = firstName;
    }

    public String getLastName() {
        return lastName;
    }

    public void setLastName(String lastName) {
        this.lastName = lastName;
    }

    public Integer getFreePasses() {
        return freePasses;
    }

    public void setFreePasses(Integer freePasses) {
        this.freePasses = freePasses;
    }

    public String getPostalCode() {
        return postalCode;
    }

    public void setPostalCode(String postalCode) {
        this.postalCode = postalCode;
    }

    public String getCourseCode() {
        return courseCode;
    }

    public void setCourseCode(String courseCode) {
        this.courseCode = courseCode;
    }
}
```


## Rest Controller
### Customer Controller (CustomerController.java)
```
package com.luv2code.springdemo.mvc;

import jakarta.validation.Valid;
import org.springframework.beans.propertyeditors.StringTrimmerEditor;
import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.validation.BindingResult;
import org.springframework.web.bind.WebDataBinder;
import org.springframework.web.bind.annotation.*;

@Controller
public class CustomerController {
    // add an initbinder to remove leading and tailing whitespaces
    @InitBinder
    public void initBinder(WebDataBinder dataBinder) {
        StringTrimmerEditor stringTrimmerEditor = new StringTrimmerEditor(true);
        dataBinder.registerCustomEditor(String.class, stringTrimmerEditor);
    }

    @GetMapping("/")
    public String showForm(Model theModel) {

        theModel.addAttribute("customer", new Customer());

        return "customer-form";
    }

    @PostMapping("/processForm")
    public String processform(
        @Valid @ModelAttribute("customer") Customer theCustomer, BindingResult theBindingResult) {

        System.out.println("First Name: [" + theCustomer.getFirstName() + "]");
        System.out.println("Last Name:  [" + theCustomer.getLastName() + "]");
        System.out.println("Binding Resultss: " + theBindingResult.toString());
        System.out.println("\\n\\n\\n\\n");
        if(theBindingResult.hasErrors()) {
            return "customer-form";
        } else {
            return "customer-confirmation";
        }
    }
}
```

## Validation Package
### Validation (CourseCode.java)
```
package com.luv2code.springdemo.mvc.validation;

import ch.qos.logback.core.net.server.Client;
import jakarta.validation.Constraint;
import jakarta.validation.Payload;

import java.lang.annotation.ElementType;
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;
import java.lang.annotation.Target;

@Constraint(validatedBy = CourseCodeConstraintValidator.class)
@Target({ElementType.METHOD, ElementType.FIELD})
@Retention(RetentionPolicy.RUNTIME)
public @interface CourseCode {
    // define default course code
    public String value() default "LUV";

    // define default error message
    public String message() default "must start with LUV";

    // define default groups
    public Class<?>[] groups() default {};

    // define default payloads
    public Class<? extends Payload>[] payload() default {};
}
```

### Validation Constraint (CourseCodeConstraintValidator.java)
```
package com.luv2code.springdemo.mvc.validation;

import jakarta.validation.ConstraintValidator;
import jakarta.validation.ConstraintValidatorContext;

public class CourseCodeConstraintValidator implements ConstraintValidator<CourseCode,String> {
    private String coursePrefix;

    @Override
    public void initialize(CourseCode courseCode) {
        coursePrefix = courseCode.value();
    }

    @Override
    public boolean isValid(String code, ConstraintValidatorContext constraintValidatorContext) {
        boolean result;

        if (code != null) {
            result = code.startsWith(coursePrefix);
        } else {
            result = true;
        }

        return result;
    }
}
```



## Templates
### Customer Confirmation (customer-confirmation.haml)
```
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <title>Customer Confirmation</title>
</head>
<body>
The Customer is Confirmed: <span th:text="${customer.firstName} + ' ' + ${customer.lastName}" />
<br><br>
Free Passes: <span th:text="${customer.freePasses}" />
Postal Code: <span th:text="${customer.postalCode}" />
Course Code: <span th:text="${customer.courseCode}" />

</body>
</html>
```

## Customer Form (customer-form.haml)
```
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <title>Customer Registration Form</title>
    <!-- Server side form validation Styles -->
    <style>
        .error (color:red)
    </style>

    <!-- CLient side form validation Styles -->
    <style>
        form {
          font: 1em sans-serif;
          max-width: 320px;
        }

        p > label {
          display: block;
        }

        input[type="text"],
        input[type="email"],
        input[type="number"],
        textarea,
        fieldset {
          width: 100%;
          border: 1px solid #333;
          box-sizing: border-box;
        }

        input:invalid {
          box-shadow: 0 0 5px 1px red;
        }

        input:focus:invalid {
          box-shadow: none;
        }
    </style>
</head>
<body>

<h2>Server-side form validation</h2>

<i>Fill out the Form. Asterisk (*) means required.</i>

<form th:action="@{/processForm}" th:object="${customer}" method="POST">
    First name: <input type="text" th:field="*{firstName}" />
    <br><br>

    Last name (*): <input type="text" th:field="*{lastName}" />
    <!-- Show error message (if present) -->
    <span th:if="${#fields.hasErrors('lastName')}"
          th:errors="*{lastName}"
          class="error"></span>
    <br><br>

    Free Pass: <input type="text" th:field="*{freePasses}" />
    <!-- Show error message (if present) -->
    <span th:if="${#fields.hasErrors('freePasses')}"
          th:errors="*{freePasses}"
          class="error"></span>
    <br><br>

    Postal Code: <input type="text" th:field="*{postalCode}" />
    <!-- Show error message (if present) -->
    <span th:if="${#fields.hasErrors('postalCode')}"
          th:errors="*{postalCode}"
          class="error"></span>
    <br><br>

    Course Code: <input type="text" th:field="*{courseCode}" />
    <!-- Show error message (if present) -->
    <span th:if="${#fields.hasErrors('courseCode')}"
          th:errors="*{courseCode}"
          class="error"></span>
    <br><br>

    <input type="submit" value="Submit" />
</form>

<br><br>

<h2>Client-side form validation</h2>
<!-- CLient side form validation -->
<form>
    <fieldset>
        <legend>
            Do you have a driver's license?<span aria-label="required">*</span>
        </legend>
        <!-- While only one radio button in a same-named group can be selected at a time,
             and therefore only one radio button in a same-named group having the "required"
             attribute suffices in making a selection a requirement -->
        <input type="radio" required name="driver" id="r1" value="yes" /><label
            for="r1"
    >Yes</label
    >
        <input type="radio" required name="driver" id="r2" value="no" /><label
            for="r2"
    >No</label
    >
    </fieldset>
    <p>
        <label for="n1">How old are you?</label>
        <!-- The pattern attribute can act as a fallback for browsers which
             don't implement the number input type but support the pattern attribute.
             Please note that browsers that support the pattern attribute will make it
             fail silently when used with a number field.
             Its usage here acts only as a fallback -->
        <input
                type="number"
                min="12"
                max="120"
                step="1"
                id="n1"
                name="age"
                pattern="\d+" />
    </p>
    <p>
        <label for="t1"
        >What's your favorite fruit?<span aria-label="required">*</span></label
        >
        <input
                type="text"
                id="t1"
                name="fruit"
                list="l1"
                required
                pattern="[Bb]anana|[Cc]herry|[Aa]pple|[Ss]trawberry|[Ll]emon|[Oo]range" />
        <datalist id="l1">
            <option>Banana</option>
            <option>Cherry</option>
            <option>Apple</option>
            <option>Strawberry</option>
            <option>Lemon</option>
            <option>Orange</option>
        </datalist>
    </p>
    <p>
        <label for="t2">What's your email address?</label>
        <input type="email" id="t2" name="email" />
    </p>
    <p>
        <label for="t3">Leave a short message</label>
        <textarea id="t3" name="msg" maxlength="140" rows="5"></textarea>
    </p>
    <p>
        <button>Submit</button>
    </p>
</form></form>

</body>
</html>
```

## Properties
### Application Properties (application.properties)
```
spring.application.name=validationdemo
```

### Messages Properties (messages.properties)
```
# Web Error message:
# Failed to convert property value of type java.lang.String to required type java.lang.Integer for property freePasses; For input string: "asdcasdcasdc"
# Spring Trace Errors:
# Binding Resultss: org.springframework.validation.BeanPropertyBindingResult: 1 errors
# Field error in object 'customer' on field 'freePasses': rejected value [gagadu]; codes [typeMismatch.customer.freePasses,typeMismatch.freePasses,typeMismatch.java.lang.Integer,typeMismatch]; arguments [org.springframework.context.support.DefaultMessageSourceResolvable: codes [customer.freePasses,freePasses]; arguments []; default message [freePasses]]; default message [Failed to convert property value of type 'java.lang.String' to required type 'java.lang.Integer' for property 'freePasses'; For input string: "gagadu"]

# <errornam>.<attrib>.<fieldnam>.<Message>
typeMismatch.customer.freePasses=Invalid Number
typeMismatch.freePasses=Error Message for all Attributes with name 'freePasses'
typeMismatch.java.lang.Integer=Error Messge for all Integer Missmatches
```

