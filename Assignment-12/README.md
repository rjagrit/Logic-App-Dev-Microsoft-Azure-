# Assignment-12: JSON Data Validation Logic App

This repository contains an **Azure Standard Logic App** workflow that validates incoming JSON payloads for required fields.  
The Logic App ensures all required fields are present and contain at least one character. If validation passes, a `200 OK` response is returned. Otherwise, a `400 Bad Request` response with details of the missing/invalid fields is returned.

---

## 🚀 Workflow Overview

### Trigger
- **When an HTTP request is received**  
  - Accepts a `POST` request with a JSON payload.
  - The schema enforces structure for the required fields.

### Actions
1. **Initialize Variables**
   - `validationErrors` → Stores validation error details.
   - `requiredFields` → List of required fields:
     - `firstName`
     - `lastName`
     - `email`
     - `phoneNumber`
     - `address`
     - `city`
     - `state`
     - `postalCode`
     - `country`
     - `gender`

2. **For each field (Loop)**
   - Checks if the field is missing or empty.
   - If invalid, appends an error message to `validationErrors`.

3. **Condition (Validation Check)**
   - If `validationErrors` is empty → Respond with **200 OK** and message `"Validation Passed"`.
   - Else → Respond with **400 Bad Request** including details of the failed fields.

---

## 📌 JSON Schema (Expected Request Body)

```json
{
  "firstName": "John",
  "lastName": "Doe",
  "email": "john.doe@example.com",
  "phoneNumber": "1234567890",
  "address": "123 Street Name",
  "city": "Sample City",
  "state": "Sample State",
  "postalCode": "12345",
  "country": "Sample Country",
  "gender": "Male"
}
