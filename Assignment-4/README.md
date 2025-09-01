# Assignment-4: Azure Logic App - Recurrence Trigger Workflow

## 📌 Overview
This project demonstrates how to create an **Azure Logic App (Standard)** with a **Recurrence Trigger**.  
The workflow is scheduled to run **every Monday and Friday, every hour at exactly 00 minutes**, starting from `2025-08-28T00:00:00` in the **AUS Eastern Standard Time** zone.  

You can extend the workflow by adding actions such as:
- Moving/processing files in **Azure Blob Storage**
- Sending notifications via **Outlook/Teams**
- Invoking **HTTP APIs**
- Running **SQL stored procedures**

---

## ⚙️ Steps to Implement

### 1. Create Logic App (Consumption)
1. Go to **Azure Portal** → Click **Create a resource**.
2. Search for **Logic App (Standard)**.
3. Fill in the required details:
   - **Resource Group** → e.g., `logicapp-rg`
   - **Logic App Name** → e.g., `WeeklyJobLogicApp`
   - **Region** → choose your preferred region
4. Click **Review + Create** → **Create**.
<img width="1920" height="1080" alt="1" src="https://github.com/user-attachments/assets/42887e94-3943-40af-a17a-9a629ed5ccd9" />

---

### 2. Add Recurrence Trigger
1. Open the created Logic App → **Workflow Designer**.
2. Add a **Recurrence Trigger**.
3. Configure with:
   - **Interval**: `1`
   - **Frequency**: `Week`
   - **Start Time**: `2025-08-28T00:00:00`
   - **Time Zone**: `AUS Eastern Standard Time`
   - **Schedule**:
     - **WeekDays** → `Monday`, `Friday`
     - **Hours** → `0 – 23`
     - **Minutes** → `0`

This means → Workflow runs **every Monday and Friday at every hour**, but only at **00 minutes**.  
(e.g., 01:00, 02:00, … up to 23:00)
<img width="1920" height="1080" alt="2" src="https://github.com/user-attachments/assets/dbe0aa6e-6ae5-4c72-b2b8-c15b599de146" />

## Create the parameter timeConfig
```json
"recurrence": {
  "interval": 1,
  "frequency": "Week",
  "timeZone": "AUS Eastern Standard Time",
  "startTime": "2025-08-28T00:00:00",
  "schedule": {
    "weekDays": ["Monday", "Friday"],
    "hours": [0,1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20,21,22,23],
    "minutes": [0]
  }
}
```
---
### - Open the code view 
- Edit the **recurrence**
<img width="1920" height="1080" alt="6" src="https://github.com/user-attachments/assets/89ef1313-6685-44d5-8c61-ff4e956ab2ec" />

- Paste the parameter **timeConfig** inside recurrence
<img width="1920" height="1080" alt="7" src="https://github.com/user-attachments/assets/10bd7319-736d-4fcc-9523-ce9dfdde26d9" />


### 3. Save & Test
1. Click **Save** in the Logic App Designer.
2. Manually run it once via **Run Trigger → Recurrence**.
3. Check **Runs History** to confirm execution.


