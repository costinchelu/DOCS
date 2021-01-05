# Spring Boot Hello World Example – Thymeleaf

## Maven

```xml
pom.xml

<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" 
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 
         http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <artifactId>web-thymeleaf</artifactId>
    <packaging>jar</packaging>
    <name>Spring Boot Web Thymeleaf Example</name>
    <description>Spring Boot Web Thymeleaf Example</description>
    <version>1.0</version>

    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.1.2.RELEASE</version>
    </parent>

    <properties>
        <java.version>1.8</java.version>
        <bootstrap.version>4.2.1</bootstrap.version>
    </properties>

    <dependencies>

        <!-- web MVC-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>

        <!-- Thymeleaf -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-thymeleaf</artifactId>
        </dependency>

        <!-- test -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>

        <!-- hot swapping, disable cache for template, enable live reload -->
        
        <!--It may need aditional settings  for IntelliJ-->
        <!--https://mkyong.com/spring-boot/intellij-idea-spring-boot-template-reload-is-not-working/-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <optional>true</optional>
        </dependency>

        <!-- Optional, for bootstrap -->
        <dependency>
            <groupId>org.webjars</groupId>
            <artifactId>bootstrap</artifactId>
            <version>${bootstrap.version}</version>
        </dependency>

    </dependencies>
    <build>
        <plugins>

            <!-- Package as an executable jar/war -->
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
                <configuration>
                    <addResources>true</addResources>
                </configuration>
            </plugin>

            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-surefire-plugin</artifactId>
                <version>2.22.0</version>
            </plugin>

        </plugins>

    </build>
</project>
```

## Controller

```java
WelcomeController.java

package com.mkyong.controller;

import org.springframework.beans.factory.annotation.Value;
import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestParam;

import java.util.Arrays;
import java.util.List;

@Controller
public class WelcomeController {

    // inject via application.properties
    @Value("${welcome.message}")
    private String message;

    private List<String> tasks = Arrays.asList("a", "b", "c", "d", "e", "f", "g");

    @GetMapping("/")
    public String main(Model model) {
        model.addAttribute("message", message);
        model.addAttribute("tasks", tasks);

        return "welcome"; //view
    }

    // /hello?name=kotlin
    @GetMapping("/hello")
    public String mainWithParam(
            @RequestParam(name = "name", required = false, defaultValue = "") 
            String name, Model model) {

        model.addAttribute("message", name);

        return "welcome"; //view
    }
}
```

## App

```java
StartWebApplication.java

package com.mkyong;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class StartWebApplication {

    public static void main(String[] args) {
        SpringApplication.run(StartWebApplication.class, args);
    }
}
```

## Thymeleaf HTML

For Thymeleaf template files, put in `src/main/resources/templates/`

```java
src/main/resources/templates/welcome.html

<!DOCTYPE HTML>
<html lang="en" xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="utf-8">
    <meta name="viewport" 
    content="width=device-width, initial-scale=1, shrink-to-fit=no">

    <title>Spring Boot Thymeleaf Hello World Example</title>

    <link rel="stylesheet" th:href="@{webjars/bootstrap/4.2.1/css/bootstrap.min.css}"/>
    <link rel="stylesheet" th:href="@{/css/main.css}"/>
</head>

<body>
    <nav class="navbar navbar-expand-md navbar-dark bg-dark fixed-top">
        <a class="navbar-brand" href="#">Mkyong.com</a>
    </nav>

<main role="main" class="container">
    <div class="starter-template">
        <h1>Spring Boot Web Thymeleaf Example</h1>
        <h2>
            <span th:text="'Hello, ' + ${message}"></span>
        </h2>
    </div>

    <ol>
        <li th:each="task : ${tasks}" th:text="${task}"></li>
    </ol>
</main>



<script   
    type="text/javascript" th:src="@{webjars/bootstrap/4.2.1/js/bootstrap.min.js}">
</script>
</body>
</html>
```

## Application properties

`src/main/resources/application.properties`  

`welcome.message: Mkyong`

`spring.thymeleaf.cache=false`

## Static

```css
src/main/resources/static/css/main.css

body {
  padding-top: 5rem;
}
.starter-template {
  padding: 3rem 1.5rem;
  text-align: center;
}

h1{
    color:#0000FF;
}

h2{
    color:#FF0000;
}
```

## Unit Testing

`MockMvc` to test the Spring MVC controller.

```java
WelcomeControllerTest.java

package com.mkyong;

import com.mkyong.controller.WelcomeController;
import org.junit.Test;
import org.junit.runner.RunWith;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.autoconfigure.web.servlet.WebMvcTest;
import org.springframework.test.context.junit4.SpringRunner;
import org.springframework.test.web.servlet.MockMvc;
import org.springframework.test.web.servlet.MvcResult;
import org.springframework.test.web.servlet.ResultActions;
import org.springframework.web.servlet.ModelAndView;

import java.util.Arrays;
import java.util.List;

import static org.hamcrest.Matchers.containsString;
import static org.hamcrest.Matchers.is;
import static org.hamcrest.core.IsEqual.equalTo;
import static org.springframework.test.web.servlet.request.MockMvcRequestBuilders.get;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.*;

@RunWith(SpringRunner.class)
@WebMvcTest(controllers = WelcomeController.class)
public class WelcomeControllerTest {

    @Autowired
    private MockMvc mockMvc;

    List<String> expectedList = Arrays.asList("a", "b", "c", "d", "e", "f", "g");

    @Test
    public void main() throws Exception {
        ResultActions resultActions = mockMvc.perform(get("/"))
                .andExpect(status().isOk())
                .andExpect(view().name("welcome"))
                .andExpect(model().attribute("message", equalTo("Mkyong")))
                .andExpect(model().attribute("tasks", is(expectedList)))
                .andExpect(content().string(containsString("Hello, Mkyong")));

        MvcResult mvcResult = resultActions.andReturn();
        ModelAndView mv = mvcResult.getModelAndView();
        //
    }

    // Get request with Param
    @Test
    public void hello() throws Exception {
        mockMvc.perform(get("/hello").param("name", "I Love Kotlin!"))
                .andExpect(status().isOk())
                .andExpect(view().name("welcome"))
                .andExpect(model().attribute("message", equalTo("I Love Kotlin!")))
                .andExpect(content().string(containsString("Hello, I Love Kotlin!")));
    }


}
```
