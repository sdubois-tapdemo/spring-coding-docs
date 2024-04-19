# Thymeleaf
Thymeleaf is a modern server-side Java template engine for both web and standalone environments.

Thymeleaf's main goal is to bring elegant natural templates to your development workflow — HTML that can be correctly displayed in browsers and also work as static prototypes, allowing for stronger collaboration in development teams.

With modules for Spring Framework, a host of integrations with your favourite tools, and the ability to plug in your own functionality, Thymeleaf is ideal for modern-day HTML5 JVM web development — although there is much more it can do.
[Thymeleaf](www.thymeleaf.org)

## What is Thymeleaf?
- Thymeleaf is a Java templating engine
- Commonly used to generate the HTML views for web apps
- However, it is a general purpose templating engine
- Can use Thymeleaf outside of web apps (more on this later)

## Top Competitors and Alternatives of Thymeleaf
(Top Competitors and Alternatives of Thymeleaf)[https://6sense.com/tech/javascript-mvc-framework/thymeleaf-market-share#])

## Annotations

| Annotation | Description |
| --- | --- |
| @NoArgsConstructor | will generate a default constructor without any parameter |
| @AllArgsConstructor | will generate a constructor with all parameters in the sequence, they are present in class |
| @RequiredArgsConstructor | will generate a constructor for only required fields which have @NotNull annotation |

# Thymeleaf Example Project

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
