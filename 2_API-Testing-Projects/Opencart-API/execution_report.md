# OpenCart REST API - Cart Module Execution Report

**Date:** July 4, 2026  
**Test Suite:** Cart Module End-to-End Functional Test  
**Environment:** Postman Automation Environment (`{{baseurl}}`)  
**Total Test Cases:** 5  
**Passed:** 5 | **Failed:** 0 | **Success Rate:** 100%
**Total Assertions:** 23  
**Passed:** 23 | **Failed:** 0 | **Success Rate:** 100%

---

## 1. Executive Summary
This execution report provides a detailed breakdown of the automated test run performed on the **OpenCart REST API - Cart Module**. The test suite covers the complete product lifecycle inside a shopping cart from session initialization and product insertion to retrieving cart states, modifying quantities, and post-test data cleanup. All 5 test cases passed successfully with zero assertion failures.

---

## 2. Test Execution Dashboard

| Metric | Value |
| :--- | :--- |
| **Total Test Cases** | 5 |
| **Passed** | 5 |
| **Failed** | 0 |
| **Blocked** | 0 |
| **Totol Assertions** | 23 |
| **Passed** | 23 |
| **Execution Status** | **100% PASS** |

---

## 3. Detailed Test Case Execution Results

### TC-001: Create Session (`/api/login`)
* **Description:** Initializes an API session, validates the response structure, and securely stores the session token.
* **Method / URL:** `POST` `{{baseurl}}api/login`
* **Expected Status:** `200 OK`
* **Execution Status:** **PASS**
* **Assertions Evaluated:**
  * Status code is 200.
  * Success message matches `"Success: API session successfully started!"`.
  * `api_token` is a valid string and is not empty.
  * Response time is below 3000ms.
* **Variables Management:** `SET: api_token_val`

### TC-002: Add Product (`/api/cart/add`)
* **Description:** Adds a product to the cart using the session token and verifies the success message.
* **Method / URL:** `POST` `{{baseurl}}api/cart/add`
* **Expected Status:** `200 OK`
* **Execution Status:** **PASS**
* **Assertions Evaluated:**
  * Status code is 200.
  * Success message matches `"Success: You have modified your shopping cart!"`.
  * Response body is not empty.
  * Response time is below 3000ms.
* **Variables Management:** None (`—`)

### TC-003: Get Cart (`/api/cart/products`)
* **Description:** Retrieves current cart items, extracts the dynamic `cart_id`, and validates the schema layout.
* **Method / URL:** `GET` `{{baseurl}}api/cart/products`
* **Expected Status:** `200 OK`
* **Execution Status:** **PASS**
* **Assertions Evaluated:**
  * Status code is 200.
  * Products array is not empty.
  * First product contains a valid string name.
  * First product has a quantity field.
  * `card_id_key` was saved successfully to the environment.
* **Variables Management:** `SET: card_id_key`

### TC-004: Edit Quantity (`/api/cart/edit`)
* **Description:** Updates the quantity of a specific item inside the cart to `4` and validates the update message.
* **Method / URL:** `POST` `{{baseurl}}api/cart/edit`
* **Expected Status:** `200 OK`
* **Execution Status:** **PASS**
* **Assertions Evaluated:**
  * Status code is 200.
  * Success message matches `"Success: You have modified your shopping cart!"`.
  * Response body is not empty.
  * Response time is below 3000ms.
* **Variables Management:** None (`—`)

### TC-005: Remove Product (`/api/cart/remove`)
* **Description:** Removes the item from the cart using `card_id_key` and unsets temporary environment variables to ensure state cleanliness.
* **Method / URL:** `POST` `{{baseurl}}api/cart/remove`
* **Expected Status:** `200 OK`
* **Execution Status:** **PASS**
* **Assertions Evaluated:**
  * Status code is 200.
  * Success message matches `"Success: You have modified your shopping cart!"`.
  * `api_token_val`, `product_id`, and `quantity` variables were cleared from the collection context.
  * Response time is below 3000ms.
* **Variables Management:** `UNSET: api_token_val, product_id, quantity`

---

## 4. Key Takeaways & Recommendations
* **Performance Standards Met:** Every single request returned well within the targeted `< 3000ms` baseline.
* **Environment Cleanliness:** Post-conditions effectively tore down the temporary variables (`api_token_val`, `product_id`, `quantity`), eliminating the risk of test pollution or stale state crossovers in subsequent runs.
