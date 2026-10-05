# Booking Microservices — Java & Spring Boot

> A distributed booking platform built to explore **microservices architecture, Domain-Driven Design, CQRS, event-driven communication, and observability** with Java and Spring Boot.

[![Java](https://img.shields.io/badge/Java-11%2B-orange?style=flat-square&logo=openjdk)](https://www.oracle.com/java/)
[![Spring Boot](https://img.shields.io/badge/Spring%20Boot-brightgreen?style=flat-square&logo=springboot)](https://spring.io/projects/spring-boot)
[![Docker](https://img.shields.io/badge/Docker-Compose-2496ED?style=flat-square&logo=docker&logoColor=white)](https://www.docker.com/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white)](https://www.postgresql.org/)
[![MongoDB](https://img.shields.io/badge/MongoDB-47A248?style=flat-square&logo=mongodb&logoColor=white)](https://www.mongodb.com/)
[![RabbitMQ](https://img.shields.io/badge/RabbitMQ-FF6600?style=flat-square&logo=rabbitmq&logoColor=white)](https://www.rabbitmq.com/)

## 🎯 Why this project?

This is a hands-on exploration of how to design a distributed backend rather than a simple CRUD application.

The project focuses on:

- **Domain-Driven Design (DDD)** and bounded contexts
- **Vertical Slice Architecture** for feature-oriented organization
- **CQRS** for separating command and query responsibilities
- **Event-driven architecture** with asynchronous messaging
- **gRPC** for internal synchronous communication
- **Outbox / Inbox patterns** for reliable messaging and idempotency
- **Keycloak + OAuth2/OIDC** for authentication and authorization
- **OpenTelemetry + Prometheus + Grafana + Jaeger** for observability
- **JUnit + Mockito + Testcontainers** for automated testing

---

## 🏗️ Architecture

```text
                         ┌─────────────────────┐
                         │       Clients       │
                         └──────────┬──────────┘
                                    │
                                    ▼
                         ┌─────────────────────┐
                         │    API Gateway      │
                         └──────────┬──────────┘
                                    │
              ┌─────────────────────┼─────────────────────┐
              │                     │                     │
              ▼                     ▼                     ▼
      ┌──────────────┐      ┌──────────────┐      ┌──────────────┐
      │    Flight    │      │  Passenger   │      │   Booking    │
      │   Service    │      │   Service    │      │   Service    │
      └──────┬───────┘      └──────┬───────┘      └──────┬───────┘
             │                     │                     │
             └──────────────┬──────┴─────────────────────┘
                            │
                            ▼
                    ┌───────────────┐
                    │    RabbitMQ   │
                    │   Event Bus   │
                    └───────────────┘

        PostgreSQL / MongoDB / Keycloak / Observability
```

### Core services

| Service | Responsibility |
|---|---|
| **API Gateway** | Entry point and request routing |
| **Keycloak** | Authentication and authorization |
| **Flight Service** | Flight management and availability |
| **Passenger Service** | Passenger management |
| **Booking Service** | Booking and ticket operations |
| **Building Blocks** | Shared technical infrastructure |

---

## 🧠 Architecture & Design Patterns

### Domain-Driven Design

The application is divided into bounded contexts so business responsibilities remain isolated and explicit.

### Vertical Slice Architecture

Features are organized around use cases instead of forcing every request through a large collection of shared technical layers.

### CQRS

Commands and queries have separate responsibilities, making read and write concerns easier to evolve independently.

### Event-Driven Communication

RabbitMQ is used for asynchronous communication between services, reducing direct coupling and supporting eventual consistency.

### Outbox Pattern

Messages are persisted alongside business changes before being published, reducing the risk of losing events between a database transaction and message publication.

### Inbox / Idempotency

Consumers can safely handle duplicate messages without repeatedly applying the same business operation.

### gRPC

Internal synchronous communication can use gRPC where strongly typed service-to-service communication is appropriate.

---

## 🔐 Security

Authentication and authorization are handled with **Keycloak**, using **OpenID Connect / OAuth2** and JWT-based access tokens.

---

## 📊 Observability

The project includes an observability stack designed for distributed systems:

- **OpenTelemetry** — telemetry collection
- **Prometheus** — metrics
- **Grafana** — dashboards
- **Jaeger** — distributed tracing
- **Kibana / structured logging** — log analysis

---

## 🧪 Testing

- **JUnit** — unit testing
- **Mockito** — mocking dependencies
- **Testcontainers** — integration testing with real infrastructure dependencies
- **End-to-end testing** — validating complete business flows

Run tests with:

```bash
mvn test
```

---

## 🛠️ Technology Stack

**Backend:** Java, Spring Boot, Spring MVC, Spring Security, Spring Data JPA, Spring Data MongoDB, Spring AMQP, gRPC

**Data:** PostgreSQL, MongoDB, Redis, Flyway

**Infrastructure:** RabbitMQ, Docker, Docker Compose, Keycloak

**Observability:** OpenTelemetry, Prometheus, Grafana, Jaeger, Kibana

**Testing/API:** JUnit, Mockito, Testcontainers, OpenAPI/Swagger

---

## 🚀 Running the Project

### Prerequisites

- JDK 11+
- Docker & Docker Compose
- Maven, or the included Maven wrapper
- IntelliJ IDEA, Eclipse, or VS Code

### 1. Start infrastructure

```bash
docker-compose -f ./deployments/docker-compose/docker-compose.infrastructure.yaml up -d
```

### 2. Build the modules

```bash
mvn clean install
```

### 3. Run the services

```bash
mvn spring-boot:run
```

Run the gateway and individual services as required by the project structure.

### 4. Test the APIs

The repository includes `booking.rest` for exercising API flows through an HTTP client. Swagger/OpenAPI documentation is available through the configured Swagger UI endpoints when services are running.

---

## 📌 Project Status

🚧 **Work in progress.**

The core architecture and main services are implemented. Ongoing work focuses on production-readiness, testing coverage, deployment and documentation.

---

## 💡 What this project demonstrates

**Java · Spring Boot · Backend Engineering · Microservices · DDD · CQRS · Event-Driven Architecture · RabbitMQ · gRPC · PostgreSQL · MongoDB · Docker · Keycloak · Testing · Observability**

---

## 👨‍💻 Author

**Mohamed BAILLA** — Software Engineering Master's student

- GitHub: https://github.com/mohamedbailla599
- LinkedIn: https://www.linkedin.com/in/mohamed-bailla-5bb45b2aa

> Built as a practical software-engineering project to learn, experiment, and apply distributed-systems concepts.
