# Spring AI Chat Bot with Streaming Support

Welcome to the Spring AI Chat Bot project! This application demonstrates how to create a chatbot with streaming capabilities using Spring AI and Spring Boot. By leveraging the power of Spring AI, I've built a robust and scalable solution for real-time AI-powered conversations.

## Project Overview

This project showcases the integration of Spring AI with Spring Boot to create a chatbot that supports both traditional request-response interactions and streaming responses. It's an excellent starting point for developers looking to implement AI-powered chat functionality in their Spring applications.


## Getting Started

To get started with this project, ensure you have Java 23 and Maven installed on your system. Then, follow these steps:

1. Set up your Anthropic API key:
    - Locate `application.properties` in the `src/main/resources` directory
    - Add the following line, replacing `your_api_key` with your actual Anthropic API key:
      ```
      spring.ai.anthropic.api-key=your_api_key
      ```
    - Specify that you want to use the Claude 3.7 Sonnet Model (or the model of your choice)
      ```
      spring.ai.anthropic.chat.options.model=claude-3-7-sonnet-latest
      ```

2. Build the project:
   ```
   mvn clean install
   ```

3. Run the application:
   ```
   mvn spring-boot:run
   ```

The application will start, and you'll be able to access the chat endpoints.

## How to Run the Application

Once the application is running, you can interact with it using the following endpoints:

1. Streaming chat (GET request):
   ```
   GET http://localhost:8080/stream?message=Your message here
   ```
2. Traditional chat (POST request):
   ```
   POST http://localhost:8080/chat?message=Your message here
   ```

For the purpose of this demo, I have served 2 static webpages to test the chatbot:
1. Streaming Chatbot

```
http://localhost:8080/stream.html
```
2. Traditional Chatbot
```
http://localhost:8080/index.html
```
You can also use tools like cURL, Postman, or create a simple frontend to interact with these endpoints. 

## Relevant Code Examples

### Chat Controller

The `ChatController` class is the heart of our application. It handles both traditional and streaming chat requests:

```java
@RestController
@CrossOrigin
public class ChatController {
    private final ChatClient chatClient;

    public ChatController(ChatClient.Builder builder) {
        this.chatClient = builder.build();
    }

    @PostMapping("/chat")
    public String chat(@RequestParam String message) {
        return chatClient.prompt()
                .user(message)
                .call()
                .content();
    }

    @GetMapping("/stream")
    public Flux<String> chatWithStream(@RequestParam String message) {
        return chatClient.prompt()
                .user(message)
                .stream()
                .content();
    }
}
```

This controller demonstrates two key methods:

1. `chat`: Handles traditional request-response interactions.
2. `chatWithStream`: Provides a streaming response using Spring WebFlux's `Flux`.

```

This class bootstraps the Spring application context and runs the embedded web server.

## Project Requirements

- Java 23
- Maven 3.6.3 or newer
- Spring Boot 3.3.4
- Spring AI 1.0.0-M2

- ## Dependencies

The project relies on the following key dependencies:

- `spring-boot-starter-web`: For building web applications with Spring MVC
- `spring-ai-anthropic-spring-boot-starter`: Spring AI starter for Anthropic's AI models
- `spring-boot-starter-test`: For testing Spring Boot applications

## Conclusion

This Spring AI Chat Bot project showcases the power and flexibility of Spring AI when integrated with Spring Boot. It provides a solid foundation for building AI-powered chat applications with both traditional and streaming capabilities.
