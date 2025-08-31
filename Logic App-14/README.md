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
<img width="700" height="435" alt="image" src="https://github.com/user-attachments/assets/8f909533-3bc7-4954-8248-3a3fa56edce0" />

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
### 4. Add Action: Execute JavaScript Code
- Add Inline Code → JavaScript action
- Configure Inputs → Code:

```
var inputNumber = workflowContext.trigger.outputs.body.number;

// Check if undefined or null
if (inputNumber === undefined || inputNumber === null) {
    return { "message": "Input number is undefined. Please provide a number." };
}

// Check if input is not a number
if (typeof inputNumber !== "number" || isNaN(inputNumber)) {
    return { "message": "Invalid input. Please provide a valid number." };
}

// Check Odd or Even
if (inputNumber % 2 === 0) {
    return { "message": inputNumber + " is Even" };
} else {
    return { "message": inputNumber + " is Odd" };
}

```
<img width="700" height="840" alt="image" src="https://github.com/user-attachments/assets/321d59b7-c865-4b06-b39b-09a2a6cbae8e" />

### 5. Add Action: Response
- Add Response → HTTP Response action
- Configure:
  - Status Code: 200
      Body: @outputs('Execute_JavaScript_code')
  - Run after Execute_JavaScript_code succeeds
 <img width="800" height="565" alt="image" src="https://github.com/user-attachments/assets/fc7ed422-b99d-40f0-8cd5-c1c576683d6f" />

 ### The Workflow
 <img width="400" height="651" alt="image" src="https://github.com/user-attachments/assets/75e30401-3141-49da-9b71-ee07ffa7bc63" />


