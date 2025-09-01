# Assignment-10: Azure Logic App - Doubling Sequence Generator

This Logic App creates an API endpoint that generates a **sequence of numbers**, where each number is double the previous one.  
The workflow runs for **10 iterations**, starting from `1`, and returns the sequence as an HTTP response.

---

## 📌 Features
- Triggered via **HTTP POST**.
- Initializes variables to store sequence and current value.
- Uses a **For Each loop** to:
  - Append the current value to an array.
  - Double the current value (`mul(x,2)`).
  - Update the variable for the next iteration.
- Returns the final sequence in the response.

---

## ⚙️ Workflow Steps

1. **Trigger: HTTP Request**
   - Type: `POST`
   - Endpoint is generated once you save the Logic App.
<img width="1920" height="1080" alt="Screenshot (2251)" src="https://github.com/user-attachments/assets/3a19e5ab-f068-439d-84bc-7e640f722554" />

2. **Initialize Variables**
   - `sequenceArray`: Array → `[]`
   - `currentValue`: Integer → `1`
<img width="1920" height="1080" alt="Screenshot (2252)" src="https://github.com/user-attachments/assets/8cd06dda-5e9e-4341-8ac4-21edac22f3c3" />
<img width="1920" height="1080" alt="Screenshot (2253)" src="https://github.com/user-attachments/assets/fcab3e91-2953-4e0c-b1f3-7af058b176c8" />

3. **For Each Loop**
   - Iterates over `range(0,9)` → 10 times.
<img width="1920" height="1080" alt="Screenshot (2254)" src="https://github.com/user-attachments/assets/27bd21f4-8cfa-4fd6-b908-9d1930a6a281" />

- Set the Degree of parallelism to 1
<img width="1920" height="1080" alt="Screenshot (2255)" src="https://github.com/user-attachments/assets/9d8638c9-9126-402f-8263-c3be45ecf2a6" />

   - Actions inside loop:
     - **Append to Array Variable** → Add current value to `sequenceArray`.
<img width="1920" height="1080" alt="Screenshot (2256)" src="https://github.com/user-attachments/assets/876a1d53-3578-4468-abba-28d505b1bf72" />

     - **Compose** → Calculate next value: `mul(variables('currentValue'), 2)`.
<img width="1920" height="1080" alt="Screenshot (2257)" src="https://github.com/user-attachments/assets/953e2a3c-300d-4818-a5fc-80ba9c9d7024" />

     - **Set Variable** → Update `currentValue` with doubled value.
<img width="1920" height="1080" alt="Screenshot (2258)" src="https://github.com/user-attachments/assets/2f00acb3-90f4-4144-9401-ab1e63e05f04" />

4. **Response**
   - Status Code: `200`
   - Body: `@variables('sequenceArray')`
<img width="1920" height="1080" alt="Screenshot (2259)" src="https://github.com/user-attachments/assets/1ed80ae6-e942-419a-b6d7-ebd551a4248f" />

## The output:
<img width="1920" height="1080" alt="Screenshot (2260)" src="https://github.com/user-attachments/assets/a0f4170d-71c1-4975-b521-688747de95e2" />



---
