
# DroolEngineProject

## Overview

DroolEngineProject is a Spring Boot application that integrates the Drools rule engine to process business rules for order discounts and claim risk levels. This application allows for dynamic rule management, enabling you to define, update, and apply custom rules to orders and claims via a RESTful API.

The project implements two key functionalities:

1. **Order Discount Processing**: Calculates discounts based on order attributes such as card type and price.
2. **Claim Risk Evaluation**: Determines the risk level of insurance claims based on predefined rules.

You can easily add, manage, and update rules through the provided API.

## Key Features

- **Dynamic Rule Management**: Define new rules for orders and claims via the API.
- **Drools Integration**: Leverage the Drools engine to process complex business logic.
- **REST API**: Expose endpoints to apply rules to orders and claims.
- **Persistence**: Store rules using Spring Data JPA with an underlying database.

## Project Structure

- `com.springproject.droolEngineProject`
  - `service`: Contains the business logic for processing orders and claims.
  - `controller`: RESTful controllers for handling API requests.
  - `model`: Defines the data models (e.g., `Order`, `Claim`, `Rule`).
  - `repo`: JPA repository for managing rule persistence.
  - `config`: Configuration files for setting up the Drools environment.
  - `rules`: Contains the DRL (Drools Rule Language) files for predefined business rules.

## APIs

### 1. Order Discount API

- **POST** `/getDiscount`: Apply discount rules to an order.

  **Request**:

    {
      "name": "first",
      "cardType": "MASTERCARD",
      "price": 50000
    }

  **Response**:

    {
      "name": "first",
      "cardType": "MASTERCARD",
      "discount": 10,
      "price": 50000
    }

### 2. Claim Risk Evaluation API

- **POST** `/api/getClaimRisk`: Evaluate the risk level of a claim.

  **Request**:

    {
      "type": "high"
    }

  **Response**:

    {
      "type": "high",
      "riskLevel": "High",
      "message": "High risk claim detected."
    }

### 3. Manage Rules API

- **POST** `/rule`: Add a new rule.

  **Request**:

    {
      "ifcondition": "orderObject: Order(cardType == "MasterCard" && price > 4000)",
      "thencondition": "orderObject.setDiscount(50)",
      "version": "1"
    }

- **GET** `/rules`: Retrieve all rules.

  **Response**:

    [
      {
        "id": 1,
        "ifcondition": "orderObject: Order(cardType == "MasterCard" && price > 4000)",
        "thencondition": "orderObject.setDiscount(50)",
        "version": 1
      }
    ]

## Running the Application

### Prerequisites

- Java 11+
- Maven
- Docker (optional for database)

### Build and Run

1. Clone the repository:

    git clone https://github.com/your-repo/droolEngineProject.git
    cd droolEngineProject

2. Build the project:

    mvn clean install

3. Run the application:

    mvn spring-boot:run

4. Access the APIs via http://localhost:8080.

## Customizing Rules

You can define custom rules for processing orders and claims by adding or updating the rules through the provided API endpoints. 

For example, to add a new rule:

    {
      "ifcondition": "orderObject: Order(cardType == "Visa" && price > 10000)",
      "thencondition": "orderObject.setDiscount(15)",
      "version": "1"
    }

## Technologies Used

- Spring Boot: Framework for building Java-based applications.
- Drools: A rule engine for processing business logic.
- Spring Data JPA: For data persistence.
- RESTful API: For interacting with the rule engine.
- Maven: Build and dependency management.

## Contributing

Contributions are welcome! Please create a pull request or submit an issue.

## License

This project is licensed under the MIT License.
