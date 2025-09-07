# Patient Management App

A cloud-native, microservices-based Patient Management System built using Java, Spring Boot, Kafka, gRPC, Docker, postgreSQL and AWS. This project demonstrates scalable, secure, and fault-tolerant architecture leveraging containerization technologies.

---

## ✅ **Architecture Overview**

<img width="5284" height="2084" alt="image" src="https://github.com/user-attachments/assets/a7c335e0-473e-425e-9678-acb169bbe2bc" />



The system is deployed within a Virtual Private Cloud (VPC) and follows best practices for microservices architecture:

### External Access
- **Frontend Client** sends requests to the system through the **Application Load Balancer (ALB)**.

### Network Design
- **Public Subnet**: Hosts the ALB for routing incoming traffic.
- **Private Subnet**: Hosts the core microservices, databases, and messaging systems for security and scalability.

### ECS Cluster
All services are implemented as **ECS tasks running within ECS services** to ensure high availability and load balancing:

- **API Gateway** – Central routing layer exposing REST endpoints.
- **Auth Service** – Manages user authentication and authorization.
- **Patient Service** – Handles patient data management, produces Kafka events, and communicates with the Billing Service via gRPC.
- **Billing Service** – Handles payment-related operations, exposed as a gRPC server.
- **Analytics Service** – Consumes Kafka events to process patient-related analytics.

### Databases
- **RDS (Relational Database Service)**: Used for storing service-specific data.
  - `Auth DB`: Contains authentication and user-related data.
  - `Patient DB`: Stores patient profiles and medical history.

### Messaging
- **MSK (Managed Streaming for Apache Kafka)**: Facilitates asynchronous communication between services.
  - Topic: `patient`, used by producers (Patient Service) and consumers (Analytics Service).

---

## ✅ **Technologies Used**

### Core Stack
- Java 21
- Spring Boot, Spring Cloud, Spring Security
- REST APIs and gRPC for client-service and inter-service communication
- Kafka for event-driven architecture
- Docker for containerization

### Security
- Network isolation with private subnets
- Authentication via JWT/OAuth2 (integrated with Auth Service)
- Secure communication over HTTPS and internal channels

### Testing
- Unit and integration tests using **JUnit 5**

### AWS Infrastructure
- ECS (Elastic Container Service) for orchestrating containers
- RDS for managed relational databases
- MSK for distributed messaging
- ALB for routing traffic
- VPC with segregated public and private subnets

---
