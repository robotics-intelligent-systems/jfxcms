# Coding Challenge

## Position:
Backend Java Developer (Spring Boot + MySQL)

## Title:
Candidate Management System for the Selection and Hiring Process

## Context: A company is developing a customer management system to offer a better user experience. A microservice is required to handle the registration, querying, and analysis of customer data using MySQL as the database.

The goal is for this service to be scalable, secure, and compliant with software development best practices.

## Requirements:
- Create new customers using an endpoint that allows registration of first name, last name, age, and date of birth.

- Query a set of metrics about existing customers, such as average age and standard deviation of ages.

- List all registered customers with their complete data and a derived calculation, such as an estimated date for a future event based on customer data (e.g., life expectancy).

## Additional Points:
- Design the service using a best practices approach based on design principles and architectural patterns. A clear separation of responsibilities between system layers is expected.

- Document the API using industry-standard tools to facilitate its consumption.

- Implement a persistence model to store client data.

- Apply security principles to ensure that only authorized users can interact with the service.

- Design the system considering its deployment in a cloud environment.

- The service must properly handle exceptions and return clear messages to API consumers, using HTTP codes appropriately (500, 401, 422, etc.).

- Include a suite of tests to validate the implemented functionality.

- Implement a mechanism to log and monitor service activity.

- Design the service to be scalable to handle increases in data volume or requests.

## Recommendations:
- The microservice must be functional and meet the requirements mentioned.
- The design and design decisions must be understandable through the code, documentation, or comments.

- The use of design patterns (e.g., Factory, Builder, or Repository) and architectural patterns (e.g., RESTful or event-driven) will be valued.

- The implementation must be efficient and follow best practices for Java and Spring Boot applications.
- Use Spring Data JPA, Spring Security, and Flyway.

- Use a build system such as Maven or Gradle.

- Include clear instructions on how to configure and run the application.

- Consider code modularity and reuse.

## Deliverables:
- GitHub repository with the source code.

- URL of the API deployed on AWS, Azure, or GCP, providing collaborator access to review the deployed code.

- Endpoint documentation in Swagger
- A Postman collection containing calls to each API, including a couple of pre-recorded cases (one with HTTP Status 200, successful, and one with 500, for error, 422 for business errors) for each endpoint.

## Optional:
- Implement a message queue to handle asynchronous client-related processes.

- Expose metrics in a format compatible with monitoring systems.