# Assignment-11: Azure Logic App - Blob Validation Workflow

This Logic App is designed to validate a file in Azure Blob Storage based on the file path provided through an HTTP request.  
It performs the following checks:

1. **File existence** in Blob Storage  
2. **File content check** (whether empty or has valid data)  
3. Returns appropriate **HTTP status codes** and messages.

---

## 🛠 Workflow Overview

### 1. Trigger
- **When an HTTP request is received**
  - Method: `POST`
  - Expected JSON Schema:
    ```json
    {
      "type": "object",
      "properties": {
        "filePath": {
          "type": "string"
        }
      },
      "required": [
        "filePath"
      ]
    }
    ```
<img width="1920" height="1080" alt="Screenshot (2317)" src="https://github.com/user-attachments/assets/01f86fe3-44f5-4eee-977b-bfd57b144c6a" />

### 2. Actions

#### 🔹 Step 1: Check if Blob Exists
- Action: **Get Blob Metadata using Path (V2)**
- Input: `filePath` from HTTP request
<img width="1920" height="1080" alt="Screenshot (2318)" src="https://github.com/user-attachments/assets/9b779cd0-ff07-4f7a-a3ec-2ca4f6077363" />

- If blob does not exist → return:
  ```json
  {
    "statusCode": 404,
    "body": {
      "error": "File not found"
  ```


### Step 3. Action: Get Blob Content using Path (V2)
- Input: filePath from HTTP request
<img width="1920" height="1080" alt="Screenshot (2319)" src="https://github.com/user-attachments/assets/8f50fd7c-2702-4ac0-9f32-3164a7856234" />

### Step 3: Condition – Check File Content
- If file content length = 0 → return:
<img width="1920" height="1080" alt="Screenshot (2320)" src="https://github.com/user-attachments/assets/2c8d8b46-42c2-4742-a581-664f3a378bed" />
<img width="1920" height="1080" alt="Screenshot (2321)" src="https://github.com/user-attachments/assets/bb7be67e-2bfe-49f2-a068-306c165da531" />
<img width="1920" height="1080" alt="Screenshot (2326)" src="https://github.com/user-attachments/assets/adaab487-ef7b-466a-abe8-a85dc945e108" />
<img width="1920" height="1080" alt="Screenshot (2327)" src="https://github.com/user-attachments/assets/0a0310ab-cdb1-4c77-a7ca-6cca352c05cf" />

- Else → return:
<img width="1920" height="1080" alt="Screenshot (2328)" src="https://github.com/user-attachments/assets/fac2c679-6637-4e06-90bb-ce0d80a9b2c5" />

- The Workflow
<img width="1082" height="676" alt="Screenshot (2329)" src="https://github.com/user-attachments/assets/98e0041a-2591-4080-8283-22460f52d329" />
