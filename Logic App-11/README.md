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
<img width="600" height="773" alt="image" src="https://github.com/user-attachments/assets/10863742-5449-409f-9053-4dc5b73312c1" />

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
<img width="600" height="867" alt="image" src="https://github.com/user-attachments/assets/98a5375a-f331-4ad1-b7ce-ceeb896a220c" />

  2. **RunCount** (Integer) → `0`
<img width="600" height="431" alt="image" src="https://github.com/user-attachments/assets/71426c9b-f21d-4951-b841-74c292486502" />

---

### 5. Create CSV Table

- Add **Data Operations → Create CSV table**
- Configure:
  - **From:** `@variables('ProductsArray')`
  - **Format:** CSV
<img width="600" height="553" alt="image" src="https://github.com/user-attachments/assets/3267f890-f4b3-4fad-99d1-ad2da7fad6d9" />


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
<img width="600" height="855" alt="image" src="https://github.com/user-attachments/assets/e92daa95-2e70-4ae3-9428-c3ed898dfad7" />

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
<img width="600" height="848" alt="image" src="https://github.com/user-attachments/assets/0b2b3fa1-dbeb-459b-8e96-52f81c2abc8f" />

**b) Increment Variable**

- Add **Variables → Increment Variable** after Send Email
- Configure:
  - **Name:** `RunCount`
  - **Value:** 1
<img width="600" height="471" alt="image" src="https://github.com/user-attachments/assets/c541d0c9-6d2a-429f-9fd6-43e0f920a52c" />

**c) Delay**

- Add **Control → Delay** after Increment Variable
- Configure:
  - **Interval:** 1 Minute
<img width="600" height="468" alt="image" src="https://github.com/user-attachments/assets/3cbdb0fd-849b-40ba-be76-3c87c4825a85" />

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
### The Output
<img width="800" height="114" alt="image" src="https://github.com/user-attachments/assets/297c7a10-0783-490a-b4e8-728ba2d5e949" />
<img width="800" height="294" alt="image" src="https://github.com/user-attachments/assets/b8d7cede-68fa-46a4-8a86-f5321a6f3daa" />
<img width="800" height="296" alt="image" src="https://github.com/user-attachments/assets/3cf0b526-a9d4-4383-a1de-04495814316f" />

---

## The Workflow
<img width="700" height="1014" alt="image" src="https://github.com/user-attachments/assets/dd18c706-d80a-4c73-a363-ab7d5aab6f6f" />


