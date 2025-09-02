## Logic App-2

**What it does:**  
Address validation using an HTTP trigger (if condition)

### 🔹 Steps:
1. Create the Workflow named if-condition demo (stateful)
<img width="915" height="613" alt="image" src="https://github.com/user-attachments/assets/89abdadc-a30a-4604-a855-1f36bb7c8d52" />

2. Select the Trigger as When an HTTP request is received. 
- Click on Use sample payload to generate schema, to add the JSON data
<img width="915" height="585" alt="image" src="https://github.com/user-attachments/assets/6b00194a-a0ff-43c2-9d18-496a3478ffc4" />

The JSON File
<img width="915" height="260" alt="image" src="https://github.com/user-attachments/assets/c39061b5-fb53-4f4b-a720-aefff588fcda" />
<img width="916" height="428" alt="image" src="https://github.com/user-attachments/assets/dbfdccd7-d615-4f66-a582-a4a749673951" />

3. Choose an action, so here we have to validate the data, so we choose **Compose**
- Need to insert the dynamic content(The JSON content) in the Input.
<img width="889" height="400" alt="image" src="https://github.com/user-attachments/assets/186fb384-6628-4a10-a5d6-8e9318659aff" />

4. Next action we choose is type Condition
<img width="915" height="524" alt="image" src="https://github.com/user-attachments/assets/de111ca6-70ed-4535-b05a-7b5239d4b89d" />

- The condition we validate is **If the address is United States**
<img width="915" height="314" alt="image" src="https://github.com/user-attachments/assets/8d5d7a9a-870c-4ed4-8aaf-0abd8818f73f" />

5. The Response for each Block
## a) The True Block Logic
- Using the concat function by choosing the Expression option
<img width="915" height="668" alt="image" src="https://github.com/user-attachments/assets/bf419c10-26ed-4941-b392-b3fdfde577cc" />

## b) The False Block Logic
<img width="915" height="718" alt="image" src="https://github.com/user-attachments/assets/fdfbab6f-76e3-4b0f-83fa-9a3b81ed4d15" />

### ✅ The Output

<img width="920" height="557" alt="image" src="https://github.com/user-attachments/assets/d0807a16-b277-4fc8-bc7f-5f10c9c166ab" />  
<img width="920" height="573" alt="image" src="https://github.com/user-attachments/assets/4499305c-1bf0-411f-8d15-37a26dfcb0d9" />

---
### 🖼 Workflow Design

<img width="915" height="644" alt="image" src="https://github.com/user-attachments/assets/ae671cd5-fda3-4e52-85c6-24c8548be75b" />
