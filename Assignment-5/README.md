# Assignment-5: JSON to XML Converter & Blob Storage Saver

This **Azure Logic App (Standard)** workflow receives a **JSON payload** via HTTP POST, converts it into **XML**, and then stores the file in an **Azure Blob Storage** container.

---

## 📌 Workflow Summary
1. **Trigger** – HTTP POST request with JSON body.  
2. **Compose** – Converts JSON payload into XML.  
3. **Create Blob (V2)** – Uploads the generated XML into a Blob container.  

---

## ⚙️ Detailed Workflow Steps
### 1. Create the Logic App (Standard)
<img width="1920" height="1080" alt="Screenshot (2149)" src="https://github.com/user-attachments/assets/a238064c-aaa5-4001-a394-c8c40be17e31" />

### 2. Create the Workflow
<img width="1920" height="1080" alt="Screenshot (2152)" src="https://github.com/user-attachments/assets/9c02c897-0cc9-4a71-8edb-73a399db1d20" />


### 2. HTTP Request Trigger
- **Trigger Type**: `When a HTTP request is received`
- **Method**: `POST`
- **JSON Schema**:
  ```json
  {
    "type": "object",
    "properties": {
      "id": { "type": "string" },
      "name": { "type": "string" },
      "age": { "type": "integer" }
    }
  }

<img width="1920" height="1080" alt="Screenshot (2153)" src="https://github.com/user-attachments/assets/011784a7-a538-4438-88fc-9c9915be4a29" />

### 2. Convert JSON to XML
- Action: Compose
<img width="1920" height="1080" alt="Screenshot (2154)" src="https://github.com/user-attachments/assets/4ef59b61-ac97-4410-bf66-17e13ae30433" />

## - The Storaga Account
<img width="1920" height="1080" alt="Screenshot (2155)" src="https://github.com/user-attachments/assets/0eb6e777-4ddc-4cf1-ab18-84504b0c1e52" />

- Create the Container
<img width="1920" height="1080" alt="Screenshot (2155)" src="https://github.com/user-attachments/assets/54216ab7-9632-4692-add9-08028a2c167b" />
<img width="1920" height="1080" alt="Screenshot (2157)" src="https://github.com/user-attachments/assets/c383691d-0a31-4f80-86a1-f21685f0a1ac" />

### 3. Save XML to Blob
- Action: Create blob (V2)
<img width="1920" height="1080" alt="Screenshot (2158)" src="https://github.com/user-attachments/assets/47f99dd7-a831-45d8-b266-b54d184b463f" />

- Connection: azureblob
<img width="1920" height="1080" alt="Screenshot (2159)" src="https://github.com/user-attachments/assets/be8022a1-69da-4487-a3a5-0e468d9362ad" />
<img width="1920" height="1080" alt="Screenshot (2160)" src="https://github.com/user-attachments/assets/e05ae193-0706-47b1-bf1e-376ca97f67a4" />

- Folder Path: /xml-files
- Blob Name: jsonfile.xml
- Blob Content: Output from Compose (XML data)
- The XML file is stored in the specified container in your Storage Account.
<img width="1920" height="1080" alt="Screenshot (2161)" src="https://github.com/user-attachments/assets/a5cad0c7-857d-45e9-9a03-4e10067c29d0" />
<img width="1920" height="1080" alt="Screenshot (2162)" src="https://github.com/user-attachments/assets/33d47eb5-0573-4a96-ae0a-13e872d67027" />


## The Output 
- Provide the Raw Data
<img width="1920" height="1080" alt="Screenshot (2165)" src="https://github.com/user-attachments/assets/bfd529a9-a491-499d-b5ec-00d8a4ac8a32" />

- File Created in Container
<img width="1920" height="1080" alt="Screenshot (2166)" src="https://github.com/user-attachments/assets/72501e40-16b0-481f-bead-a6125472d7f9" />

- Downloaded file
<img width="1920" height="1080" alt="Screenshot (2168)" src="https://github.com/user-attachments/assets/e23b0f59-1a3a-4465-b88f-b1f4e5c859e3" />

- Open in Notepad
<img width="1439" height="730" alt="Screenshot (2169)" src="https://github.com/user-attachments/assets/f85a8b53-45b6-4dd9-9a5d-a24794bd0513" />







