# JWT Security with Spring Boot

A secure RESTful API implementation using Spring Boot 4.0.0 and JSON Web Tokens (JWT) for authentication and authorization.

## Features

- User registration and authentication
- JWT-based stateless authentication
- Role-based access control
- Secure password storage with BCrypt
- CSRF protection
- Session management with stateless policy

## Prerequisites

- Java 21
- Maven 3.6.3 or later
- PostgreSQL or MySQL database
- (Optional) Postman or any API testing tool

## Tech Stack

- **Framework**: Spring Boot 4.0.0
- **Security**: Spring Security, JWT
- **Database**: PostgreSQL/MySQL
- **Build Tool**: Maven
- **Lombok**: For reducing boilerplate code
- **JSON Web Token**: For authentication

## API Endpoints

### Authentication

- `POST /api/v1/auth/register` - Register a new user
  - Request body: `{ "firstname": "string", "lastname": "string", "email": "string", "password": "string" }`
  - Response: JWT token

- `POST /api/v1/auth/authenticate` - Authenticate user and get JWT token
  - Request body: `{ "email": "string", "password": "string" }`
  - Response: JWT token

### Protected Endpoints

- `GET /api/v1/demo` - Example protected endpoint
  - Requires valid JWT token in Authorization header

## Setup Instructions

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd jwt-sec
   ```

2. **Configure Database**
   - Update `application.properties` with your database credentials
   - Ensure the database server is running

3. **Build the application**
   ```bash
   mvn clean install
   ```

4. **Run the application**
   ```bash
   mvn spring-boot:run
   ```

5. **Access the application**
   - The application will start on `http://localhost:8080`

## Usage

1. **Register a new user**
   ```bash
   curl -X POST http://localhost:8080/api/v1/auth/register \
   -H "Content-Type: application/json" \
   -d '{"firstname":"John", "lastname":"Doe", "email":"john@example.com", "password":"password123"}'
   ```

2. **Authenticate**
   ```bash
   curl -X POST http://localhost:8080/api/v1/auth/authenticate \
   -H "Content-Type: application/json" \
   -d '{"email":"john@example.com", "password":"password123"}'
   ```
   Copy the JWT token from the response.

3. **Access protected endpoint**
   ```bash
   curl -X GET http://localhost:8080/api/v1/demo \
   -H "Authorization: Bearer YOUR_JWT_TOKEN"
   ```

## Security

- JWT tokens are used for stateless authentication
- Passwords are hashed using BCrypt
- CSRF protection is enabled
- Session management is stateless
- All endpoints except `/api/v1/auth/**` are secured

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
