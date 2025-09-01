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

## - To work on blob storage, copy the three fields:
- Storage account Name
- Key (that you get in **Security + networking -> Access Keys**
- Connection string
<img width="1920" height="861" alt="10" src="https://github.com/user-attachments/assets/21ad3135-4dce-4133-8ba9-6d5ef0f1a2cf" />

### 5. Add Action: Create Blob (V2)
- Add Azure Blob Storage → Create blob (V2) action
<img width="1920" height="858" alt="12" src="https://github.com/user-attachments/assets/9f21f2cc-7380-48cb-8f2d-f0784a79977f" />

- Choose the authentication type based on your choice. Here, we choose **Access key** means we authenticate using **Access key**. 
<img width="1920" height="858" alt="12" src="https://github.com/user-attachments/assets/9c34f0d1-0479-4f3c-b28c-e9ca23a3c34a" />

- Fill the required fields like Storage account name, the key that we mentioned above.
<img width="1920" height="871" alt="13" src="https://github.com/user-attachments/assets/06f2e148-2d44-4101-bf44-8690e4aa5cc4" />

- Now again fill details like storage account name, folder path(file location), blob name, blob content, content type(if needed) 
<img width="1920" height="858" alt="14" src="https://github.com/user-attachments/assets/f1dc944e-54c0-4163-a2c4-5d28cffd16c5" />
<img width="1920" height="867" alt="15" src="https://github.com/user-attachments/assets/ab58af41-dcbf-4563-a691-f8e807cfa23d" />
<img width="1920" height="863" alt="16" src="https://github.com/user-attachments/assets/4caff9cb-3477-44de-b7fa-f585c733d9a6" />
<img width="1920" height="864" alt="17" src="https://github.com/user-attachments/assets/f6cb9a34-9cf9-4c09-9720-4f9d1fcec514" />

## The Output
- Save the Workflow and just copy the link generated, paste it along with the Raw Data as JSON 
<img width="1920" height="1019" alt="19" src="https://github.com/user-attachments/assets/ddfde34f-812c-41ea-9178-ad7c0948e9d9" />
<img width="1920" height="1024" alt="20" src="https://github.com/user-attachments/assets/fe79891b-1bd1-499a-b75f-ca10640c9de0" />

- Here you see the pracBlob that we gave a name to our blob, open it, and download it to see the data inside. 
<img width="1920" height="868" alt="21" src="https://github.com/user-attachments/assets/f7a2866f-5cbe-4b5a-bb3c-be4db81ddc8f" />

- Downloaded CSV file9pracBlob)
- open it in Notepad to evaluate, though
<img width="1920" height="1024" alt="23" src="https://github.com/user-attachments/assets/27c83d42-bb47-47f5-9c87-1cc8fb0f87e9" />

### The Workflow
<img width="1920" height="861" alt="18" src="https://github.com/user-attachments/assets/80b7117d-5267-4da4-856e-edc47a3a448d" />














