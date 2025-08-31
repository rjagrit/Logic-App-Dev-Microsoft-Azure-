# Logic App-15: Save Email Attachments to Azure Blob Storage

What it does: This **Logic App** automatically saves attachments from incoming Outlook emails to Azure Blob Storage.

## 🚀 Features

- Triggered by **new email arrival** in Outlook Inbox
- Only processes emails with **attachments**
- Saves each attachment to **Azure Blob Storage**
- Handles **multiple attachments** per email
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

### 3. Add Trigger: When a New Email Arrives (V2)

- Search **Outlook 365 Connector → When a new email arrives (V2)**
- Configure:
  - **Folder**: `Inbox`
  - **Include Attachments**: `Yes`
  - **Only emails with attachments**: `Yes`
  - **Importance**: Any
- Enable **splitOn** for `@triggerBody()?['value']`
<img width="900" height="713" alt="image" src="https://github.com/user-attachments/assets/9609b46b-7136-4a00-9bdd-993fb75a2221" />

---

### 4. Add Action: For Each Attachment

- Add **Control → For Each**
- Select **Attachments** from dynamic content: `@triggerBody()?['Attachments']`
<img width="900" height="357" alt="image" src="https://github.com/user-attachments/assets/02d852e4-5c5c-443f-b3d8-18f5f1eb87ea" />

---

### 5. Inside For Each: Create Blob (V2)

- Add **Azure Blob Storage → Create blob (V2)** action
- Configure:
  - **Folder Path**: `/files`
  - **Blob Name**: `@items('For_each')?['Name']`
  - **File Content**: `@items('For_each')`
  - **Read File Metadata from Server**: `Yes`
- Use **Chunked transfer mode** to handle large files
- Ensure connection references your **Azure Blob Storage account**
<img width="900" height="668" alt="image" src="https://github.com/user-attachments/assets/4e68c097-591d-4d50-ad9b-b45a2d15ce02" />

---
### The Storage Account
<img width="900" height="312" alt="image" src="https://github.com/user-attachments/assets/515ed511-94a2-4656-914d-11a029e6843a" />

### Results
## 1. Test Email along with attached files
<img width="900" height="551" alt="image" src="https://github.com/user-attachments/assets/84e98014-1a9f-4059-93bb-98c2301a5d09" />

## 2. Email attached files inside the container (the blob)
<img width="900" height="554" alt="image" src="https://github.com/user-attachments/assets/53e91667-b05d-4b3c-847a-fb427a1b3512" />


### 6. Save & Test

- Click **Save**
- Send an email to your configured inbox **with attachments**
- Logic App will automatically:
  1. Trigger on new email
  2. Loop through attachments
  3. Upload each attachment as a blob in `/files` folder in Azure Blob Storage

---

### The Workflow
<img width="504" height="838" alt="image" src="https://github.com/user-attachments/assets/a3f89c25-fb32-4794-8532-417096114d4f" />


