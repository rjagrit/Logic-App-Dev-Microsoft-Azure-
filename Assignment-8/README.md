# Assignment-8: Email to CSV Converter using Azure Logic Apps

This project demonstrates how to build an **Azure Logic App** that:
1. Listens for incoming emails in **Outlook** with attachments.
2. Validates the presence of an attachment.
3. Parses the attached JSON file.
4. Converts the JSON data into CSV format using inline **JavaScript Code**.
5. Saves the converted file into **Azure Blob Storage**.

---

## 🚀 Workflow Overview

- **Trigger**: When a new email arrives in Outlook with an attachment.  
- **Validation**: Checks if the attachment is present.  
- **Processing**:  
  - Parses JSON attachment.  
  - Converts JSON → CSV.  
- **Storage**: Uploads the converted `.csv` file to Azure Blob Storage inside `/outputfiles/`.

---

## 🛠️ Prerequisites

Before deploying this Logic App, make sure you have:

1. **Azure Subscription**
2. **Logic App (Standard or Consumption)** deployed
3. **Azure Blob Storage** account & container created
   - Example container: `outputfiles`
4. **Outlook Connection** for reading emails
5. Basic knowledge of **JSON schema** and **Azure Portal**

---

## 📂 Logic App Steps

### 1. Trigger: *When a new email arrives (V2)*
- Monitors the **Inbox** folder.
- Ensures only emails with attachments are processed.
<img width="1920" height="1080" alt="Screenshot (2333)" src="https://github.com/user-attachments/assets/efb1695f-1580-4a4e-8863-7258770247fb" />

### 2. Condition: *Check Attachment Presence*
- Verifies that at least one attachment is included.
- If no attachment → stops workflow.
<img width="1920" height="1080" alt="Screenshot (2334)" src="https://github.com/user-attachments/assets/ed94ce49-60a5-40cd-80cb-e8c0124f3093" />

### 3. For Each Attachment
Loops through attachments and performs:
<img width="1920" height="1080" alt="Screenshot (2335)" src="https://github.com/user-attachments/assets/ae58cc59-842e-41fc-bbc8-375b588d82a5" />

#### a. **Parse JSON**
- Decodes Base64 content from the email attachment.
- Validates it against the JSON schema:  
  ```json
  {
    "type": "array",
    "items": {
      "type": "object",
      "properties": {
        "id": { "type": "integer" },
        "name": { "type": "string" },
        "salary": { "type": "integer" }
      },
      "required": ["id", "name", "salary"]
    }
  }
<img width="1920" height="1080" alt="Screenshot (2336)" src="https://github.com/user-attachments/assets/6cd60ec7-20a2-427e-a643-dc1fe747eff5" />

### b. Execute JavaScript Code
<img width="1920" height="1080" alt="Screenshot (2339)" src="https://github.com/user-attachments/assets/e9e4eca8-ad37-4dc5-89e0-466aa790900d" />

### c. Create Blob (V2)
- Uploads the generated converted.csv to Azure Blob Storage.
- Folder path: /outputfiles/
- File name: converted.csv
<img width="1920" height="1080" alt="Screenshot (2338)" src="https://github.com/user-attachments/assets/b565bc58-58d1-4961-a3a5-5a0351124eb3" />

### The Output

## - Send the test email along with an attachment
<img width="1920" height="1080" alt="Screenshot (2347)" src="https://github.com/user-attachments/assets/e89575a4-0bfc-4a2b-9fbc-40a4de7e59b2" />

## - File generated in Container
<img width="1920" height="1080" alt="Screenshot (2343)" src="https://github.com/user-attachments/assets/40ebc937-6ee2-4031-9ba1-c41ddeaf87de" />

## - Download the file
<img width="1920" height="1080" alt="Screenshot (2344)" src="https://github.com/user-attachments/assets/eed21518-1055-43a9-b583-68d4887d8cb2" />

## - Open file in Notepad
<img width="1422" height="719" alt="Screenshot (2345)" src="https://github.com/user-attachments/assets/4e772b74-6266-4ea9-ba8d-1b92542fb875" />

