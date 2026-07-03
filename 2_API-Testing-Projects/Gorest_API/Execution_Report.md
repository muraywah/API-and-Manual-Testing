# API Test Execution Report

## Project Information

| Item               | Details                          |
| ------------------ | -------------------------------- |
| **Project**        | GoRest API Chaining Testing      |
| **Application**    | GoRest Public API                |
| **Base URL**       | `https://gorest.co.in/public/v2` |
| **Authentication** | Bearer Token Authentication      |
| **Execution Type** | Manual API Testing (Postman)     |

---

## Execution Summary

| Metric                    | Value |
| ------------------------- | ----- |
| Total Endpoints Tested    | 5     |
| Total Test Cases Executed | 5     |
| Passed                    | 5     |
| Failed                    | 0     |
| Pass Rate                 | 100%  |

---

## HTTP Methods Used

* POST
* GET
* PUT
* DELETE

---

## Validation Performed

* HTTP Status Code Validation
* Response Body Validation
* JSON Structure Validation
* Data Integrity Validation
* Environment Variable Validation
* API Chaining Validation
* Authentication Validation
* CRUD Operation Validation
* Dynamic Test Data Validation
* Response Content Verification
* Variable Extraction and Reuse Validation
* Environment Cleanup Validation

---

## Endpoints Tested

| Endpoint                   | Purpose                 | Expected Status |
| -------------------------- | ----------------------- | --------------- |
| `POST /users`              | Create User             | 201 Created     |
| `GET /users/{{userid}}`    | Retrieve User Data      | 200 OK          |
| `PUT /users/{{userid}}`    | Update User Information | 200 OK          |
| `DELETE /users/{{userid}}` | Delete User             | 204 No Content  |

---

## End-to-End CRUD Workflow

The following API chaining workflow was successfully executed:

```text
Create User
     ↓
Retrieve User
     ↓
Update User
     ↓
Delete User
```

**Result:** Successful end-to-end CRUD validation.

---

## Environment Variables Used

| Variable               |
| ---------------------- |
| `{{auth_secret_0emk}}` |
| `{{userid}}`           |
| `{{email_env}}`        |
| `{{name_env}}`         |

---

## Assertions Executed

* Status code validation
* Response field existence validation
* Response value verification
* User ID extraction and storage
* Environment variable creation
* Environment variable reuse
* Updated data verification
* Data consistency across requests
* Environment cleanup after deletion

---

## Test Result

✅ All API requests executed successfully.

✅ Authentication was validated successfully.

✅ CRUD operations completed without errors.

✅ Environment variables were correctly created, stored, reused, and cleared.

✅ Data consistency was maintained throughout the API chaining workflow.

### Final Status: PASSED
