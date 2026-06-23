API TEST EXECUTION REPORT

Project: GoRest API Chaining Testing

Application: GoRest Public API

Base URL: https://gorest.co.in/public/v2

Authentication: Bearer Token Authentication

Execution Type: Manual API Testing (Postman)

Total Endpoints Tested: 5

Total Test Cases Executed: 5

Passed: 5

Failed: 0

Pass Rate: 100%

Methods Used:

POST
GET
PUT
DELETE

Validation Performed:

HTTP Status Code Validation
Response Body Validation
JSON Schema / Structure Validation
Data Integrity Validation
Environment Variable Validation
API Chaining Validation
Authentication Validation
CRUD Operation Validation
Dynamic Test Data Validation
Response Content Verification
Variable Extraction and Reuse Validation
Environment Cleanup Validation

Endpoints Tested:

POST /users
Create User
Status Code: 201 Created
GET /users
Retrieve User Data
Status Code: 200 OK
PUT /users/{{userid}}
Update User Information
Status Code: 200 OK
DELETE /users/{{userid}}
Delete User
Status Code: 204 No Content
Full CRUD Chaining Flow
Create → Read → Update → Delete
End-to-End Validation

Environment Variables Used:

{{auth_secret_0emk}}
{{userid}}
{{email_env}}
{{name_env}}

Assertions Executed:

- Status code validation

- Response field existence validation

- Response value verification

- User ID extraction and storage

- Environment variable creation

- Environment variable reuse

- Updated data verification

- Data consistency across requests

- Environment cleanup after deletion