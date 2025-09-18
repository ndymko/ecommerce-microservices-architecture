# E-Commerce Microservices Architecture

This repository contains the `docker-compose.yml` file for launching a full-featured e-commerce platform using prebuilt microservices hosted on Docker Hub.

## 🏗️ Architecture Overview

![Architecture Diagram](./architecture.png)

## ⚙️ Technologies

- Spring Boot (MVC & WebFlux)
- Kafka & Schema Registry  
- Redis  
- MySQL & MongoDB  
- Flyway (database migrations)
- Docker & Docker Compose  
- Resilience4j  
- Keycloak (OAuth2 / OpenID Connect)  
- Spring Security  
- Wiremock, Mockito, Testcontainers (testing)

## 🧩 Included Services

- **Security Client** (https://github.com/Mitohondriyaa/security-client) – Returns an access token from Keycloak via an internal client using password credentials flow
- **API Gateway** (https://github.com/Mitohondriyaa/api-gateway) – Routes requests & handles authentication (JWT)
- **Product Service** (https://github.com/Mitohondriyaa/product-service) – Manages product catalog
- **Order Service** (https://github.com/Mitohondriyaa/order-service) – Processes orders 
- **Inventory Service** (https://github.com/Mitohondriyaa/inventory-service) – Tracks stock levels  
- **Notification Service** (https://github.com/Mitohondriyaa/notification-service) – Sends email notifications  
- **Keycloak** – Provides authentication & authorization  
- **Kafka + Schema Registry** – Enables asynchronous communication  
- **Kafka UI** – Provides a web interface for monitoring and managing Kafka topics and consumers
- **Redis** – Provides idempotency & caching  
- **MySQL / MongoDB** – Store persistent data  

## ⚙️ Environment Variables

### 🛒 Product Service

| Variable Name         | Description                         | Example Value            |
|-----------------------|-------------------------------------|--------------------------|
| `REDIS_CACHE_HOST`    | Hostname for Redis cache            | `redis-cache-product`    |
| `REDIS_CACHE_PORT`    | Port for Redis used for product cache                | `6379`                   |
| `REDIS_COUNTER_HOST`  | Hostname for Redis used for product counter          | `redis-counter-product`  |
| `REDIS_COUNTER_PORT`  | Port for Redis counter              | `6379`                   |
| `DB_HOST`             | Hostname of MongoDB                    | `mongodb-product`        |
| `DB_PORT`             | Port of MongoDB                        | `27017`                  |
| `DB_USERNAME`         | Username for MongoDB                | `root`                   |
| `DB_PASSWORD`         | Password for MongoDB                | `password`               |
| `AUTH_SERVER_URL`     | Keycloak auth server URL            | `http://keycloak:8080`   |
| `AUTH_SERVER_REALM`   | Keycloak realm                      | `microservices-realm`    |
| `KAFKA_BOOTSTRAP_SERVERS`    | Kafka bootstrap servers              | `kafka-1:9092,kafka-2:9092`         |
| `SCHEMA_REGISTRY_URL`        | Schema Registry endpoint            | `http://schema-registry:8081`       |

### 🧾 Order Service

| Variable Name              | Description                           | Example Value                          |
|----------------------------|---------------------------------------|----------------------------------------|
| `INVENTORY_URL`            | URL to Inventory Service              | `http://inventory-service:8082`        |
| `PRODUCT_URL`              | URL to Product Service                | `http://product-service:8080`          |
| `DB_HOST`                  |  Hostname of MySQL                    | `mysql-order`                          |
| `DB_PORT`                  | Port of MySQL                         | `3306`                                 |
| `DB_USERNAME`              | Username for MySQL                    | `root`                                 |
| `DB_PASSWORD`              | Password for MySQL                    | `password`                             |
| `AUTH_SERVER_URL`          | Keycloak auth server URL              | `http://keycloak:8080`                 |
| `AUTH_SERVER_REALM`        | Keycloak realm                        | `microservices-realm`                  |
| `KAFKA_BOOTSTRAP_SERVERS`  | Kafka bootstrap servers               | `kafka-1:9092,kafka-2:9092`            |
| `SCHEMA_REGISTRY_URL`      | Schema Registry endpoint      | `http://schema-registry:8081`          |

### 📦 Inventory Service

| Variable Name                | Description                              | Example Value                          |
|------------------------------|------------------------------------------|----------------------------------------|
| `REDIS_IDEMPOTENCY_HOST`     | Hostname for Redis used for idempotency  | `redis-idempotency-inventory`          |
| `REDIS_IDEMPOTENCY_PORT`     | Port for Redis idempotency               | `6379`                                 |
| `DB_HOST`                    | Hostname of MySQL                        | `mysql-inventory`                      |
| `DB_PORT`                    | Port of MySQL                            | `3306`                                 |
| `DB_USERNAME`                | Username for MySQL                       | `root`                                 |
| `DB_PASSWORD`                | Password for MySQL                       | `password`                             |
| `AUTH_SERVER_URL`            | Keycloak auth server URL                 | `http://keycloak:8080`                 |
| `AUTH_SERVER_REALM`          | Keycloak realm                           | `microservices-realm`                  |
| `KAFKA_BOOTSTRAP_SERVERS`    | Kafka bootstrap servers                  | `kafka-1:9092,kafka-2:9092`            |
| `SCHEMA_REGISTRY_URL`        | Schema Registry endpoint         | `http://schema-registry:8081`          |

### 📬 Notification Service

| Variable Name                | Description                              | Example Value                          |
|------------------------------|------------------------------------------|----------------------------------------|
| `REDIS_IDEMPOTENCY_HOST`     | Hostname for Redis used for idempotency  | `redis-idempotency-notification`       |
| `REDIS_IDEMPOTENCY_PORT`     | Port for Redis idempotency               | `6379`                                 |
| `KAFKA_BOOTSTRAP_SERVERS`    | Kafka bootstrap servers                  | `kafka-1:9092,kafka-2:9092`            |
| `SCHEMA_REGISTRY_URL`        | URL to Confluent Schema Registry         | `http://schema-registry:8081`          |
| `MAIL_HOST`                  | SMTP mail server host                    | `sandbox.smtp.mailtrap.io`             |
| `MAIL_PORT`                  | SMTP mail server port                    | `2525`                                 |
| `MAIL_USERNAME`              | SMTP username                            | `h9gh359h3384gj`                        |
| `MAIL_PASSWORD`              | SMTP password                            | `328hf28fcnmito`                        |

### 🌐 API Gateway

| Variable Name             | Description                           | Example Value                       |
|---------------------------|---------------------------------------|-------------------------------------|
| `INVENTORY_URL`           | URL to Inventory service              | `http://inventory-service:8082`     |
| `PRODUCT_URL`             | URL to Product service                | `http://product-service:8080`       |
| `ORDER_URL`               | URL to Order service                  | `http://order-service:8081`         |
| `AUTH_SERVER_URL`         | Keycloak auth server URL           | `http://keycloak:8080`              |
| `AUTH_SERVER_REALM`       | Keycloak realm                   | `microservices-realm`               |

### 🔐 Security Client

| Variable Name        | Description                       | Example Value                          |
|----------------------|-----------------------------------|----------------------------------------|
| `CLIENT_ID`          | Keycloak Client ID                  | `security-client`                      |
| `CLIENT_SECRET`      | keycloak Client Secret              | `vCSZ0cAynvIvpsxbWvFQg1UVBsyc8AXb`     |
| `USER_LOGIN`         | Keycloak User Login                   | `test-user`                            |
| `USER_PASSWORD`      | Keycloak User Password                | `12345`                                |
| `AUTH_SERVER_URL`    | Keycloak auth server URL       | `http://keycloak:8080`                 |
| `AUTH_SERVER_REALM`  | Keycloak realm               | `microservices-realm`                  |

### ⚡ Example Workflow

### 1. Get access token

Send a GET request to `http://localhost:8084/api/access-token`


### 2. Create a product

Send a POST request to `http://localhost:9000/api/product` with JSON body:

```json
{
  "name": "some name",
  "description": "some description",
  "price": 100
}
```

### 3. Increase product quantity in Inventory Service

After product creation, an inventory record with quantity 0 is automatically created via Kafka.  
Next, send a POST request to `http://localhost:9000/api/inventory` with JSON body:

```json
{
    "productId": "892hf92f23jf32qf",
    "quantity": 100
}
```

### 4. Place order

Send a POST request to `http://localhost:9000/api/order` with JSON body to order products:

```json
{
    "productId": "892hf92f23jf32qf",
    "quantity": 10
}
```

### 5. Receive notification

After the order is successfully processed and inventory is reserved, Notification Service sends an email confirmation to the customer.

The notification is triggered automatically based on Kafka events.

Example email content:

```
Hi, Alexander Sidorov,

Thank you for your order!

Your order #7d5cdd00-9540-4420-9437-35259ca5066b has been placed successfully!

Best regards,
Mitohondriyaa
```

## 🚀 Getting Started

> Make sure you have [Docker](https://www.docker.com/) and [Docker Compose](https://docs.docker.com/compose/) installed.

```bash
git clone https://github.com/Mitohondriyaa/ecommerce-microservices-architecture
cd ecommerce-microservices-architecture
docker-compose up -d
```

If you encounter permission issues with Kafka data directories after running Docker Compose, run:

```bash
sudo chown -R 1001:1001 ./kafka-1-data ./kafka-2-data
```

## 📚 API Documentation

Access the full Swagger documentation through the API Gateway:

👉 [Swagger UI](http://localhost:9000/swagger-ui.html)
