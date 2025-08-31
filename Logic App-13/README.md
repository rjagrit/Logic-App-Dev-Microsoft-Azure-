# Logic App-13: Execute JavaScript and Respond

This **Logic App** executes inline JavaScript code and returns the result as an HTTP response.

---

## 🚀 Features

- Triggered via **HTTP POST request**
- Executes JavaScript code inside the Logic App
- Returns output using **Response** action
- Example output: `"Hello world from <LogicAppName>"`

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
- This allows the Logic App to be triggered via an HTTP POST request

---

### 4. Add Action: Execute JavaScript Code

- Add **Inline Code → JavaScript** action
- Configure **Inputs → Code**:

```javascript
var text = "Hello world from " + workflowContext.workflow.name;
return text;
```
