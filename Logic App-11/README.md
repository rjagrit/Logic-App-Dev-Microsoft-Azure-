# Logic App-10: Products CSV Email Automation

This **Logic App** generates a CSV table of products and sends it via email repeatedly until a specified run count is reached.

---

## 🚀 Features

- Initializes a product array and run counter
- Generates a CSV table of products
- Sends the CSV via **Gmail** email
- Loops with a delay until run count reaches the limit
- Configurable loop iterations and delay

---

## 🛠 Steps to Create

### 1. Create the Logic App

- Go to **Azure Portal** → **Create a Resource** → Search **Logic App (Consumption)**
- Select your **Resource Group**, provide a **Logic App Name**, choose a **Region**, and click **Create**

---

### 2. Open Logic App Designer

- Open your Logic App → **Logic App Designer**
- Select **Blank Logic App**

---

### 3. Add Trigger: When a HTTP Request is Received

- Search for **HTTP** → select **When a HTTP request is received**
- Configure:
  - **Method:** POST

---

### 4. Initialize Variables

- Add **Variables → Initialize variable** action
- Configure two variables:
  1. **ProductsArray** (Array)
     ```json
     [
       { "Description": "Apples", "Product_id": 1 },
       { "Description": "Oranges", "Product_id": 2 }
     ]
     ```
  2. **RunCount** (Integer) → `0`

---

### 5. Create CSV Table

- Add **Data Operations → Create CSV table**
- Configure:
  - **From:** `@variables('ProductsArray')`
  - **Format:** CSV

---

### 6. Add Until Loop

- Add **Control → Until** action
- Configure:
  - **Condition:**
    ```expression
    @greaterOrEquals(variables('RunCount'),2)
    ```
    Loops until `RunCount >= 2`
  - **Limit:** Max 60 iterations, Timeout: 1 hour

---

### 7. Add Actions Inside Until Loop

**a) Send Email (V2)**

- Add **Gmail → Send Email (V2)** inside the loop
- Configure:
  - **To:** `derik7208@gmail.com`
  - **Subject:** `Run Count-@{variables('RunCount')}`
  - **Body:**
    ```html
    <p>@{body('Create_CSV_table')}</p>
    ```
- Uses Gmail connection provided in `$connections`

**b) Increment Variable**

- Add **Variables → Increment Variable** after Send Email
- Configure:
  - **Name:** `RunCount`
  - **Value:** 1

**c) Delay**

- Add **Control → Delay** after Increment Variable
- Configure:
  - **Interval:** 1 Minute

---

### 8. Save & Test

- Click **Save**
- Send a HTTP POST request to trigger the workflow
- The Logic App will:
  1. Generate a CSV of products
  2. Send it via email
  3. Increment `RunCount`
  4. Wait 1 minute and repeat until `RunCount >= 2`

---

## 📈 Flow Diagram
