# Logic App-10: Employee Data Processing

This **Logic App** processes an array of employees sent via HTTP POST and performs multiple operations:

- Creates a **CSV table** of employees
- Creates a **HTML table** of employees
- Filters employees in the **IT department**
- Selects employee names and joins them as a comma-separated string
- Selects employee names and emails for structured output

---

## 🚀 Features

- Accepts multiple employee records in a single request.
- Outputs multiple formats (CSV, HTML) for reporting.
- Filters and selects employee data dynamically.
- Fully automated using **Azure Logic Apps (Consumption)**.

---

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
        "employees": {
          "type": "array",
          "items": {
            "type": "object",
            "properties": {
              "name": { "type": "string" },
              "email": { "type": "string" },
              "dept": { "type": "string" }
            },
            "required": ["name", "email", "dept"]
          }
        }
      }
    }
    ```
<img width="600" height="890" alt="image" src="https://github.com/user-attachments/assets/2b2d632e-d40b-443c-bbc7-55e844de9560" />
<img width="600" height="490" alt="image" src="https://github.com/user-attachments/assets/ebaa4f73-8241-4b59-a3dd-54b2e8e8f5e5" />
<img width="600" height="137" alt="image" src="https://github.com/user-attachments/assets/df605f46-3930-463b-8d02-7a2e04dbfb55" />



---

### 4. Create CSV Table

- Add **Data Operations → Create CSV table**.
- Configure:
  - **From:** `@triggerBody()?['employees']`
  - **Format:** CSV

---
<img width="600" height="656" alt="image" src="https://github.com/user-attachments/assets/88921a59-df75-4b4d-bb8f-af0e17537a0c" />

### 5. Create HTML Table

- Add **Data Operations → Create HTML table** **after CSV table**.
- Configure:
  - **From:** `@triggerBody()?['employees']`
  - **Format:** HTML
  - **Columns:** Custom  
    | Header | Value |
    |-----------------|---------------------------|
    | Employee Name | `@item()?['name']` |
    | Email Address | `@item()?['email']` |
    | Department | `@item()?['dept']` |

---
<img width="600" height="909" alt="image" src="https://github.com/user-attachments/assets/b72706c0-b4e0-4295-8e75-49d13a9fdd37" />

### 6. Filter Array (IT Department)

- Add **Data Operations → Filter array** **after HTML table**.
- Configure:
  - **From:** `@triggerBody()?['employees']`
  - **Condition:**
    ```expression
    @equals(item()?['dept'], '"IT"')
    ```

---

### 7. Select Names

- Add **Data Operations → Select** **after Filter array**.
- Configure:
  - **From:** `@triggerBody()?['employees']`
  - **Map:**
    - Name → `@item()?['name']`

---
<img width="600" height="487" alt="image" src="https://github.com/user-attachments/assets/701ba202-c1f2-4aef-b033-702383e9bcab" />

### 8. Join Names

- Add **Data Operations → Join** **after Select**.
- Configure:
  - **From:** `@body('Select')`
  - **Join With:** `,`
<img width="600" height="458" alt="image" src="https://github.com/user-attachments/assets/dc266a05-6e32-43e2-a74a-3d5dbe850c2d" />

---

### 9. Select Employee Names & Emails

- Add **Data Operations → Select** **after Join**.
- Configure:
  - **From:** `@triggerBody()?['employees']`
  - **Map:**
    - Employee-Name → `@item()?['name']`
    - empMail → `@item()?['email']`
<img width="600" height="596" alt="image" src="https://github.com/user-attachments/assets/b8fbe320-e0e8-4084-a0fc-300f3d332bf1" />

---

### 10. Send Response

- Add **Response (HTTP)** **after the last Select**.
- Configure:
  - **Status Code:** 200
  - **Body:**
    ```json
    {
      "CSV Table": "@outputs('Create_CSV_table')",
      "HTML-table": "@outputs('Create_HTML_table')",
      "Filtered Array": "@outputs('Filter_array')",
      "Joined Names": "@outputs('Join')",
      "Selected Array": "@outputs('Select_1')"
    }
    ```
<img width="600" height="397" alt="image" src="https://github.com/user-attachments/assets/65b3ad51-c4ee-48d1-b3a1-9daa3be45570" />
<img width="600" height="787" alt="image" src="https://github.com/user-attachments/assets/64539cf1-7abf-4152-924f-e486c1641755" />


---

### 11. Save & Test

- Click **Save**.
- Copy the HTTP POST URL generated by the trigger.
- Send a POST request with JSON like:

```json
{
  "employees": [
    { "name": "Jagrit", "email": "jagrit@example.com", "dept": "IT" },
    { "name": "Alice", "email": "alice@example.com", "dept": "HR" },
    { "name": "Bob", "email": "bob@example.com", "dept": "IT" }
  ]
}
```

### The Output
<img width="1090" height="263" alt="image" src="https://github.com/user-attachments/assets/5d7add04-136a-45af-ab9b-3991db02f294" />
<img width="1090" height="430" alt="image" src="https://github.com/user-attachments/assets/d93d64ab-a23a-4540-8842-48e55de68ef6" />
<img width="1090" height="218" alt="image" src="https://github.com/user-attachments/assets/4e7997b1-8e54-4212-b788-c2fa8ddfc284" />

## The Workflow
<img width="600" height="625" alt="image" src="https://github.com/user-attachments/assets/35f297de-9a46-4a7f-9384-937e4ed2f944" />
<img width="630" height="592" alt="image" src="https://github.com/user-attachments/assets/84baa433-f2d5-4002-bb5f-c6bb27fdd581" />




