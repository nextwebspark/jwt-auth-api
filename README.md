# JWT Authentication API

## Overview

This is a Spring Boot application that provides authentication functionality using JWT (JSON Web Tokens). It allows users to register, log in, and obtain JWT tokens for authentication. This API consists of two main endpoints:

- **POST /auth/signup**: Registers a new user.
- **POST /auth/login**: Authenticates a user and generates a JWT token.

## Features

- User Registration
- User Login and JWT Token Generation
- Spring Security for Authentication

## Technologies Used

- Spring Boot 3.x
- Spring Security
- JWT (JSON Web Tokens)
- MySQL / H2 (for database)
- Maven for Dependency Management

## Prerequisites

Before running this project, ensure that you have the following installed:

- Java 17 or later
- Maven
- MySQL (or H2 for embedded DB)
- Postman or any API testing tool (for making requests)

## Getting Started

### Clone the repository

Clone this repository to your local machine:

```bash
git clone https://github.com/yourusername/jwt-auth-api.git
cd jwt-auth-api
```
### Setup Database
H2 Database: If you're using the H2 embedded database, no additional setup is required. It will be used automatically in the development environment.

### Build the Application
Use Maven to build the project:

```bash
mvn clean install
```

### Run the Application
You can run the application with the following command:

```bash
mvn spring-boot:run
```








