# Logic App-8: Multi-User Admin Check (variable demonstration)

This **Logic App** receives an array of users via HTTP POST, checks which users belong to the `Admin` group, and returns:

- `adminUsers`: An array of users who are Admins
- `messages`: An array of messages indicating each user's admin status

## 🚀 Features

- Accepts multiple users in a single request.
- Loops through each user to check their group.
- Returns separate arrays for admin users and status messages.
- Fully automated using Azure Logic Apps (Consumption).

## 🛠 Steps to Create

### 1. Create the Logic App

- Go to **Azure Portal** → **Create a Resource** → Search **Logic App (Consumption)**.
- Select your **Resource Group**, provide a **Logic App Name**, choose a **Region**, and click **Create**.

---

### 2. Open Logic App Designer

- Open your Logic App → **Logic App Designer**.
- Select **Blank Logic App**.

---

### 3. Add Trigger: When a HTTP Request is Received

- Search for **HTTP** → select **When a HTTP request is received**.
- Configure:
  - **Method:** POST
  - **Request Body JSON Schema:**
    ```json
    {
      "type": "object",
      "properties": {
        "users": {
          "type": "array",
          "items": {
            "type": "object",
            "properties": {
              "user": { "type": "string" },
              "group": { "type": "string" }
            }
          }
        }
      }
    }
    ```

---

### 4. Initialize Variables

- Add **Variables → Initialize variable**.
- Initialize **two array variables**:
  1. `adminUsers` → `[]`
  2. `messages` → `[]`

---

### 5. Add Scope: Process Users

- Add **Control → Scope** → name it `Process_Users_Scope`.

---

### 6. Add For Each Loop

- Inside the Scope, add **Control → For each**.
- Configure:
  - **Select an output from previous steps:** `@triggerBody()?['users']`

---

### 7. Add Condition Inside For Each

- Inside the For Each loop, add **Control → Condition**.
- Configure the **expression**:
  ```expression
  @equals(item()?['group'], 'Admin')
  ```

---

### 8. Configure Actions for Condition

---

### 9. Send Response

---

### 10. Save & Test
