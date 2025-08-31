# Logic App-15: Save Email Attachments to Azure Blob Storage

This **Logic App** automatically saves attachments from incoming Outlook emails to Azure Blob Storage.

---

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

---

### 4. Add Action: For Each Attachment

- Add **Control → For Each**
- Select **Attachments** from dynamic content: `@triggerBody()?['Attachments']`

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

---

### 6. Save & Test

- Click **Save**
- Send an email to your configured inbox **with attachments**
- Logic App will automatically:
  1. Trigger on new email
  2. Loop through attachments
  3. Upload each attachment as a blob in `/files` folder in Azure Blob Storage

---

## 📈 Flow Diagram
