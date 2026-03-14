# What I Learned

Building this E-Commerce REST API was a comprehensive journey into enterprise-grade backend development. It served as a practical application of theoretical concepts, transitioning from basic API construction to building a secure, scalable, and production-ready system. Below is a breakdown of the key takeaways from this project.

## 1. System Design Concepts Learned

- **Layered Architecture**: I learned how to separate concerns strictly by dividing the application into Presentation (Controllers), Business (Services), and Data Access (Repositories) layers. This ensures that changes in one layer (like swapping the database) don't bleed into others.
- **Statelessness**: Understanding that REST APIs should be stateless. Instead of using server-side sessions, I implemented JSON Web Tokens (JWT) so the server doesn't need to remember who is logged in between requests.
- **Transaction Management**: Learning where to place atomic boundaries (using `@Transactional` on service methods) to ensure that if a complex operation (like checking out a cart and creating an order) fails halfway, the database safely rolls back to its original state.
- **Database Migrations**: Using Flyway taught me that database schemas should be treated as code. Instead of manually altering tables in an SQL client, having versioned SQL scripts guarantees that the database structure evolves predictably across all environments.
- **Containerization**: Wrapping the application and its database in Docker containers with `docker-compose`. This taught me how to abstract away the host environment, making the application run consistently anywhere without `"it works on my machine"` problems.

## 2. Concepts Implemented

- **Authentication & Authorization flow**: Handling user registration, encrypting passwords, issuing short-lived access tokens and long-lived refresh tokens.
- **Object-Relational Mapping (ORM)**: Translating Java Objects directly into MySQL tables using Hibernate, managing complex relationships (One-to-Many, Many-to-One), and understanding the implications of lazy vs. eager fetching.
- **Payment Processing**: Integrating a third-party gateway (Stripe) to securely handle financial transactions without touching sensitive credit card data on our servers.
- **Global Error Handling**: Using `@ControllerAdvice` to intercept exceptions across all controllers and map them to standardized, user-friendly HTTP JSON responses.
- **Data Validation**: Utilizing the Bean Validation API to sanitize and verify incoming DTOs before they ever reach the business logic.

## 3. Technologies Explored

- **Spring Ecosystem** (`Spring Boot`, `Spring Web`, `Spring Data JPA`, `Spring Security`): The core framework that drastically reduces boilerplate and auto-configures robust defaults.
- **Java 21**: Leveraging the latest LTS features of the language.
- **MySQL**: The relational database management system used for persistent data storage.
- **MapStruct**: A code generator that drastically simplified the mapping between Database Entities and REST DTOs at compile time.
- **Lombok**: A library used to eliminate the visual clutter of getters, setters, and constructors in Java classes.
- **Stripe SDK**: Used to build a robust and secure checkout pipeline.
- **Swagger / OpenAPI 3**: Automatically generating API documentation to make testing and frontend integration effortless.
- **Docker & Docker Compose**: Used to orchestrate the backend services and the database environment.

## 4. Design Patterns Used

- **Data Transfer Object (DTO) Pattern**: Decoupling the internal database structure (Entities) from the external API contract. This prevents infinite recursion in JSON serialization and hides sensitive data (like password hashes).
- **Dependency Injection (DI) / Inversion of Control (IoC)**: Letting the Spring framework manage object creation and lifecycle. Classes declare their dependencies via constructors, and Spring wires them together.
- **Builder Pattern**: Utilized heavily via Lombok's `@Builder` annotation to construct complex objects (like `User` or `Order`) in a readable, fluent manner.
- **Repository Pattern**: Provided by Spring Data JPA, abstracting away the low-level JDBC and SQL code behind clean, intuitive Java interfaces (`save()`, `findById()`).
- **Singleton Pattern**: Understand that Spring Beans (like Controllers and Services) are singletons by default, meaning they must be stateless and thread-safe.
