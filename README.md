# Building AI Applications with Spring AI and Azure OpenAI

Author: Ayush Shrivastava

------------------------------------------------------------------------

## 1. What is Spring AI?

Spring AI is a Spring ecosystem project that helps developers build
AI-powered applications using simple and familiar Spring Boot concepts.

It provides integration with popular AI providers like OpenAI and Azure
OpenAI. Instead of writing complex HTTP calls manually, Spring AI gives
you ready-to-use abstractions like ChatClient, EmbeddingClient, and
more.

If you already know Spring Boot, you can easily start building AI
applications without learning new complicated frameworks.

------------------------------------------------------------------------

## 2. Why Do We Need Spring AI?

Before Spring AI: - Developers had to manually call REST APIs. - They
had to handle authentication, request bodies, and response parsing. -
Code became complex and hard to maintain.

With Spring AI: - Configuration is simple. - Dependency injection works
as usual. - AI calls look clean and readable. - It integrates smoothly
with Spring Boot projects.

------------------------------------------------------------------------

## 3. Core Features of Spring AI

### 1. ChatClient

Used for sending prompts and receiving AI-generated responses.

### 2. Model Abstraction

Supports multiple AI providers without changing much code.

### 3. Auto Configuration

Works with Spring Boot auto-configuration.

### 4. Simple Prompt Handling

Send a message and receive content in a few lines of code.

### 5. Integration Friendly

Works well with REST APIs, databases, microservices, and cloud
deployments.

------------------------------------------------------------------------

## 4. Project Setup Explanation

Let us understand your project step by step.

------------------------------------------------------------------------

## 5. Maven Dependencies Explained

Your project uses:

### Parent

Spring Boot Parent: Provides dependency management and plugin
configurations.

### Spring Web MVC

Used to create REST APIs.

### Spring AI Azure OpenAI Starter

This dependency connects your application with Azure OpenAI service.

### DevTools

Used for development-time auto restart.

### Test Dependency

Used for writing test cases.

### Spring AI BOM

This manages compatible versions of Spring AI libraries.

------------------------------------------------------------------------

## 6. application.properties Explanation

spring.application.name=openai

spring.ai.azure.openai.api-key=${AZURE_OPENAI_API_KEY} spring.ai.azure.openai.endpoint=${AZURE_OPENAI_ENDPOINT}
spring.ai.azure.openai.chat.options.deployment-name=\${AZURE_OPENAI_DEPLOYMENT}
spring.ai.azure.openai.chat.options.temperature=1

Explanation:

-   application.name: Name of the application.
-   api-key: Azure OpenAI API key taken from environment variable.
-   endpoint: Azure endpoint URL.
-   deployment-name: Your deployed model name in Azure.
-   temperature: Controls creativity of the AI (1 means moderate
    creativity).

Using environment variables is a secure way to manage secrets.

------------------------------------------------------------------------

## 7. Main Application Class

@SpringBootApplication public class OpenaiApplication {

    public static void main(String[] args) {
        SpringApplication.run(OpenaiApplication.class, args);
    }

}

Explanation:

-   @SpringBootApplication enables auto configuration and component
    scanning.
-   SpringApplication.run starts the application.

This is the entry point of your Spring Boot application.

------------------------------------------------------------------------

## 8. Chat Controller Explained

@RestController @RequestMapping("/api") public class ChatController {

    private final ChatClient chatClient;

    public ChatController(ChatClient.Builder chatClientBuilder) {
        this.chatClient = chatClientBuilder.build();
    }

    @GetMapping("/chat")
    public String chat(@RequestParam("message") String message) {
        return chatClient
                .prompt(message)
                .call()
                .content();
    }

}

Let us break it down:

### @RestController

Marks the class as a REST controller.

### @RequestMapping("/api")

Base URL path for all APIs in this controller.

### ChatClient Injection

Spring automatically provides a ChatClient builder. We build it using
chatClientBuilder.build().

### /chat Endpoint

This endpoint accepts a query parameter called "message".

Example:

http://localhost:8080/api/chat?message=Hello

### How It Works Internally

1.  User sends a message.
2.  chatClient.prompt(message) sends prompt to Azure OpenAI.
3.  call() executes the request.
4.  content() extracts only the AI response text.
5.  The response is returned to the client.

Very clean and simple.

------------------------------------------------------------------------

## 9. How to Run This Project

Step 1: Set environment variables

On Windows:

set AZURE_OPENAI_API_KEY=your_key\
set AZURE_OPENAI_ENDPOINT=your_endpoint\
set AZURE_OPENAI_DEPLOYMENT=your_model_name

Step 2: Run the application

mvn spring-boot:run

Step 3: Test using browser or Postman

http://localhost:8080/api/chat?message=What is Java?

You will receive an AI-generated response.

------------------------------------------------------------------------

## 10. What You Have Built

You have built:

-   A REST API
-   Connected to Azure OpenAI
-   Using Spring AI abstraction
-   With secure configuration using environment variables

This is a production-ready base for:

-   AI Chatbot
-   AI FAQ system
-   AI-powered backend
-   Developer assistant
-   Content generator

------------------------------------------------------------------------

## 11. Next Level Improvements

You can improve this project by:

-   Adding system prompts
-   Storing chat history in database
-   Creating streaming responses
-   Adding authentication
-   Building a frontend using React or Thymeleaf
-   Converting it into a microservice

------------------------------------------------------------------------

## 12. Final Summary

Spring AI makes AI integration simple for Spring Boot developers.

Your current project: - Uses Spring Boot 4 - Uses Spring AI 2.0.0-M2 -
Connects to Azure OpenAI - Exposes a clean REST endpoint - Follows
secure configuration practices

With very little code, you have enabled powerful AI capabilities inside
your backend application.

This is the modern way of building intelligent backend systems using
Java and Spring Boot.
