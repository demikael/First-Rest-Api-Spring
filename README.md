![Postman 1](https://github.com/user-attachments/assets/67e5a69a-8845-4053-86cf-436672cb9c96)# Task 2 - First REST API Application

## Project Overview

This project involves building a fully functional REST API using the Spring Framework. The application manages a product catalog, supporting complete CRUD (Create, Read, Update, Delete) operations and persisting data in an H2 in-memory database.

## Technologies Used

* **Java** (Latest compatible version) 
* **Spring Boot** (Spring Web, Spring Data JPA, DevTools) 
* **H2 Database** (In-memory) 
* **Lombok** (To reduce boilerplate code) 
* **Swagger UI / OpenAPI** (API Documentation) 
* **Postman** (API Testing) 



---

## Step-by-Step Implementation

### 2.A: Project Initialization & Structure

![Postman 1](https://github.com/user-attachments/assets/b4ca2b44-35fb-443c-94ad-1952dc6439fc)

The project was initialized using **Spring Initializr** within IntelliJ IDEA. We included dependencies for Spring Web, H2 Database, Spring Data JPA, and DevTools.

The project follows a modular package structure:

* `api`: Contains `ProductController` and request/response DTOs.

* `domain`: Contains the `Product` entity.

* `repository`: Manages data persistence.

* `service`: Handles business logic.

* `support`: Includes utility classes like `ProductMapper` and exception handlers.



### 2.B: Adding Swagger UI

![Swagger UI](https://github.com/user-attachments/assets/6c5ba761-54b2-434f-be7c-9dc1dd8ed8a6)

![Swagger without UI (JSON)](https://github.com/user-attachments/assets/9359f430-5072-43ac-987a-147bab127542)

To document and test the API easily, we added **Swagger UI (OpenAPI)** by adding the required dependency to `pom.xml`. We also used the `@OpenAPIDefinition` annotation in the main application class to provide metadata for the documentation.

### 2.C: Implementing the GET Endpoint

![Postman 2](https://github.com/user-attachments/assets/8cafdd65-548c-4f72-a509-c59eb65d5ed5)

We added an endpoint to retrieve a product by its unique ID (`/api/v1/products/{id}`). This involves using `@GetMapping` and `@PathVariable` to capture the ID from the URL and pass it to the service and repository layers.

### 2.D: Exception Handling

To avoid returning generic "500 Internal Server Error" messages, we implemented custom exception handling. We created a `ProductNotFoundException` and used `@ControllerAdvice` to catch this exception and return a clear `404 Not Found` status with a descriptive JSON message.

### 2.E: Implementing the PUT Method

![Swagger](https://github.com/user-attachments/assets/f6d675f8-e723-401e-97b1-dcdd2d6a8c82)

The `PUT` method was added to allow updating existing product records. This required creating an `UpdateProductRequest` DTO and updating the service logic to map new data onto existing entities.

### 2.F: GET ALL and DELETE Functionality

We expanded the API to support:

* **GET ALL**: Returns a list of all products in the database.

* **DELETE**: Removes a product by ID, returning a `204 No Content` status upon success.



### 2.G: Database Integration (H2 & JPA)

![H2](https://github.com/user-attachments/assets/8346bcd4-5ddc-4b98-b54d-2a4f7d7c4999)

![H2 Console](https://github.com/user-attachments/assets/d32c3ef3-32dc-4a2d-8652-ce344364b69f)

![H2 Console 2](https://github.com/user-attachments/assets/1a909dd5-bb4c-494b-816e-6a54cc787fbd)

We transitioned from a temporary HashMap to a real (in-memory) **H2 Database**.

1. **Configuration**: Updated `application.properties` to enable the H2 console and set the JDBC URL (`jdbc:h2:mem:testdb`).

2. **Entity Mapping**: The `Product` class was annotated with `@Entity`, `@Id`, and `@GeneratedValue` to map it to a database table.

3. **JPA Repository**: The `ProductRepository` was converted to an interface extending `JpaRepository`, granting us access to automatic CRUD implementations.



### 2.H: Final Test

![2H](https://github.com/user-attachments/assets/d380a242-63af-4504-b77d-db511454a4e5)
