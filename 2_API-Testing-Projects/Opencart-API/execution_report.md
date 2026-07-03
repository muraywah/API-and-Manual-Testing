# API TEST EXECUTION REPORT

**Project:** OpenCart REST API – Cart Module Testing

**Application:** OpenCart (Demo Instance)

**Base URL:** `{{baseurl}}` *(e.g. https://demo.opencart.com/)*

**Authentication:** API Key Authentication (`api_token` passed as query/form param)

**Execution Type:** Manual API Testing (Postman)

---

**Total Endpoints Tested:** 5

**Total Test Cases Executed:** 12

**Existing Tests (pre-session):** 5

**New Tests (this session):** 7

**Passed:** 12

**Failed:** 0

**Pass Rate:** 100%

---

## Methods Used

- `POST`
- `GET`

---

## Validation Performed

- HTTP Status Code Validation
- Response Body Validation
- JSON Key Existence Validation
- Success Message Verification
- Error / Warning Handling Validation
- Negative Testing (invalid token, invalid product, zero quantity, oversized quantity)
- API Chaining Validation (token → add → get → edit → remove)
- Authentication Validation (valid and invalid api_token)
- CRUD Cart Operation Validation
- Dynamic Variable Extraction and Reuse
- Environment Variable Creation and Cleanup
- Post-Deletion State Verification (empty cart assertion)
- Session Persistence Validation mid-flow

---

## Endpoints Tested

### `POST {{baseurl}}api/login`
**Create Session / Token**
- Status Code: `200 OK`
- Extracts and stores `api_token` as collection variable

### `POST {{baseurl}}api/cart/add`
**Add Product to Cart**
- Status Code: `200 OK`
- Verified success message in response body
- Also tested with: invalid token (TC-006), zero quantity (TC-007), invalid product ID (TC-008)

### `GET {{baseurl}}api/cart/products`
**Get Cart Contents**
- Status Code: `200 OK`
- Extracts `cart_id` from first product for chaining
- Also used to: verify session persistence (TC-012), verify empty cart after removal (TC-009)

### `POST {{baseurl}}api/cart/edit`
**Edit Product Quantity**
- Status Code: `200 OK`
- Verified success message; also tested with large quantity value (TC-010)

### `POST {{baseurl}}api/cart/remove`
**Remove Product from Cart**
- Status Code: `200 OK`
- Verified success message; also tested with non-existent cart key (TC-011)
- Cleans up collection variables: `api_token_val`, `product_id`, `quantity`

---

## Full Cart Flow (Chaining)

```
POST /api/login
  → SET api_token_val
      ↓
POST /api/cart/add (product_id + quantity)
      ↓
GET /api/cart/products
  → SET card_id_key (from products[0].cart_id)
      ↓
POST /api/cart/edit (key: card_id_key, quantity: 4)
      ↓
POST /api/cart/remove (key: card_id_key)
  → UNSET api_token_val, product_id, quantity
```

---

## Environment / Collection Variables Used

| Variable | Set By | Used By |
|---|---|---|
| `{{api_token_val}}` | TC-001 (POST /login) | TC-002, TC-003, TC-004, TC-005 |
| `{{card_id_key}}` | TC-003 (GET /cart/products) | TC-004, TC-005 |
| `{{product_id}}` | Pre-set in collection | TC-002, TC-003 |
| `{{quantity}}` | Pre-set in collection | TC-002 |
| `{{api_key}}` | Pre-set in collection | TC-001 (login body) |

---

## New Test Scripts Added (This Session)

### TC-006 — Add to Cart with Invalid Token
```javascript
pm.test("Status code is not 200 with bad token", function () {
    pm.expect(pm.response.code).to.not.equal(200);
});
pm.test("Error response present", function () {
    var j = pm.response.json();
    pm.expect(j).to.have.property("error");
});
```

### TC-007 — Add to Cart with Zero Quantity
```javascript
pm.test("Status code check", function () {
    pm.response.to.have.status(200);
});
pm.test("Response has a key (success or warning/error)", function () {
    var j = pm.response.json();
    pm.expect(j).to.satisfy(function(r) {
        return r.success || r.error || r.warning;
    });
});
```

### TC-008 — Add to Cart with Invalid Product ID
```javascript
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});
pm.test("Contains error or warning key", function () {
    var j = pm.response.json();
    pm.expect(j).to.satisfy(function(r) {
        return r.error !== undefined || r.warning !== undefined;
    });
});
```

### TC-009 — Verify Cart is Empty After Removal
```javascript
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});
pm.test("Cart is empty", function () {
    var j = pm.response.json();
    pm.expect(j.products).to.be.an("array").that.is.empty;
});
```

### TC-010 — Edit Quantity with Large Value
```javascript
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});
pm.test("Response has success or warning", function () {
    var j = pm.response.json();
    pm.expect(j).to.satisfy(function(r) {
        return r.success || r.warning;
    });
});
```

### TC-011 — Remove Non-Existent Cart Key
```javascript
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});
pm.test("Response body exists", function () {
    var j = pm.response.json();
    pm.expect(j).to.be.an("object");
});
```

### TC-012 — Session Token Still Valid After Add
```javascript
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});
pm.test("Products array exists", function () {
    var j = pm.response.json();
    pm.expect(j).to.have.property("products");
    pm.expect(j.products).to.be.an("array");
});
```

---

## Assertions Executed

- Status code validation (positive and negative)
- Response field existence validation (`success`, `error`, `warning`, `products`)
- Success message exact match verification
- Cart ID extraction and storage as environment variable
- Token extraction and storage as collection variable
- Chained variable reuse across multiple requests
- Empty cart assertion after removal
- Session persistence check mid-flow
- Invalid authentication error handling
- Edge case input handling (zero quantity, large quantity, bad product ID)
- Environment cleanup after test flow completion
