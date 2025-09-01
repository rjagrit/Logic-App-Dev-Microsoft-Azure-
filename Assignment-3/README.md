# Assignment-3 Azure Logic App – Blob Trigger with Unzip to Another Folder

This project demonstrates how to create an **Azure Standard Logic App** workflow that:
- Triggers when a **ZIP file** is uploaded to an Azure Blob Storage container.
- **Unzips** the contents of the uploaded file.
- Saves the extracted files into another container/folder.

---

## 🚀 Workflow Overview

1. **Trigger:** When a ZIP file is uploaded in `/input` container.
2. **Get Blob Content:** Download the uploaded ZIP file into the Logic App runtime.
3. **Extract Archive:** Unzip the file contents to a temporary folder.
4. **Loop Through Files:** Iterate through each extracted file.
5. **Create Blob:** Upload the extracted files to `/output` container.

---

## 🛠️ Step-by-Step Implementation

### 🔹 Step 1: Create the Logic App (Standard)
1. Open **Azure Portal** → `Create a resource`.
2. Search for **Logic App (Standard)** → Click **Create**.
3. Fill in details:
   - **Resource Group:** e.g., `LogicAppRG`
   - **Logic App name:** `BlobUnzipWorkflow`
   - **Region:** Select nearest region
   - **Plan type:** `Standard`
4. Click **Review + Create** → then **Create**.

---

### 🔹 Step 2: Add a Blob Trigger
1. Open the Logic App Designer.
2. Choose **Blank Workflow**.
3. Select **Azure Blob Storage** connector →  
   `When a blob is added or modified (properties only) (V2)`.
4. Configure:
   - **Storage Account connection:** Create or select existing.
   - **Container:** `input`
   - **Blob path:** leave blank (all files).
5. This will trigger every time a file is uploaded into `/input`.

---

### 🔹 Step 3: Get Blob Content
1. Add a new step → **Azure Blob Storage** → `Get blob content (V2)`.
2. In **Blob Path**, select **dynamic content → Path** from the trigger.  
   This ensures the Logic App fetches the uploaded ZIP file.

---

### 🔹 Step 4: Extract Archive
1. Add action → **Data Operations** → `Extract archive to folder`.
2. Configure:
   - **Archive file content:** Select **File Content** from previous step.
   - **Destination folder path:** Provide a temporary folder, e.g., `/unzipped/`.
3. This action extracts the ZIP file into multiple files stored temporarily inside the Logic App runtime.

---

### 🔹 Step 5: For Each File in Extracted Archive
1. Add **Control → For each**.
2. Select **dynamic content → Output of Extract archive**.
3. Inside the loop:
   - Add action → **Azure Blob Storage** → `Create blob (V2)`.
   - Configure:
     - **Container:** `output`
     - **Blob path:** `@items('For_each')?['Name']`
     - **Blob content:** `@items('For_each')?['FileContent']`

This uploads each extracted file into the `/output` container.

---

### 🔹 Step 6: (Optional Enhancements)
- **Archive original ZIP:** After extraction, move the original ZIP to an `/archive` folder.
- **Send notification:** Add an Outlook/Gmail action to send an email when files are processed.
- **File type validation:** Add a condition to check file extensions before extraction.
