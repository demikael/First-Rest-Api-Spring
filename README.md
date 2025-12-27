# Task 2 - First REST API Application

## Project Overview

This project is a fully functional REST API built using the Spring Framework. It manages a product catalog, allowing for Create, Read, Update, and Delete (CRUD) operations. The application uses an H2 in-memory database for data persistence during runtime.

## Technologies Used

* **Java** (Latest compatible version) 
* **Spring Boot** (Spring Web, Spring Data JPA, DevTools) 
* **H2 Database** (In-memory) 
* **Lombok** (To reduce boilerplate code) 
* **Swagger UI / OpenAPI** (API Documentation) 
* **Postman** (API Testing) 



---

## Step-by-Step Implementation

### 1. Project Initialization

The project was created using **Spring Initializr** directly in the IDE.

* **Dependencies:** Spring Web, H2 Database, Spring Data JPA, Lombok, Spring Boot DevTools.



### 2. Project Structure

The application follows a standard package-based division for better organization:

* `api`: Contains the `ProductController`.
* `domain`: Contains the `Product` entity.
* `repository`: Contains the `ProductRepository` interface.
* `service`: Contains the `ProductService` for business logic.
* `support`: Contains mappers and exception handlers.



### 3. Domain Model (`Product`)

The `Product` class is marked as a JPA `@Entity` to map it to the database.

```java
@Entity
@Table(name = "PRODUCTS")
@Getter @Setter @NoArgsConstructor
public class Product {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String name;
}

```

### 4. Database Configuration

Configured `application.properties` to enable the H2 Console and define the data source.

```properties
spring.h2.console.enabled=true
spring.h2.console.path=/console
spring.datasource.url=jdbc:h2:mem:testdb
spring.jpa.show-sql=true

```

### 5. API Endpoints (Controller)

The `ProductController` handles incoming HTTP requests.

| Method | Endpoint | Description |
| :--- | :--- | :--- |
| **POST** | `/api/v1/products` | Create a new product |
| **GET** | `/api/v1/products/{id}` | Retrieve a product by ID |
| **GET** | `/api/v1/products` | List all products |
| **PUT** | `/api/v1/products/{id}` | Update an existing product |
| **DELETE** | `/api/v1/products/{id}` | Remove a product |

### 6. Exception Handling

Custom exception handling ensures clear error messages and correct HTTP status codes (e.g., 404 Not Found instead of 500 Error).

```java
@ControllerAdvice
public class ProductExceptionHandler {
    @ExceptionHandler(ProductNotFoundException.class)
    public ResponseEntity<ErrorMessageResponse> handleNotFound(ProductNotFoundException ex) {
        return new ResponseEntity<>(new ErrorMessageResponse(ex.getMessage()), HttpStatus.NOT_FOUND);
    }
}

```

---

## Testing & Web View

### Swagger UI Documentation

Once the application is running, the API documentation is accessible at:

* `http://localhost:8080/swagger-ui/index.html` 



### H2 Database Console

View and execute SQL queries directly in the browser:

* `http://localhost:8080/console`
* **JDBC URL:** `jdbc:h2:mem:testdb` 



### Testing with Postman

Example of a `POST` request to create a product:

* **Body (JSON):** `{"name": "New Product"}`
* **Expected Response:** `201 Created`



---

## Step-by-Step Implementation

### 2.A: Project Initialization & Structure

The project was initialized using **Spring Initializr** within IntelliJ IDEA. We included dependencies for Spring Web, H2 Database, Spring Data JPA, and DevTools.
![ConsoleOutput](https://github.com/user-attachments/assets/e43dc443-9d15-4043-92f2-87cb9d3ad342)

The project follows a modular package structure:

* `api`: Contains `ProductController` and request/response DTOs.
  ![ProductController](https://github.com/user-attachments/assets/3610aa29-56ce-4574-88eb-9ab3549a7a67)
  ![ProductRequest](https://github.com/user-attachments/assets/393b0a76-ab45-449d-8740-5df8bd5c6929)
  ![ProductRequest](https://github.com/user-attachments/assets/e6e4bc65-10df-41b9-88ed-bf9b187331c0)

* `domain`: Contains the `Product` entity.
  ![Product](https://github.com/user-attachments/assets/46984a39-07c2-4933-bd4d-4ae3e15f2ac1)

* `repository`: Manages data persistence.
  ![ProductRepository](https://github.com/user-attachments/assets/edeaeecc-fd45-4e97-830c-36e98aec8d34)

* `service`: Handles business logic.
  ![ProductService](https://github.com/user-attachments/assets/9a0e39d1-fdeb-4036-b20e-e1a8eb3748f7)

* `support`: Includes utility classes like `ProductMapper` and exception handlers.



### 2.B: Adding Swagger UI

![Swagger UI dependency](https://github.com/user-attachments/assets/00150be5-50ee-428e-a218-5c5a152fd198)

To document and test the API easily, we added **Swagger UI (OpenAPI)** by adding the required dependency to `pom.xml`. We also used the `@OpenAPIDefinition` annotation in the main application class to provide metadata for the documentation.
![Swagger UI](https://github.com/user-attachments/assets/d4e68404-a9dc-446f-b7ba-bd2663011054)



### 2.C: Implementing the GET Endpoint

![Endpoint (ProductController)](https://github.com/user-attachments/assets/259c7fb9-ea02-4967-8d76-187f32252a05)
![Endpoint (ProductService)](https://github.com/user-attachments/assets/3ec2bb85-5cc0-45c0-a6dd-90d53297ee67)
![Endpoint (ProductRepository)](https://github.com/user-attachments/assets/2bd61b1d-795e-4f5e-b8d9-3c25498b6d9d)

We added an endpoint to retrieve a product by its unique ID (`/api/v1/products/{id}`). This involves using `@GetMapping` and `@PathVariable` to capture the ID from the URL and pass it to the service and repository layers.
![Postman 2](https://github.com/user-attachments/assets/fbb72710-f71e-44b0-8c93-84b26faa6111)



### 2.D: Exception Handling

![ProductNotFoundException](https://github.com/user-attachments/assets/22f55596-c52d-4288-a6c0-1d17d160cc7f)
![ProductExceptionSupplier](https://github.com/user-attachments/assets/1bd8bfdf-b0e6-46e7-a9ac-260df166de45)
![ProductExceptionAdvisor](https://github.com/user-attachments/assets/ea74de30-bfb1-4fae-89f2-ad548066ae09)
![ErrorMessageResponse](https://github.com/user-attachments/assets/22789ae8-9fa1-4a90-ba35-db704f47c084)

To avoid returning generic "500 Internal Server Error" messages, we implemented custom exception handling. We created a `ProductNotFoundException` and used `@ControllerAdvice` to catch this exception and return a clear `404 Not Found` status with a descriptive JSON message.

### 2.E: Implementing the PUT Method

![Put Method](https://github.com/user-attachments/assets/2220b4e0-8852-4b9a-abd3-536d7a381bc0)
![UpdateProductRequest](https://github.com/user-attachments/assets/9d99c045-3998-4ed1-b7ca-5b0f0e185efd)

The `PUT` method was added to allow updating existing product records. This required creating an `UpdateProductRequest` DTO and updating the service logic to map new data onto existing entities.
![Swagger](https://github.com/user-attachments/assets/581172de-d3fb-4273-a86c-b842a31a2ee6)



### 2.F: GET ALL and DELETE Functionality

We expanded the API to support:

* **GET ALL**: Returns a list of all products in the database.
  ![Get All (ProductController)](https://github.com/user-attachments/assets/6a5e261b-9007-49a5-a6a0-027474ff8f88)



* **DELETE**: Removes a product by ID, returning a `204 No Content` status upon success.
  ![Delete (ProductController)](https://github.com/user-attachments/assets/434339ac-f8cd-4389-a7d0-fee887699604)



### 2.G: Database Integration (H2 & JPA)

We transitioned from a temporary HashMap to a real (in-memory) **H2 Database**.
![H2 Console 2](https://github.com/user-attachments/assets/8179726b-2b19-4686-bfde-1033404978ac)

1. **Configuration**: Updated `application.properties` to enable the H2 console and set the JDBC URL (`jdbc:h2:mem:testdb`).
   ![application_properties](https://github.com/user-attachments/assets/a24af3e2-dbf3-428e-829c-beeeee2c5b36)

2. **Entity Mapping**: The `Product` class was annotated with `@Entity`, `@Id`, and `@GeneratedValue` to map it to a database table.
   ![Database (Product)](https://github.com/user-attachments/assets/a852543a-3447-4e9e-8774-5ccbc9622ddd)

3. **JPA Repository**: The `ProductRepository` was converted to an interface extending `JpaRepository`, granting us access to automatic CRUD implementations.
   ![Database (ProductRepository)](https://github.com/user-attachments/assets/bbbf0963-5ee8-4f5e-8630-e19a2e2adcf6)



### 2.H: Final Tests
![2H](https://github.com/user-attachments/assets/9aa710d0-d601-414a-ac7f-cef8a1933f73)
