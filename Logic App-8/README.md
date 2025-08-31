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
<img width="700" height="496" alt="image" src="https://github.com/user-attachments/assets/ab7aa282-f75d-4d15-8ecd-319cd086a817" />
<img width="700" height="283" alt="image" src="https://github.com/user-attachments/assets/80b7b932-c8e7-4542-a7db-7add29a8e44d" />

---

### 9. Send Response
<img width="700" height="374" alt="image" src="https://github.com/user-attachments/assets/1c50eee7-9e08-43ec-a139-94b656837f92" />

---

### 10. Save & Test
<img width="700" height="421" alt="image" src="https://github.com/user-attachments/assets/96c93c48-d1d1-4d97-8653-21259ebf511a" />
<img width="700" height="384" alt="image" src="https://github.com/user-attachments/assets/2a7318e5-7a3f-47ca-8083-40837111c319" />

