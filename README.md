# BankinApp

A full-stack banking application built with Spring Boot and React that allows users to manage their bank accounts and transactions securely.

## Table of Contents

- [Features](#features)
- [Technology Stack](#technology-stack)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Configuration](#configuration)
- [Running the Application](#running-the-application)
- [API Endpoints](#api-endpoints)
- [Project Structure](#project-structure)
- [Testing](#testing)
- [Contributing](#contributing)

## Features

- User authentication and authorization with JWT
- User registration and login
- User profile management (view and edit)
- Multiple bank account management
- Transaction tracking and management
- Transaction history and reporting
- Secure REST API
- Responsive React frontend
- PostgreSQL database integration

## Technology Stack

### Backend
- **Java 21**
- **Spring Boot 3.5.5**
- **Spring Security** - Authentication and authorization
- **Spring Data JPA** - Database operations
- **PostgreSQL** - Database
- **JWT (JSON Web Tokens)** - Token-based authentication
- **Lombok** - Reduces boilerplate code
- **Maven** - Build and dependency management

### Frontend
- **React 19.1.1**
- **TypeScript 4.9.5**
- **React Router DOM 7.9.1** - Navigation
- **Axios 1.12.2** - HTTP requests
- **React Scripts 5.0.1** - Build tooling

### Testing
- **JUnit 5** - Unit testing
- **Spring Security Test** - Security testing
- **Selenium WebDriver** - End-to-end testing
- **React Testing Library** - Frontend testing

## Prerequisites

Before you begin, ensure you have the following installed:

- **Java Development Kit (JDK) 21** or higher
- **Node.js** (v16 or higher) and **npm**
- **PostgreSQL** (v12 or higher)
- **Maven** (v3.6 or higher)
- **Git**

## Installation

### 1. Clone the Repository

```bash
git clone <repository-url>
cd BankinApp
```

### 2. Database Setup

Create a PostgreSQL database for the application:

```sql
CREATE DATABASE bankinapp;
CREATE USER bankinapp_user WITH PASSWORD 'your_password';
GRANT ALL PRIVILEGES ON DATABASE bankinapp TO bankinapp_user;
```

### 3. Backend Configuration

Create or update `src/main/resources/application.properties`:

```properties
# Database Configuration
spring.datasource.url=jdbc:postgresql://localhost:5432/bankinapp
spring.datasource.username=bankinapp_user
spring.datasource.password=your_password
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.PostgreSQLDialect

# JWT Configuration
jwt.secret=your-secret-key-here-make-it-long-and-secure
jwt.expiration=86400000

# Server Configuration
server.port=8080
```

### 4. Install Frontend Dependencies

```bash
cd frontend
npm install
```

## Configuration

### JWT Secret Key

Generate a secure JWT secret key and update it in `application.properties`:

```bash
# Generate a secure random key
openssl rand -base64 64
```

### CORS Configuration

The backend is configured to accept requests from `http://localhost:3000` during development. Update `SecurityConfig.java` if you need to modify CORS settings.

## Running the Application

### Development Mode

#### Start Backend (Spring Boot)

```bash
# From the project root directory
mvn spring-boot:run
```

The backend will start on `http://localhost:8080`

#### Start Frontend (React)

```bash
# From the frontend directory
cd frontend
npm start
```

The frontend will start on `http://localhost:3000`

### Production Build

#### Build Frontend

```bash
cd frontend
npm run build
```

#### Build and Run Complete Application

```bash
# From the project root directory
mvn clean package
java -jar target/BankingApp-0.0.1-SNAPSHOT.jar
```

The application will be available at `http://localhost:8080`

## API Endpoints

### Authentication

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/api/auth/register` | Register a new user |
| POST | `/api/auth/login` | Login and receive JWT token |

### User Management

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/users/profile` | Get current user profile |
| PUT | `/api/users/profile` | Update user profile |
| GET | `/api/users/usernames` | Get all usernames (for validation) |

### Account Management

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/accounts` | Get all accounts for current user |
| POST | `/api/accounts` | Create a new account |
| GET | `/api/accounts/{id}` | Get account by ID |
| DELETE | `/api/accounts/{id}` | Delete an account |

### Transaction Management

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/accounts/{accountId}/transactions` | Get all transactions for an account |
| POST | `/api/accounts/{accountId}/transactions` | Create a new transaction |
| PUT | `/api/transactions/{id}` | Update a transaction |
| DELETE | `/api/transactions/{id}` | Delete a transaction |

### Reports

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/api/reports/generate` | Generate transaction report |

## Project Structure

```
BankinApp/
├── src/
│   ├── main/
│   │   ├── java/org/example/bankinapp/
│   │   │   ├── config/              # Security & JWT configuration
│   │   │   ├── controller/          # REST controllers
│   │   │   ├── dto/                 # Data Transfer Objects
│   │   │   ├── exception/           # Exception handling
│   │   │   ├── model/               # Entity classes
│   │   │   ├── repository/          # JPA repositories
│   │   │   └── service/             # Business logic
│   │   └── resources/
│   │       └── application.properties
│   └── test/                        # Unit and integration tests
├── frontend/
│   ├── public/                      # Static files
│   ├── src/
│   │   ├── components/              # React components
│   │   ├── pages/                   # Page components
│   │   ├── App.tsx                  # Main App component
│   │   └── index.tsx                # Entry point
│   └── package.json
├── pom.xml                          # Maven configuration
└── README.md
```

## Testing

### Backend Tests

Run all backend tests:

```bash
mvn test
```

Run specific test class:

```bash
mvn test -Dtest=UserServiceTest
```

### Frontend Tests

Run frontend tests:

```bash
cd frontend
npm test
```

### End-to-End Tests

The application includes Selenium tests for end-to-end testing:

```bash
mvn test -Dtest=RegisterTest,LoginTest
```

## Key Features Explained

### Authentication Flow

1. User registers with username, email, password, name, and phone number
2. Passwords are encrypted using BCrypt
3. User logs in with username and password
4. Server generates JWT token valid for 24 hours
5. Client includes JWT token in Authorization header for subsequent requests

### Security

- JWT-based stateless authentication
- Password encryption with BCrypt
- Role-based access control
- CSRF protection
- Secure HTTP headers

### Account Types

Users can create multiple accounts with different types:
- Savings
- Checking
- Credit

### Transaction Management

- Record deposits, withdrawals, and transfers
- Track transaction dates and descriptions
- View transaction history by account
- Generate reports for specific date ranges

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Contact

For questions or support, please open an issue in the repository.

---

Built with Spring Boot and React
