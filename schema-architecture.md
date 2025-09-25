# Smart Clinic Management System – Architecture Design

## 1. Architecture Summary

The Smart Clinic Management System is built using a three-tier architecture comprising the Presentation, Application, and Data layers. The frontend uses HTML and Thymeleaf to render dynamic content, while the backend is powered by Spring Boot. It supports both MVC-style controller endpoints and RESTful APIs. The application integrates two types of databases: a relational database (MySQL) accessed via Spring Data JPA, and a NoSQL database (MongoDB) accessed using Spring Data MongoDB. This hybrid design enables structured data storage and flexible document-based data handling for different modules.

## 2. Numbered Flow – Request/Response Cycle

1. **User Request (Frontend):**
   - The user accesses the application through a web browser.
   - The request is sent to the server via either a form submission (HTML/Thymeleaf) or a REST client (API call).

2. **Routing to Controller:**
   - Spring Boot routes the incoming request to the appropriate MVC Controller (for web pages) or REST Controller (for API endpoints).

3. **Business Logic Execution (Application Layer):**
   - Controllers delegate processing to services in the Application layer.
   - Services contain the business logic and coordinate interactions between controllers and repositories.

4. **Database Access – MySQL (Structured Data):**
   - For structured data (e.g., patient records, appointments), the service accesses the MySQL database using Spring Data JPA repositories.

5. **Database Access – MongoDB (Unstructured or Flexible Data):**
   - For flexible or document-based data (e.g., logs, feedback), the service interacts with MongoDB using Spring Data MongoDB repositories.

6. **Data Retrieval and Processing:**
   - Retrieved data is processed or transformed as needed by the service layer.

7. **Response Generation:**
   - For MVC requests, the controller returns a model and view rendered by Thymeleaf templates.
   - For API requests, the controller returns JSON data as a REST response.

8. **User Receives Response:**
   - The frontend displays the HTML page or REST response is consumed by the client application (e.g., frontend JavaScript or mobile app).

     # Smart Clinic Management System – Architecture Design

## 1. Architecture Summary

The Smart Clinic Management System is a Spring Boot-based web application that uses both Spring MVC and RESTful APIs to serve different parts of the system. Admin and Doctor dashboards are rendered using Thymeleaf (MVC), while other modules such as Appointments and Patient Records interact with the backend through REST APIs.

The architecture follows a **three-tier design**:

- **Presentation Tier:** Responsible for user interaction. It includes Thymeleaf templates for web dashboards and external clients (like mobile apps) that consume REST APIs.
- **Application Tier:** The Spring Boot backend contains controllers, services, and the core business logic.
- **Data Tier:** Integrates two databases:
  - **MySQL** for structured, relational data (e.g., Patient, Doctor, Appointment, Admin)
  - **MongoDB** for flexible, document-oriented data (e.g., Prescriptions)

The application ensures a clean separation of concerns by routing all requests (whether MVC or REST) through the **Service Layer**, which then delegates to either **JPA repositories (MySQL)** or **MongoDB repositories**. This dual-database setup allows for both robust data integrity and flexible data modeling.

---

## 2. Numbered Flow – Request/Response Cycle

1. **User Interaction**  
   Users access the system either via:
   - Web dashboards (AdminDashboard, DoctorDashboard) rendered with Thymeleaf, or  
   - External API clients (like PatientDashboard or mobile apps) that call REST endpoints.

2. **Routing to Controller Layer**  
   Spring Boot handles routing:
   - Requests for server-rendered views go to MVC Controllers.
   - Requests from REST clients go to REST Controllers.
   Each controller is mapped to specific URL patterns and HTTP methods.

3. **Controller Delegates to Service Layer**  
   Controllers do not contain business logic. Instead, they forward incoming requests to appropriate service classes that handle the processing.

4. **Business Logic Execution in Service Layer**  
   Services apply business rules, validations, and coordinate workflows. For example, checking doctor availability before booking an appointment.

5. **Repository Layer Access**  
   Services interact with:
   - **Spring Data JPA Repositories** for relational data (MySQL)
   - **Spring Data MongoDB Repositories** for document data (MongoDB)
   This layer abstracts direct database operations.

6. **Database Communication**  
   - **MySQL** handles core tables like Patient, Doctor, Appointment, and Admin.
   - **MongoDB** stores dynamic and nested data like Prescriptions, allowing for flexible schema evolution.

7. **Response Returned to Client**  
   - For MVC: Data is passed to Thymeleaf templates, rendered as HTML, and returned to the browser.  
   - For REST: Data is serialized to JSON and returned in the HTTP response.



