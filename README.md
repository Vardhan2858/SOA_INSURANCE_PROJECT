# SOA Insurance Project

A Spring Boot microservices application for managing insurance policies, claims,
and settlements. The services use Eureka for service discovery, MySQL for
persistence, and JWT for authentication in the policy and claim services.

## Services

| Service | Port | Purpose |
|---|---:|---|
| Eureka Server | 8761 | Service discovery |
| Policy Service | 8081 | Create and manage insurance policies |
| Claim Service | 8082 | Create, verify, and manage claims |
| Settlement Service | 8083 | Create and manage claim settlements |

## Technology

- Java 17
- Spring Boot 4.1.1
- Spring Cloud 2025.1.3
- Spring Data JPA
- MySQL
- Spring Security with JWT
- Netflix Eureka
- Maven Wrapper

## Prerequisites

- Java 17 or later
- MySQL running locally
- A database named `insurance_db`

Create the database before starting the services:

```sql
CREATE DATABASE insurance_db;
```

## Configuration

Database connection settings are stored in each service's
`src/main/resources/application.properties` file. Set the database password
using the `DB_PASSWORD` environment variable. The policy and claim services
also require a JWT signing key in the `JWT_SECRET` environment variable.

PowerShell example:

```powershell
$env:DB_PASSWORD = "your-database-password"
$env:JWT_SECRET = "your-long-random-jwt-secret"
```

Do not commit real passwords, signing keys, or other credentials to the
repository.

## Running the services

Open a separate terminal for each service. Start Eureka first, followed by
the application services.

```powershell
cd eureka-server
.\mvnw.cmd spring-boot:run
```

```powershell
cd policy-service
.\mvnw.cmd spring-boot:run
```

```powershell
cd claim-service
.\mvnw.cmd spring-boot:run
```

```powershell
cd settlement-service
.\mvnw.cmd spring-boot:run
```

The Eureka dashboard is available at
<http://localhost:8761>.

## API areas

- Authentication: `POST /auth/login`
- Policies: `/policies`
- Claims: `/claims`
- Settlements: `/settlements`

The exact request and response models are defined in the corresponding
service source code.

## Building and testing

Run the following command from each service directory:

```powershell
.\mvnw.cmd clean test
```

Build an executable JAR with:

```powershell
.\mvnw.cmd clean package
```

Build output is written to the service's `target` directory, which is ignored
by Git.
