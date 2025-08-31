# 1) Logic App-1 [ Auto-Reply Email Logic App (Consumption) ]
What it will Do: This Logic App automatically replies to emails when a new email arrives in the inbox with the subject **"testing"**.


## 🚀 Steps to Create

### 1. Create Logic App
- Go to **Azure Portal** → **Create a resource** → Search for **Logic App (Consumption)**.  
- Select your **Resource Group**, give a **Logic App Name**, choose a **Region**, and click **Create**.  
### 2. Open Logic App Designer
- After deployment, open your Logic App.  
- Select **Blank Logic App** in the Designer.  

### 3. Add Trigger: *When a new email arrives (V2)*
- Search for **Outlook 365** connector or **Gmail Connector**.  
- Select **When a new email arrives (V2)**.  
- Configure:  
  - **Folder**: `Inbox`  
  - **Subject Filter**: `testing` ✅ (this ensures the trigger only fires when subject contains "testing").  

### 4. Add Action: *Send an email (V2)*
- Add a new action → **Send an email (V2)**.  
- Configure:  
  - **To**: `From` (dynamic content → Sender’s email address)  
  - **Subject**:  
    ```text
    Re: @{triggerOutputs()?['body/Subject']}
    ```  
  - **Body**:  
    ```text
    Hello,

    This is an automated reply regarding your email with subject: "@{triggerOutputs()?['body/Subject']}".

    Regards,  
    Jagrit
    ```  
### 5. Save & Test
- Click **Save**.  
- Send an email to yourself (or from another account) with subject = `testing`.  
- The Logic App will trigger and send an **auto-reply**.  

