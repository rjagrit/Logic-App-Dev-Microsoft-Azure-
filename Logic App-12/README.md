# Logic App: Recurring Email with Compose Action

This **Logic App** runs on a scheduled recurrence, initializes variables, composes user data, and sends it via Gmail if a condition is met.

---

## 🚀 Features

- Runs every 30 seconds (configurable recurrence)
- Initializes variables: First Name, Last Name, Age, Run Count
- Increments Run Count on each run
- Uses **Condition** to check run count limit (`runCount < 3`)
- Composes a JSON object with Full Name and Age
- Sends Gmail email with Compose results
- No action is performed if condition fails

---

## 🛠 Steps to Create

### 1. Create the Logic App

- Go to **Azure Portal → Create a Resource → Logic App (Consumption)**
- Select your **Resource Group**, provide a **Logic App Name**, choose a **Region**, and click **Create**

---

### 2. Open Logic App Designer

- Open the deployed Logic App → **Logic App Designer**
- Select **Blank Logic App**

---

### 3. Add Trigger: Recurrence

- Search **Recurrence** → select **Recurrence** trigger
- Configure:
  - **Frequency:** Second
  - **Interval:** 30
  - **Time Zone:** India Standard Time
- This triggers the workflow every 30 seconds

---

### 4. Initialize Variables

Add **Variables → Initialize Variable** actions **in sequence**:

1. **firstName**

   - Type: String
   - Value: `Jagrit`

2. **lastName**

   - Type: String
   - Value: `Rattan`

3. **ageVar**

   - Type: Integer
   - Value: `24`

4. **runCount**
   - Type: Integer
   - Value: `0`

> Each variable should run **after the previous variable succeeds**

---

### 5. Increment runCount

- Add **Variables → Increment Variable** action
- Configure:
  - Name: `runCount`
  - Value: `1`
- Run **after `counterVariable`**

---

### 6. Add Condition

- Add **Control → Condition** action
- Configure **Expression**:

```expression
@less(variables('runCount'), 3)
```
