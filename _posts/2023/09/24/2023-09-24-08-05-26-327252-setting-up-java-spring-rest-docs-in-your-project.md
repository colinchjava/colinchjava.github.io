---
layout: post
title: "Setting up Java Spring REST Docs in your project"
description: " "
date: 2023-09-24
tags: [Documentation]
comments: true
share: true
---

If you are developing a Java Spring project that includes RESTful APIs, documenting those APIs is essential for both developers and stakeholders. One popular tool for API documentation in Java Spring is **REST Docs**. REST Docs allows you to generate documentation directly from your API tests, ensuring that your documentation is always up to date.

In this blog post, we will guide you through the process of setting up REST Docs in your Java Spring project.

## Prerequisites
Before you get started, make sure you have the following prerequisites:
- A Java Spring project set up and running.
- API tests using a testing framework such as JUnit or Spock.

## Step 1: Add REST Docs Dependencies
To start using REST Docs, you need to add its dependencies to your project. Open your project's `pom.xml` file and add the following dependencies:

```xml
<dependency>
    <groupId>org.springframework.restdocs</groupId>
    <artifactId>spring-restdocs-mockmvc</artifactId>
    <version><!-- latest version --></version>
    <scope>test</scope>
</dependency>

<dependency>
    <groupId>io.rest-assured</groupId>
    <artifactId>spring-mock-mvc</artifactId>
    <version><!-- latest version --></version>
    <scope>test</scope>
</dependency>
```

Make sure to replace `<!-- latest version -->` with the latest version of the dependencies.

## Step 2: Write API Tests with REST Docs
Now, let's start writing API tests that generate the documentation using REST Docs. Create a new test class for your API endpoints and annotate it with `@RunWith` and `@SpringBootTest` to enable Spring Boot testing.

Here's an example of an API test using JUnit:

```java
@RunWith(SpringRunner.class)
@SpringBootTest
public class UserApiTest {

    @Autowired
    private MockMvc mockMvc;

    @Rule
    public JUnitRestDocumentation restDocumentation = new JUnitRestDocumentation();

    @Before
    public void setUp() {
        this.mockMvc = MockMvcBuilders
                .webAppContextSetup(...)
                .apply(documentationConfiguration(this.restDocumentation))
                .build();
    }

    @Test
    public void testGetUserById() throws Exception {
        // Write your test code here
        mockMvc.perform(get("/users/{id}", 1))
                .andExpect(status().isOk())
                .andDo(document("getUserById"));
    }
}
```

In this example, we are using JUnit, but the steps are similar for other testing frameworks.

## Step 3: Generate API Documentation
To generate the API documentation, run your API tests. REST Docs will automatically generate documentation snippets as part of the test execution. These snippets can be combined later to generate a complete documentation in a desired format, such as HTML, PDF, or Markdown.

## Step 4: Combine Snippets and Generate Documentation
After running your tests, REST Docs generates snippets under a directory called `build/generated-snippets`. You can find separate snippets for request, response, and path parameters, among others.

To combine and generate a complete documentation, use the `asciidoctor-maven-plugin` or `asciidoctor-gradle-plugin` in your build configuration. These plugins allow you to specify the output format and location for your documentation.

## Conclusion
By setting up Java Spring REST Docs in your project, you can easily generate up-to-date API documentation directly from your tests. This ensures that your documentation stays in sync with your API implementation. With proper documentation, both developers and stakeholders can easily understand and consume your APIs.

#API #Documentation