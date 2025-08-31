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
<img width="908" height="431" alt="image" src="https://github.com/user-attachments/assets/5f89812e-194f-42b2-a486-3014acd3588e" />

---

### 4. Add Action: Execute JavaScript Code

- Add **Inline Code → JavaScript** action
- Configure **Inputs → Code**:

```javascript
var text = "Hello world from " + workflowContext.workflow.name;
return text;
```
<img width="851" height="429" alt="image" src="https://github.com/user-attachments/assets/1e6c964f-0a62-4843-a43b-64fa4cdf7cbc" />

### 5. Add Action: Response
<img width="900" height="185" alt="image" src="https://github.com/user-attachments/assets/fc3dc88a-a800-4a51-aaec-6e71b4f3e72b" />
<img width="900" height="613" alt="image" src="https://github.com/user-attachments/assets/c4be3373-b896-40f5-9838-a2922fc62ba4" />


### 6. Save & Test
- Click Save
  - Send an HTTP POST request to the trigger URL
    - The Logic App will:
    1. Execute the JavaScript code
    2. Return the result via HTTP response

### The Output
<img width="862" height="424" alt="image" src="https://github.com/user-attachments/assets/b70a49ad-52ec-400d-8210-523f9eb9f3a6" />


