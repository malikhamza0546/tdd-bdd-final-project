# IBM Cloud IDE – Product Catalog Microservice (TDD & BDD)

![Python](https://img.shields.io/badge/Python-3.8-3776AB?logo=python)
![Flask](https://img.shields.io/badge/Flask-Backend-000000?logo=flask)
![Selenium](https://img.shields.io/badge/Selenium-BDD-43B02A?logo=selenium)
![Behave](https://img.shields.io/badge/Behave-Testing-333333)
![TDD](https://img.shields.io/badge/Testing-TDD-success)
![BDD](https://img.shields.io/badge/Testing-BDD-blue)
![SQLAlchemy](https://img.shields.io/badge/ORM-SQLAlchemy-red)

## Project Overview

This project demonstrates the development, integration, and testing of a **microservices-based Product Catalog Application** using a Cloud IDE with Docker.

The application allows administrators to maintain an e-commerce product catalog through an interactive web interface. The application consists of two main components that were rigorously tested using industry-standard methodologies:

- **Product REST API Microservice (Python):** A fully functional Create, Read, Update, Delete (CRUD) API. It was developed using strict **Test-Driven Development (TDD)**, ensuring high reliability, >95% code coverage, and a robust database design using SQLAlchemy.
- **Administrative Frontend (HTML, CSS, and JavaScript):** A pre-built user interface tested using **Behavior-Driven Development (BDD)**. Selenium WebDriver and Behave are used to simulate real user interactions and verify UI functionality.

The backend service is built with Flask and interacts with a relational database. The frontend communicates with the backend via RESTful HTTP requests. This project provided practical experience with API development, automated testing, browser automation, and cloud-based development environments.

---

## Project Objectives

The main objectives of this project are:

- Develop a Python-based backend microservice using Test-Driven Development (TDD).
- Write failing unit tests before implementing code to pass them.
- Achieve at least 95% code coverage using `nosetests`.
- Deploy and manage an ephemeral Cloud IDE and Docker environment.
- Integrate Selenium WebDriver and Behave for automated UI testing.
- Write BDD scenarios in Gherkin syntax to test administrative workflows.
- Implement step definitions to load background data and interact with the UI.
- Test Create, Read, Update, Delete (CRUD) and search functions via the UI.
- Troubleshoot application deployment, database connections, and automated testing issues.

---

## Architecture

The application follows a microservices architecture consisting of a backend REST API and a frontend UI connected via HTTP requests.

### Application Architecture

```mermaid
flowchart TD
    A[Admin User / Browser] --> B[Frontend Application]
    
    B -->|GET /products?name=...| C[Product REST API - Python/Flask]
    B -->|POST /products| C
    B -->|PUT /products/id| C
    B -->|DELETE /products/id| C
    
    C -->|JSON Data / Status Codes| B
    
    B --> D[Display Product List]
    B --> E[Display Success/Error Messages]
    B --> F[Update UI Form]


## Microservices Description

### 1. Product REST API Microservice – Python (Flask)

Responsible for retrieving, creating, updating, and deleting product information in the database.

Main API operations:

| Endpoint | Purpose |
|---|---|
| `GET /products` | Retrieves a list of products (supports search by name, category, and availability) |
| `GET /products/<id>` | Retrieves a single product by ID |
| `POST /products` | Creates a new product |
| `PUT /products/<id>` | Updates an existing product |
| `DELETE /products/<id>` | Deletes a product |

### 2. Administrative Frontend – HTML, CSS and JavaScript

Provides the user interface and coordinates communication with the backend service.

Main responsibilities:

- Load the full product catalog when the homepage opens.
- Provide a form to create new products and update existing ones.
- Provide search functionality by Name, Category, and Availability.
- Display dynamic success or error messages without refreshing the page.

---

## Frontend-to-Backend Communication

The frontend acts as the coordinator between the user and the backend microservice.

The application follows this workflow:

1. The user opens the frontend application.
2. The frontend sends an HTTP GET request to the Product API to retrieve the product list.
3. The frontend displays the products in a table.
4. When the user clicks "Create", a form is displayed.
5. The user fills out the form and submits it, sending an HTTP POST request to the API.
6. The frontend displays a success message and refreshes the product list.

---

## Repository Structure

```text
tdd-bdd-final-project/
│
├── service/
│   ├── models.py            # Database schema and ORM methods
│   ├── routes.py            # REST API endpoints
│   └── common/              # Error handlers, status codes, etc.
│
├── tests/
│   ├── factories.py         # Fake data generation using Faker
│   ├── test_models.py       # TDD unit tests for the database model
│   └── test_routes.py       # TDD unit tests for REST API endpoints
│
├── features/
│   ├── products.feature     # BDD scenarios (Gherkin syntax)
│   └── steps/
│       ├── load_steps.py    # Steps to load background data
│       └── web_steps.py     # Steps for Selenium UI interactions
│
├── bin/
│   └── setup.sh             # Script to initialize the environment
│
├── README.md
└── .gitignore


### Directory Description

| Directory / File | Description |
|---|---|
| `service/` | Contains the core application logic, models, and routes |
| `tests/` | Contains all TDD unit tests and fake data factories |
| `features/` | Contains BDD feature files and Behave step definitions |
| `bin/setup.sh` | Script to initialize the Python virtual environment |
| `README.md` | Project overview and technical documentation |

---

## Technologies and Tools

| Technology | Usage |
|---|---|
| Python 3.8 | Backend development and test automation |
| Flask | Backend API implementation |
| SQLAlchemy | ORM for database management |
| Unittest / Nose | TDD unit testing and coverage reporting |
| Behave | BDD test framework |
| Selenium | WebDriver for UI automation testing |
| Faker | Generation of fake product data for tests |
| Docker | Containerisation of the development environment |
| Git and GitHub | Version control and source code management |

---

# Practical Implementation

## 1. Environment Initialization

Configured the Cloud IDE environment and activated the Python virtual environment.

```bash
bash ./bin/setup.sh
2. Test-Driven Development (TDD) - Part 1
Developed the REST API by writing failing unit tests first, followed by the implementation.

Running Model Tests
bash
nosetests tests/test_models.py
Running Route Tests
bash
nosetests tests/test_routes.py
Checking Code Coverage
bash
coverage run -m nose
coverage report -m
3. Behavior-Driven Development (BDD) - Part 2
Created feature files to test the UI and step definitions to execute the scenarios.

Starting the Service
bash
honcho start
Running BDD Scenarios
bash
behave
4. BDD Scenarios Tested
The following 7 scenarios were written and successfully executed to ensure the UI functions correctly:

Read a Product: Search by name and retrieve the product.

Update a Product: Modify an existing product's details.

Delete a Product: Remove a product from the catalog.

List all Products: Ensure all items are displayed.

Search by Category: Filter products by category.

Search by Available: Filter by True or False availability.

Search by Name: Find specific products by their name.
