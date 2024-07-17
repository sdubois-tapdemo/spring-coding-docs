# Thymeleaf Example Project

## JPA Project Setup
```
src/
├── main/
│   └── java/
|       ├── Application.java
|       ├── controller/
|       |   └── StudentController.java
|       └── model/
|           └── Student.java
└── resources/
    |-- statuc.css/
    |     └── demo.css
    |-- templates/
    |     └── student-confirmation.html
    |     └── student-form.html
    └── application.properties
```

## Model
### Student (Student.java)
```
package com.luv2code.springboot.thymdleafdemo.model;

import org.springframework.stereotype.Component;

import java.util.List;

public class Student {
    private String firstName;
    private String lastName;
    private String country;
    private String favoriteLanguage;
    private List<String> favoriteSystems;

    public Student() {

    }

    public String getCountry() {
        return country;
    }

    public void setCountry(String country) {
        this.country = country;
    }

    public String getFirstName() {
        return firstName;
    }

    public String getLastName() {
        return lastName;
    }

    public void setFirstName(String firstName) {
        this.firstName = firstName;
    }

    public void setLastName(String lastName) {
        this.lastName = lastName;
    }

    public String getFavoriteLanguage() {
        return favoriteLanguage;
    }

    public void setFavoriteLanguage(String favoriteLanguage) {
        this.favoriteLanguage = favoriteLanguage;
    }

    public List<String> getFavoriteSystems() {
        return favoriteSystems;
    }

    public void setFavoriteSystems(List<String> favoriteSystems) {
        this.favoriteSystems = favoriteSystems;
    }
}

```


## Rest Controller
### Student Controller (StudentController.java)
```
package com.luv2code.springboot.thymdleafdemo.controller;

import com.luv2code.springboot.thymdleafdemo.model.Student;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.ModelAttribute;
import org.springframework.web.bind.annotation.PostMapping;

import java.util.List;

@Controller
public class StudentController {
    @Value("${countries}")
    private List<String> countries;
    @Value("${languages}")
    private List<String> languages;

    @Value("${systems}")
    private List<String> systems;

    @GetMapping("/showStudentForm")
    public String showForm(Model theModel) {
        // create a new student object
        Student theStudent = new Student();

        // add the student object to the model
        theModel.addAttribute("student", theStudent);

        // add a list of countries to the model
        theModel.addAttribute("countries", countries);

        // Add a list of languages to the model
        theModel.addAttribute("languages", languages);

        // Add a list of systems to the model
        theModel.addAttribute("systems", systems);

        return "student-form";
    }

    @PostMapping("/processStudentForm")
    public String processStudentForm(@ModelAttribute("student") Student theStudent) {
        // log the input data
        System.out.println("Student: " + theStudent.getFirstName() + " " + theStudent.getLastName());

        return "student-confirmation";
    }
}

```

## Templates
### Student Confirmation (student-confirmation.haml)
```
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.tymeleaf.org">
<head>
    <meta charset="UTF-8">
    <title>Student Confirmation</title>
</head>
<body>
<h3>Student Confirmation</h3>

The Student is confirmed: <span th:text="${student.firstName} + ' ' + ${student.lastName}"/>
<br><br>
Country: <span th:text="${student.country}"/>
<br><br>
Favorite Programming Language: <span th:text="${student.favoriteLanguage}"/>
<br><br>
Favorite Operating Systems: <ul>
    <li th:each="tempSystem : ${student.favoriteSystems}" th:text="${tempSystem}"/>
</ul>

<br><br>

</body>
</html>
```

## Student Form (student-form.haml)

```
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.tymeleaf.org">
<head>
    <meta charset="UTF-8">
    <title>Student Registration Form</title>
</head>
<body>
<h3>Student Registration Form</h3>
<form th:action="@{/processStudentForm}" th:object="${student}" method="POST">
    First Name: <input type="text" th:field="*{firstName}" />
    <br><br>
    Last Name: <input type="text" th:field="*{lastName}" />
    <br><br>
    Country:
    <!-- Thymeleaf Drop Down List with values from application.properties -->
    <select th:field="*{country}">
        <option th:each="tempCountry : ${countries}" th:value="${tempCountry}" th:text="${tempCountry}" />
    </select>

    <!-- HTML Drop Down List
    <select name="country">
        <option value="Brazil">Brazil</option>
        <option value="France">France</option>
        <option value="Germany">Germany</option>
        <option value="India">India</option>
    </select>  -->

    <br><br>
    Favorite Programming Language:
    <input type="radio" th:field="*{favoriteLanguage}" th:each="tempLang : ${languages}" th:value="${tempLang}" th:text="${tempLang}" />

    <!-- HTML Radio Bottons
    <input type="radio" th:field="*{favoriteLanguage}" th:value="Go">Go</input>
    <input type="radio" th:field="*{favoriteLanguage}" th:value="Java">Java</input>
    <input type="radio" th:field="*{favoriteLanguage}" th:value="Python">Python</input>
    -->

    <br><br>

    Favorite Operating Systems:
    <input type="checkbox" th:field="*{favoriteSystems}" th:each="tempSystem : ${systems}" th:value="${tempSystem}" th:text="${tempSystem}" />

    <!-- HTML Checkboxes
    <input type="checkbox" th:field="*{favoriteSystems}" th:value="Linux">Linux</input>
    <input type="checkbox" th:field="*{favoriteSystems}" th:value="macOS">macOS</input>
    <input type="checkbox" th:field="*{favoriteSystems}" th:value="'Microsoft Windows'">Microsoft Windows</input>
    -->
    <br><br>

    <input type="submit" value="Submit">
    <br><br>

</form>

</body>
</html>
```

## CSS Stylesheats
### Demo Stylesheet (demo.css)
```
.funny {
    font-style: italic;
    color: green;
}
```
