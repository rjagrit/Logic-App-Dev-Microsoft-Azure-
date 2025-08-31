# Logic App-14: Odd/Even Number Checker

This **Logic App** receives a number via HTTP POST request, validates the input, and returns whether the number is **odd** or **even** using inline JavaScript.

---

## 🚀 Features

- Triggered via **HTTP POST request**
- Validates input for:
  - Missing number
  - Invalid number (non-integer)
- Returns result: Odd or Even
- Returns appropriate error messages for invalid input

---

## 🛠 Steps to Create

### 1. Create the Logic App

- Go to **Azure Portal → Create a Resource → Logic App (Consumption)**
- Select your **Resource Group**, provide a **Logic App Name**, choose a **Region**, and click **Create**

---

### 2. Open Logic App Designer

- Open the deployed Logic App → **Logic App Designer**
- Select **Blank Logic App**

---

### 3. Add Trigger: When a HTTP Request is Received

- Search **HTTP** → select **When a HTTP request is received**
- Configure:
  - **Method:** POST
  - **Request Body JSON Schema:**

```json
{
  "type": "object",
  "properties": {
    "number": {
      "type": ["integer", "null"]
    }
  }
}
```
