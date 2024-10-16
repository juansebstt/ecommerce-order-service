# E-commerce Order Service

## Overview

The **E-commerce Order Service** is responsible for managing orders placed by users in the e-commerce platform. It handles order creation, updates, status tracking, and integrates with various other microservices such as the **Cart Service**, **Payment Service**, and **Notification Service**. This service ensures that once a cart is finalized, an order is created, processed, and tracked until delivery.

## Features

- **Order Creation**: Transforms a finalized shopping cart into an order.
- **Order Status Tracking**: Manages the state of the order (e.g., pending, shipped, delivered).
- **Payment Integration**: Communicates with the **Payment Service** to process payments.
- **Notification Integration**: Notifies users about the status of their orders via the **Notification Service**.

## Technologies Used

- **Java**
- **Spring Boot**
- **Maven** (for dependency management)
- **PostgreSQL** (for order data storage)

## Prerequisites

Before running this service, ensure you have the following:

- **Java JDK 11 or higher**
- **Maven** (for building the project)
- A running **PostgreSQL** database (or other supported database).
- Access to the relevant microservices (e.g., Cart Service, Payment Service, Notification Service).

## Installation

1. Clone the repository:

    ```bash
    git clone https://github.com/juansebstt/ecommerce-order-service.git
    ```

2. Navigate to the project directory:

    ```bash
    cd ecommerce-order-service
    ```

3. Build the project using Maven:

    ```bash
    mvn clean install
    ```


## Configuration

You need to configure the database and application settings in your `application.yml` or `application.properties` file.

### Sample Configuration

```yaml
server:
  port: 8086

spring:
  datasource:
    url: jdbc:postgresql://localhost:5432/ecommerce_order_db
    username: yourUsername
    password: yourPassword
    driver-class-name: org.postgresql.Driver

  jpa:
    hibernate:
      ddl-auto: update
    show-sql: true

  application:
    name: ecommerce-order-service
```

## Inter-Service Communication

The **E-commerce Order Service** communicates with the following microservices:

- **[E-commerce Cart Service](https://github.com/juansebstt/ecommerce-cart-service)**:
    - Transforms the cart data into an order when the user finalizes their cart.
- **[E-commerce Payment Service](https://github.com/juansebstt/ecommerce-payment-service):**
    - Processes payments for orders and updates the order status based on payment success or failure.
- **[E-commerce Notification Service](https://github.com/juansebstt/ecommerce-notification-service)**:
    - Sends order confirmation and status updates to users.
- **[E-commerce Catalog Service](https://github.com/juansebstt/ecommerce-catalog-service)**:
    - Validates product availability before finalizing the order.
- **[E-commerce User Service](https://github.com/juansebstt/ecommerce-user-service)**:
    - Manages user-related information associated with the order.
- **[E-commerce API Gateway](https://github.com/juansebstt/ecommerce-api-gateway)**:
    - Routes order-related requests from the frontend.

## Usage

### Creating an Order

To create an order, make a POST request to the `/orders/create` endpoint with the following payload:

```json
{
  "userId": "user-001",
  "cartId": "cart-123",
  "paymentMethod": "credit-card"
}
```

### Checking Order Status

To check the status of an order, make a GET request to the `/orders/{orderId}/status` endpoint.

```json
{
  "orderId": "order-001"
}
```

### Order Status Flow

- **Pending**: The order is awaiting payment confirmation.
- **Processing**: The order is being prepared for shipment.
- **Shipped**: The order has been shipped.
- **Delivered**: The order has been delivered to the user.
- **Cancelled**: The order has been cancelled.

## Testing

You can use tools like **Postman** or **curl** to test the various API endpoints. Ensure proper authentication if the service is secured.

## Contributing

Feel free to submit pull requests or open issues if you find bugs or want to contribute to the project.