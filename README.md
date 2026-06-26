# 🚀 API Gateway
![Java](https://img.shields.io/badge/Java-21-blue)  ![Spring Boot|102](https://img.shields.io/badge/Spring_Boot-4.1.0-brightgreen)  ![Spring Config Server|128](https://img.shields.io/badge/Spring-Cloud_Gateway-orange)  ![Docker](https://img.shields.io/badge/Docker-Enabled-blue) ![Maven|72](https://img.shields.io/badge/Maven-4.0.0-brightgreen) 
## 📌 Overview

The API Gateway acts as the single entry point for all client requests in the microservices architecture. Instead of clients communicating directly with individual services, all requests pass through the gateway, which is responsible for routing, security, and cross-cutting concerns.

The gateway provides centralized request handling, allowing backend services to remain independent and focused on their business responsibilities.
## 🏗️ Role in the Whole System

### Request routing

```text
1. Client (X) sends request to API Gateway 

2. API Gateway check request authentication

3. API Gateway fetchs registry data from Eureka service registry to get info about up microservices.
   
4. API Gateway forwards the request to the appropriate microservice, and apply load balancing if multiple instances are up from the same microservice, using round robbin algorithm by default.

```

![Service registration](docs/APIGatewayRole.svg)
## ✨ Features

✅ Dynamic routing using service names.

✅ Load balancing across multiple service instances.

✅ JWT token validation.

✅ Request and response filtering.

✅ Rate limiting preventing abuse.

✅ Centralized logging.

✅ CORS configuration.

✅ SSL termination.
## 🛠️ Tech Stack

| Technology           | Purpose               |
| -------------------- | --------------------- |
| Spring Boot          | Application Framework |
| Spring Cloud Gateway | Request routing       |
| Docker               | Containerization      |
| Maven                | Build tool            |

## 📂 Project Structure

```text
api-gateway/
│
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── com/isag/erp/apigateway/
│   │   │       └── ApiGatewayApplication.java
│   │   │
│   │   └── resources/
│   │       └── application.yml
│   │
│   └── test/
│
├── Dockerfile
├── .dockerignore
├── pom.xml
└── README.md
```
## ▶️ Build and Run

### 1️⃣ Run Locally Using Docker

#### Prerequisites
1. Docker
2. Config Server Docker Container
#### Build the Project

```bash
mvn clean package
```

#### Build Docker Image

```bash
docker build -t api-gateway:v1.0 .
```

#### Run Container

```bash
docker run -d \
  -p 8080:8080 \
  -e CONFIG_SERVER_URL=<Link to config server> \
  --name api-gateway:v1.0 \
  api-gateway:v1.0
```

### 2️⃣ Run Locally Without Docker

#### Prerequisites
1. Java 17+
2. Maven 3+
3. Running Config Server
#### Set environment variables

Linux/macOS:

```bash
export CONFIG_SERVER_URL=<link to config server>
```

Windows:

```bash
set CONFIG_SERVER_URL=<link to config sever>
```
#### Build the Project

```bash
mvn clean install
```

#### Run the Service

```bash
mvn spring-boot:run
```

or

```bash
java -jar target/api-gateway.jar
```
## 📤 Output After Running

### The client only sends requests to:

```text
http://localhost:8080/
```
