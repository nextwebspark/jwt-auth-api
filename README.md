JWT Authentication API
Overview
This is a Spring Boot application that provides authentication functionality using JWT (JSON Web Tokens). It allows users to register, log in, and obtain JWT tokens for authentication. This API consists of two main endpoints:

POST /auth/signup: Registers a new user.
POST /auth/login: Authenticates a user and generates a JWT token.
Features
User Registration
User Login and JWT Token Generation
Spring Security for Authentication
Technologies Used
Spring Boot 3.x
Spring Security
JWT (JSON Web Tokens)
MySQL / H2 (for database)
Maven for Dependency Management
Prerequisites
Before running this project, ensure that you have the following installed:

Java 17 or later
Maven
MySQL (or H2 for embedded DB)
Postman or any API testing tool (for making requests)
Getting Started
Clone the repository
Clone this repository to your local machine:

bash
Copy code
git clone https://github.com/yourusername/jwt-auth-api.git
cd jwt-auth-api
Setup Database
H2 Database: If you're using the H2 embedded database, no additional setup is required. It will be used automatically in the development environment.

MySQL Database: If you prefer MySQL, ensure that you have MySQL running and configure the database connection in application.properties:

properties
Copy code
spring.datasource.url=jdbc:mysql://localhost:3306/your_database_name
spring.datasource.username=your_username
spring.datasource.password=your_password
Build the Application
Use Maven to build the project:

bash
Copy code
mvn clean install
Run the Application
You can run the application with the following command:

bash
Copy code
mvn spring-boot:run
Alternatively, you can run it directly from your IDE.

Once the application starts, it will be available at:

arduino
Copy code
http://localhost:8080
API Endpoints
1. User Registration (POST /auth/signup)
Request:

json
Copy code
POST /auth/signup
Request body:

json
Copy code
{
  "email": "user@example.com",
  "password": "securepassword",
  "fullName": "John Doe"
}
Response:

json
Copy code
{
  "id": 1,
  "email": "user@example.com",
  "fullName": "John Doe"
}
2. User Login (POST /auth/login)
Request:

json
Copy code
POST /auth/login
Request body:

json
Copy code
{
  "email": "user@example.com",
  "password": "securepassword"
}
Response:

json
Copy code
{
  "token": "jwt_token_here",
  "expiresIn": 3600
}
token: The generated JWT token.
expiresIn: The expiration time of the token in seconds (typically 1 hour or more).
Dependencies
The following dependencies are included in the project:

spring-boot-starter-web: Provides basic Spring MVC functionality.
spring-boot-starter-security: Provides Spring Security for authentication.
spring-boot-starter-data-jpa: To interact with databases using JPA (Java Persistence API).
mysql-connector-j: MySQL JDBC driver.
h2: In-memory database (optional, if using H2).
jjwt-api, jjwt-impl, jjwt-jackson: Libraries for generating and parsing JWT tokens.
spring-boot-starter-test: For testing purposes.
Controller Implementation
The main authentication logic is handled in the AuthenticationController class:

java
Copy code
@RequestMapping("/auth")
@RestController
public class AuthenticationController {
    private final JwtService jwtService;
    private final AuthenticationService authenticationService;

    public AuthenticationController(JwtService jwtService, AuthenticationService authenticationService) {
        this.jwtService = jwtService;
        this.authenticationService = authenticationService;
    }

    // User Registration
    @PostMapping("/signup")
    public ResponseEntity<User> register(@RequestBody RegisterUserModel registerUser) {
        User registeredUser = authenticationService.signup(registerUser);
        return ResponseEntity.ok(registeredUser);
    }

    // User Login and JWT Generation
    @PostMapping("/login")
    public ResponseEntity<LoginResponse> authenticate(@RequestBody LoginUserModel loginUserDto) {
        User authenticatedUser = authenticationService.authenticate(loginUserDto);
        String jwtToken = jwtService.generateToken(authenticatedUser);
        LoginResponse loginResponse = new LoginResponse()
                .setToken(jwtToken)
                .setExpiresIn(jwtService.getExpirationTime());
        return ResponseEntity.ok(loginResponse);
    }
}
Flow Explanation
User Registration (/signup): A user sends their email, password, and full name. The system registers the user and returns the user details.

User Login (/login): A user provides their email and password. If authentication is successful, a JWT token is generated and returned, which the client can use to access protected resources.

Testing the API
You can test the API using Postman or any other API testing tool:

Register a new user by sending a POST request to /auth/signup with the appropriate JSON payload.
Login by sending a POST request to /auth/login with the registered user's email and password.
The server will return a JWT token and its expiration time, which you can use for authentication in subsequent requests.
License
This project is licensed under the MIT License - see the LICENSE file for details.
