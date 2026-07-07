# Technical Challenge - Description

## Technical Considerations:
- Use the Go (Golang) programming language for one API and Node.js for the other.

- Implement the solution using the Fiber framework for the Go API and Express.js for the Node.js API.

- Document the code clearly and concisely, following coding best practices.

- Use Docker to containerize the applications and facilitate their deployment in different environments.

- Implement communication between the two APIs using a mechanism such as HTTP.

- Use cloud services for the implementation and deployment of the applications.

## Solution Architecture:
- Go API: This API will receive the original array as input, perform the array rotation, and then send the resulting data to the second Node.js API.

- Node.js API: This API will receive the rotated array data from the Go API, calculate statistics on the data, and return these statistics as a result.

## Required Functionality:
- Create two RESTful APIs:

- A Go API that receives as input an array of number arrays representing a rectangular array and returns the QR factorization of that array.

- Another Node.js API that receives the result of the arrays returned by the first API and performs an additional operation on the data. (*) Details in the Additional Operations section.
- Implement the logic to perform the array rotation and the additional operation efficiently and correctly in each API.

## Optional Functionality:
- Implement a frontend that consumes both APIs and displays the results of the array rotation and the additional statistics.

- Apply a security layer using JWT to protect the API queries.

- Implement unit and integration tests to ensure code quality in both APIs.

## Additional Operation:
- The second API will calculate the following on the returned array data:

- Maximum value: The maximum value found in the arrays.

- Minimum value: The minimum value found in the arrays.

- Average: The average of all array values.

- Total sum: The total sum of all array values.

- Diagonal array: Check if any array is diagonal.

## Considerations:
- There is no specific standard for the names of the created objects, but consistency in their structure and documentation is expected.

- If there are any doubts regarding the job description, the candidate is expected to make informed decisions and support them during the interview.

- The efficiency and elegance of the implemented solution will be valued, as well as the candidate's ability to communicate and defend their technical decisions.