# Ass-0: Convert Products Array to CSV and Upload to Azure Blob Storage

This Logic App receives a list of products via an HTTP POST request, converts it into a CSV table, and uploads it to **Azure Blob Storage**.

---

## 🚀 Features

- Triggered via **HTTP POST request**  
- Converts JSON array of products into **CSV format**  
- Uploads the CSV as a blob to **Azure Blob Storage**  
- Supports **chunked transfer** for large files  

---

## 🛠 Steps to Create

### 1. Create the Logic App
- Go to **Azure Portal → Create a Resource → Logic App (Consumption)**  
- Select **Resource Group**, provide a **Logic App Name**, choose a **Region**, and click **Create**  

---

### 2. Open Logic App Designer
- Open the deployed Logic App → **Logic App Designer**  
- Select **Blank Logic App**  

---

### 3. Add Trigger: When a HTTP Request is Received
- Search for **Request → When a HTTP request is received**  
- Set **Method**: POST  
- Add **JSON schema** for the products array:
<img width="900" height="820" alt="4" src="https://github.com/user-attachments/assets/2cb3d47c-6e60-4146-a4cf-44510a8925bb" />

```json
{
  "type": "object",
  "properties": {
    "products": {
      "type": "array",
      "items": {
        "type": "object",
        "properties": {
          "productId": { "type": "integer" },
          "productName": { "type": "string" },
          "description": { "type": "string" },
          "price": { "type": "number" },
          "quantity": { "type": "integer" }
        },
        "required": ["productId","productName","description","price","quantity"]
      }
    }
  }
}
```
<img width="900" height="500" alt="2" src="https://github.com/user-attachments/assets/ce60d2bb-7e6b-4545-83e3-f96ee39837a5" />
<img width="900" height="211" alt="3" src="https://github.com/user-attachments/assets/3360b29b-890c-49e8-9a2e-3795581b8f68" />

### 4. Add Action: Create CSV Table
- Add Data Operations → Create CSV Table
- Configure:
  - From: @triggerBody()?['products']
  - Format: CSV
 <img width="900" height="872" alt="5" src="https://github.com/user-attachments/assets/dc115135-2612-4c29-ba60-c719ddfaa25f" />

## The Storage account Details
<img width="900" height="868" alt="6" src="https://github.com/user-attachments/assets/71eda565-1471-4e1f-9de7-62122b99f787" />
<img width="900" height="835" alt="7" src="https://github.com/user-attachments/assets/edda8113-2dda-4a18-83f0-2920243b8e12" />
<img width="900" height="871" alt="8" src="https://github.com/user-attachments/assets/aca7fde9-04d1-4050-87f0-270d69c25319" />
<img width="900" height="868" alt="9" src="https://github.com/user-attachments/assets/4dd297b0-214d-4e0f-bd8f-279b8cf3d59a" />




