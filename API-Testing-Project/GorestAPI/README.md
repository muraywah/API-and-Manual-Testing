GoRest API Chaining Testing Project

Overview

This project demonstrates manual API testing using the GoRest Public API.
It focuses on validating REST API endpoints through a complete CRUD workflow and implementing API chaining using Postman.

The main objective is to simulate a real-world user lifecycle by creating, retrieving, updating, and deleting a user while maintaining data consistency across reques


Base Information

Application: GoRest Public API
Base URL: https://gorest.co.in/public/v2
Testing Tool: Postman
Authentication: Bearer Token
Test Type: Manual API Testing
Scope: CRUD Operations 

Project Objectives

- Validate REST API endpoints for user management
- Perform end-to-end CRUD testing
- Implement API chaining using environment variables
- Generate dynamic test data for each request
- Validate response status codes and response bodies
- Ensure data consistency across all API calls
- Handle environment setup and cleanup properly

API Endpoints Tested

POST /users – Create a new user
GET /users – Retrieve user details
PUT /users/{userid} – Update existing user
DELETE /users/{userid} – Delete user

Test Scenario

The project validates a full user lifecycle:

Create user using POST request
Retrieve user using GET request
Update user using PUT request
Delete user using DELETE request

Each request is dependent on data passed from the previous request using Postman environment variables.

Environment Variables Used

auth_secret_0emk – Bearer authentication token
userid – Stores user ID from create response
email_env – Stores dynamically generated email
name_env – Stores dynamically generated name

Validations Performed

- HTTP status code validation
- Response body validation
- JSON structure validation
- API chaining validation
- Authentication validation
- Data integrity validation
- Environment variable extraction and reuse
- Environment cleanup validation

Execution Summary

Total Test Cases: 5
Passed: 5
Failed: 0
Pass Rate: 100 percent

Methods Used: POST, GET, PUT, DELETE

Status Codes Verified:
201 Created for POST
200 OK for GET and PUT
204 No Content for DELETE

Key Features

- End-to-end CRUD lifecycle testing
- Dynamic data generation to avoid duplicate email issues
- API chaining using Postman environment variables
- Real-time response validation
- Clean environment reset after test execution