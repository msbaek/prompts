# Guidelines for Spring Boot Development

This file contains guidelines for Coding Agent to follow when working on this Spring Boot project. Adhering to these standards ensures consistency, maintainability, and leverages modern practices.

## Core Technologies & Versions

- **Java:** Use the latest Long-Term Support (LTS) version of Java (e.g., Java 21 or later) unless project constraints dictate otherwise.
- **Spring Boot:** Always use the latest stable release of Spring Boot 3.x (or the latest major stable version available) for new features or projects.
- **Build Tool:** Use Gradle as the build tool. Ensure the `build.gradle` uses the latest stable Spring Boot parent POM and compatible plugin versions.

## Project Structure

- **Packaging:** Strongly prefer a **package-by-feature** structure over package-by-layer. This means grouping all code related to a specific feature or domain concept (like "posts", "users", or "orders") together in the same package hierarchy. Avoid structuring packages based solely on technical layers (like "controllers", "services", "repositories").

  - **Why Package-by-Feature?** It improves modularity, makes navigating code related to a single feature easier, reduces coupling between features, and simplifies refactoring or potentially extracting the feature into a microservice later.

  - **Example:**

    **PREFER THIS (Package-by-Feature):**

    ```
    com.example.application
    ├── posts                     # Feature: Posts
    │   ├── PostController.java   # Controller for Posts
    │   ├── PostService.java      # Service logic for Posts
    │   ├── PostRepository.java   # Data access for Posts
    │   ├── Post.java             # Domain/Entity for Posts
    │   └── dto                   # Data Transfer Objects specific to Posts
    │       ├── PostCreateRequest.java
    │       └── PostSummaryResponse.java
    │
    ├── users                     # Feature: Users
    │   ├── UserController.java
    │   ├── UserService.java
    │   ├── UserRepository.java
    │   └── User.java
    │
    └── common                    # Optional: Truly shared utilities/config
        └── exception
            └── ResourceNotFoundException.java
    ```

    **AVOID THIS (Package-by-Layer):**

    ```
    com.example.application
    ├── controller
    │   ├── PostController.java
    │   └── UserController.java
    │
    ├── service
    │   ├── PostService.java
    │   └── UserService.java
    │
    ├── repository
    │   ├── PostRepository.java
    │   └── UserRepository.java
    │
    └── model  (or domain/entity)
        ├── Post.java
        └── User.java
    ```

## Data Access

- If you are not asked to create a database, please don't.

## HTTP Clients

- **Outgoing HTTP Requests:** Use the Spring Framework 6+ **`RestClient`** for making synchronous or asynchronous HTTP calls. Avoid using the legacy `RestTemplate` in new code.

## Java Language Features

- **Data Carriers:** Use Java **Records** (`record`) for immutable data transfer objects (DTOs), value objects, or simple data aggregates whenever possible. Prefer records over traditional classes with getters, setters, `equals()`, `hashCode()`, and `toString()` for these use cases.
- **Immutability:** Favor immutability for objects where appropriate, especially for DTOs and configuration properties.

## Spring Framework Best Practices

- **Dependency Injection:** Use **constructor injection** for mandatory dependencies. Avoid field injection.
- **Configuration:** Use `application.properties` or `application.yml` for application configuration. Leverage Spring Boot's externalized configuration mechanisms (profiles, environment variables, etc.). Use `@ConfigurationProperties` for type-safe configuration binding.
- **Error Handling:** Implement consistent exception handling, potentially using `@ControllerAdvice` and custom exception classes. Provide meaningful error responses.
- **Logging:** Use SLF4j with a suitable backend (like Logback, included by default in Spring Boot starters) for logging. Write clear and informative log messages.

## Testing

- **Unit Tests:** Write unit tests for services and components using JUnit 5 and Mockito.
- **Integration Tests:** Write integration tests using `@SpringBootTest`. For database interactions, consider using Testcontainers or an in-memory database (like H2) configured only for the test profile. Ensure integration tests cover the controller layer and key application flows.
- **Test Location:** Place tests in the standard `src/test/java` directory, mirroring the source package structure.

## General Code Quality

- **Readability:** Write clean, readable, and maintainable code.
- **Comments:** Add comments only where necessary to explain complex logic or non-obvious decisions. Code should be self-documenting where possible.
- **API Design:** Design RESTful APIs with clear resource naming, proper HTTP methods, and consistent request/response formats.
