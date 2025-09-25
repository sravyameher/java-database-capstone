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



