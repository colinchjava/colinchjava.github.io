---
layout: post
title: "Integrating Java Spring REST Docs with Swagger for API documentation"
description: " "
date: 2023-09-24
tags: [Java, SpringRESTDocs]
comments: true
share: true
---

When building RESTful APIs with Java using the Spring framework, documenting the API becomes crucial for better understanding and communication between teams. Two popular tools that can be used for API documentation are Spring REST Docs and Swagger. In this blog post, we will see how we can integrate the two to generate comprehensive and user-friendly API documentation.

## What is Spring REST Docs?

**Spring REST Docs** is a powerful tool that automatically generates documentation for your RESTful APIs based on your JUnit tests. It allows you to write concise and expressive documentation along with your test cases. It generates API documentation in various formats such as HTML, Markdown, and AsciiDoc.

## What is Swagger?

**Swagger** (now known as OpenAPI) is another widely used tool for API documentation. It provides a specification, written in YAML or JSON, that describes the API endpoints, input/output parameters, and other details. Swagger UI can then be used to visualize and explore the API documentation in a user-friendly way.

## Integrating Spring REST Docs with Swagger

To integrate Spring REST Docs with Swagger, we will make use of an intermediate format called **Asciidoctor**. Asciidoctor allows us to convert the Spring REST Docs-generated AsciiDoc documentation into the Swagger format (OpenAPI specification).

### Step 1: Configure Spring REST Docs

Before we can integrate with Swagger, we need to configure Spring REST Docs to generate AsciiDoc output.

```java
@RunWith(SpringRunner.class)
@WebMvcTest(UserController.class)
public class UserControllerTests {

    @Autowired
    private MockMvc mockMvc;

    @Test
    public void testCreateUser() throws Exception {
        mockMvc.perform(post("/api/users")
                .content("{\"name\":\"John Doe\",\"email\":\"johndoe@example.com\"}")
                .contentType(MediaType.APPLICATION_JSON))
                .andExpect(status().isOk())
                .andDo(document("create-user",
                        preprocessRequest(prettyPrint()),
                        preprocessResponse(prettyPrint()),
                        requestFields(
                                fieldWithPath("name").description("The name of the user"),
                                fieldWithPath("email").description("The email of the user")
                        ),
                        responseFields(
                                fieldWithPath("id").description("The ID of the created user")
                        )
                ));
    }
}
```

In this example, we are using Spring REST Docs to document the `createUser` API endpoint. We are specifying the request and response fields using the `requestFields` and `responseFields` methods. The generated documentation will be in AsciiDoc format.

### Step 2: Convert AsciiDoc to Swagger

To convert the generated AsciiDoc documentation to Swagger, we will need to use a tool called **asciidoctor-to-swagger**. This tool takes the AsciiDoc files and outputs the Swagger (OpenAPI) specification.

To install `asciidoctor-to-swagger`, you can use npm:

```
npm install -g asciidoctor-to-swagger
```

Once installed, run the following command to convert the AsciiDoc file to Swagger:

```
asciidoctor-to-swagger input.adoc output.yml
```

### Step 3: Use Swagger UI to visualize the documentation

Now that we have the Swagger specification file, we can use **Swagger UI** to visualize and explore the API documentation. Swagger UI is an interactive UI that allows users to interact with the API endpoints and see the documentation in a user-friendly way.

To use Swagger UI, you can follow these steps:

1. Download the Swagger UI distribution from the official Swagger GitHub repository.
2. Copy the contents of the `dist` folder from the downloaded distribution to your project's web server directory.
3. Edit the `index.html` file and set the `url` field to point to your Swagger specification file (`output.yml` in our case).

Once you have done the above steps, you can access the Swagger UI by opening the `index.html` file in your web browser.

## Conclusion

Integrating Java Spring REST Docs with Swagger helps in generating comprehensive and user-friendly API documentation. With Spring REST Docs, we can document the API endpoints and generate AsciiDoc documentation. By converting the AsciiDoc documentation to the Swagger format, we can then leverage Swagger UI to visualize and explore the API documentation. This integration provides a seamless workflow for documenting and sharing APIs in a consistent and easily consumable manner.

#Java #SpringRESTDocs #Swagger