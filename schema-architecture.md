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

