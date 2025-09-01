# Assignment-6: Azure Logic App - HTTP to CSV in Blob Storage

This project contains an **Azure Standard Logic App** workflow that accepts JSON data via an **HTTP POST request**, converts the data into a **CSV file**, and stores it in **Azure Blob Storage**.

---

## 📌 Workflow Overview
## First, Create the App(Standard)
<img width="1920" height="1080" alt="1" src="https://github.com/user-attachments/assets/65aca866-95c3-4387-95d7-b31045d91c33" />
<img width="1920" height="1080" alt="2" src="https://github.com/user-attachments/assets/b64833ef-5040-4769-9dfa-fa6f1e53c012" />
<img width="1920" height="1080" alt="3" src="https://github.com/user-attachments/assets/436be279-b86b-4382-8cb3-9e5a12645ff9" />


1. **Trigger:**
   - The workflow starts when an **HTTP POST request** is received.
   - The request body must contain an **array of objects** with the fields:
     - `id` (integer)
     - `name` (string)
     - `role` (string)
<img width="1920" height="1080" alt="5" src="https://github.com/user-attachments/assets/b5c834c3-39f0-4f33-b392-009c9a348b96" />
<img width="1920" height="1080" alt="6" src="https://github.com/user-attachments/assets/d8ca7e8a-cb8b-47a1-8e69-db529edcfe9f" />
<img width="1920" height="1080" alt="7" src="https://github.com/user-attachments/assets/faa6bfe7-a5f6-4840-be73-8741d32f5abb" />
<img width="1920" height="1080" alt="4" src="https://github.com/user-attachments/assets/70843155-5787-4ea6-83b4-9b28da2231ec" />

2. **Create CSV Table:**
   - The incoming JSON data is transformed into a **CSV table**.
   - The CSV file has the following columns:
     - **Col-1** → `id`
     - **Col-2** → `name`
     - **Col-3** → `role`
<img width="1920" height="1080" alt="8" src="https://github.com/user-attachments/assets/e4525085-c3a5-40fe-8b12-adeec5f34a34" />
<img width="1920" height="1080" alt="9" src="https://github.com/user-attachments/assets/bf8ed42b-dc84-4fba-aa63-813e092d3df5" />

## - Create a Container inside Storage Account
<img width="1920" height="1080" alt="11" src="https://github.com/user-attachments/assets/acb22cee-f16e-4017-8f21-7efd58c6a4ac" />

3. **Store CSV in Blob Storage:**
   - The generated CSV is uploaded to an **Azure Blob Storage container** inside the folder `/output-files`.
   - The output file is named **`output.csv`**.
<img width="1920" height="1080" alt="14" src="https://github.com/user-attachments/assets/f7314bab-cb06-40df-864e-db6667a37599" />
<img width="1920" height="1080" alt="15" src="https://github.com/user-attachments/assets/f8723d5b-25eb-4e8f-bb75-1462988be5a9" />
<img width="1920" height="1080" alt="16" src="https://github.com/user-attachments/assets/4ecd02c5-1612-4943-a050-91ad00bfbf27" />
<img width="1920" height="1080" alt="17" src="https://github.com/user-attachments/assets/fae8c4d1-28fb-40b8-aef6-ca1304be703d" />

---

## 🛠️ Steps to Deploy
- Put Down raw data in POSTMAN
<img width="1920" height="1080" alt="19" src="https://github.com/user-attachments/assets/984b7ae0-d964-4a9b-b9ee-37eba94b008a" />
<img width="1920" height="1080" alt="20" src="https://github.com/user-attachments/assets/8f07c48e-a467-407a-97a6-9a664dd5d767" />

- File Created in the container
<img width="1920" height="1080" alt="21" src="https://github.com/user-attachments/assets/df52e449-921a-4e09-955f-c26f40526262" />

- File Downloaded
<img width="1920" height="1080" alt="23" src="https://github.com/user-attachments/assets/3ee51e98-5dd8-4c64-8e57-ad21daafe681" />

- Open the file in Notepad
<img width="1422" height="734" alt="24" src="https://github.com/user-attachments/assets/554b67a0-2515-41e6-a3ab-9bbe523cf7da" />

