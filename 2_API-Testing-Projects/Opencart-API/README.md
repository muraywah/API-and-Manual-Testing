# OpenCart REST API – Cart Module | QA Testing

Manual API test suite for the OpenCart Cart Module, executed in Postman. Covers the full cart lifecycle — session creation, adding products, viewing cart contents, editing quantities, and removing items — with chained requests and environment variable management.

---

## Folder Contents

```
opencart-cart-api-tests/
├── test_cases.xlsx          ← All test cases (existing + new)
├── execution_report.md      ← Test execution report with scripts
└── README.md                ← This file
```

---

## Collection Overview

**Collection:** `Opencart_RestAPI_CartModule`

**Base URL:** `{{baseurl}}` (e.g. `https://demo.opencart.com/`)

**Authentication:** API Key (`api_token`) obtained from login and passed as a form/query param on all subsequent requests

### Endpoints

| # | Method | Endpoint | Purpose |
|---|--------|----------|---------|
| 1 | POST | `{{baseurl}}api/login` | Create session, get api_token |
| 2 | POST | `{{baseurl}}api/cart/add` | Add product to cart |
| 3 | GET | `{{baseurl}}api/cart/products` | Retrieve cart contents |
| 4 | POST | `{{baseurl}}api/cart/edit` | Edit product quantity |
| 5 | POST | `{{baseurl}}api/cart/remove` | Remove product from cart |

---

## Collection Variables Required

Set these in your Postman collection before running:

| Variable | Description | Example Value |
|----------|-------------|---------------|
| `baseurl` | Base URL of the OpenCart instance | `https://demo.opencart.com/` |
| `api_key` | Admin API key from OpenCart backend | `XW7Ky1yQ...` |
| `product_id` | ID of the product to test with | `42` |
| `quantity` | Initial quantity to add | `2` |

> `api_token_val` and `card_id_key` are set automatically by test scripts during the flow.

---

## Test Case Summary

| TC ID | Test Name | Type | Status |
|-------|-----------|------|--------|
| TC-001 | Create Session / Token | Existing | Pass |
| TC-002 | Add Product to Cart | Existing | Pass |
| TC-003 | Get Cart Contents | Existing | Pass |
| TC-004 | Edit Product Quantity | Existing | Pass |
| TC-005 | Remove Product from Cart | Existing | Pass |
| TC-006 | Add to Cart – Invalid Token | **New** | Pass |
| TC-007 | Add to Cart – Zero Quantity | **New** | Pass |
| TC-008 | Add to Cart – Invalid Product ID | **New** | Pass |
| TC-009 | Verify Cart Empty After Remove | **New** | Pass |
| TC-010 | Edit Quantity – Large Value | **New** | Pass |
| TC-011 | Remove – Non-Existent Cart Key | **New** | Pass |
| TC-012 | Session Token Still Valid After Add | **New** | Pass |

**Total: 12 | Pass: 12 | Fail: 0 | Pass Rate: 100%**

---

## Request Chain Flow

```
POST /api/login
  └─ Stores: api_token_val
        │
POST /api/cart/add
        │
GET  /api/cart/products
  └─ Stores: card_id_key
        │
POST /api/cart/edit
        │
POST /api/cart/remove
  └─ Clears: api_token_val, product_id, quantity
```

---

## What the New Tests Cover

The 7 new test cases extend coverage beyond the happy path:

- **TC-006** — Invalid authentication: confirms the API rejects bad tokens
- **TC-007** — Zero quantity edge case: validates boundary input handling
- **TC-008** — Invalid product ID: ensures non-existent products return a clear error
- **TC-009** — Post-removal state: confirms cart is empty after remove, not just silent
- **TC-010** — Oversized quantity: validates stock-limit or success behaviour at extremes
- **TC-011** — Remove ghost key: ensures removing a non-existent item doesn't crash
- **TC-012** — Session persistence: confirms the token remains valid across multiple calls

---

## Files Reference

- **`test_cases.xlsx`** — Open in Excel or Google Sheets. Yellow rows = new test cases. Contains TC ID, endpoint, request body, test scripts, expected results, and pass/fail status.
- **`execution_report.md`** — Full execution report including all Postman test scripts, assertion list, variable table, and chaining diagram.

---

*Tested by: [Your Name] | Date: [Date] | Tool: Postman*
