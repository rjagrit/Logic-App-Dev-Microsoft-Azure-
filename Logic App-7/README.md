# Logic App-7: Multi-User Admin Check

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

### 2. Open Logic App Designer

- Open your Logic App → **Logic App Designer**.
- Select **Blank Logic App**.

---

### 3. Add Trigger: When a HTTP Request is Received

- Search for **HTTP** → select **When a HTTP request is received**.
- Configure:
  - **Method**: POST
  - **Request Body JSON Schema**:
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

### 4. Initialize Variables

- Add action → **Variables** → **Initialize variable**.
- Initialize two variables:
  1. **Name**: `adminUsers` | **Type**: Array | **Value**: `[]`
  2. **Name**: `messages` | **Type**: Array | **Value**: `[]`
<img width="600" height="878" alt="image" src="https://github.com/user-attachments/assets/80110bfc-073d-402a-b520-d13f290e42f7" />
<img width="600" height="470" alt="image" src="https://github.com/user-attachments/assets/6d0e2470-f3de-49b8-a562-e5641fbd77cd" />


### 5. Add Scope: Process Users Scope

- Add **Control** → **Scope** → name it `Process_Users_Scope`.

### 6. Add For Each Loop

- Inside the Scope, add **Control** → **For each**.
- Configure:
  - **Select an output from previous steps**: `@triggerBody()?['users']`
<img width="600" height="364" alt="image" src="https://github.com/user-attachments/assets/509b3b39-c7c7-4e8e-8998-d11079e1d96c" />

### 7. Add Condition Inside For Each

- Inside the For Each, add **Control** → **Condition**.
- Configure the condition expression:
  ```expression
  @equals(item()?['group'], 'Admin')
  ```
<img width="600" height="501" alt="image" src="https://github.com/user-attachments/assets/d7d6b97a-89d2-497d-9f47-22b8287473fd" />

### 8. Configure Actions for Condition
- If true (Yes branch):
  - Append to Array Variable → Name: adminUsers, Value: @item()?['user']
<img width="600" height="436" alt="image" src="https://github.com/user-attachments/assets/e6bf0908-3b4e-4b8f-b518-5e1046136216" />

  - Append to Array Variable → Name: messages, Value: @concat(item()?['user'],' is a Admin')
<img width="600" height="387" alt="image" src="https://github.com/user-attachments/assets/23a2c9da-d7eb-41d4-bd21-4471eb6bff6d" />

- If false (No branch):
  - Append to Array Variable → Name: messages, Value: @concat(item()?['user'],' is not a Admin')
<img width="600" height="395" alt="image" src="https://github.com/user-attachments/assets/cf6a7201-7de8-460a-94fc-69ea550ac860" />

### 9. Send Response
- Add Response (HTTP) action after Scope with status code as 200
<img width="698" height="322" alt="image" src="https://github.com/user-attachments/assets/2628b6a4-72f6-4c7d-b76e-8ce33734915a" />

### The Output:
<img width="700" height="621" alt="image" src="https://github.com/user-attachments/assets/a11fe695-7d53-4045-bf9d-6c18185d12f8" />

## The Workflow

<img width="600" height="1001" alt="image" src="https://github.com/user-attachments/assets/9d584df6-d04e-4668-a821-99ce5ee4c93e" />

