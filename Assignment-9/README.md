<img width="1920" height="1080" alt="Screenshot (2290)" src="https://github.com/user-attachments/assets/6065eb51-4bfe-40a0-b3cf-74686ebfada6" /># Assignment-9: Palindrome Number Checker - Azure Logic App

This project demonstrates an **Azure Standard Logic App** workflow that checks whether a given number is a palindrome using **JavaScript inline code**.  
It exposes an **HTTP endpoint** where you can send a JSON payload, and the Logic App validates the input, processes the number, and returns whether it is a palindrome or not.

---

## 🚀 Workflow Overview

1. **Trigger** – The workflow starts when an **HTTP POST request** is received with a JSON body containing a number.  
2. **Inline JavaScript Code** – The number is validated and processed:
   - Rejects invalid inputs (null, undefined, non-numeric, empty string).
   - Rejects negative numbers as non-palindromes.
   - Reverses the number mathematically.
   - Compares original and reversed number to check palindrome.
3. **Response** – Returns a structured JSON response with:
   - The input number.
   - Boolean result (`isPalindrome`).
   - A descriptive message.

---

## 🛠️ Steps to Recreate

### 1. Create a Logic App (Standard)
- Open **Azure Portal**.
- Create a **Logic App (Standard)** resource.
- Choose **Stateful workflow** type.
<img width="1920" height="1080" alt="Screenshot (2289)" src="https://github.com/user-attachments/assets/9cbe2bdc-1403-473d-adff-946ea522a2f2" />

---

### 2. Add HTTP Request Trigger
- Add a trigger: **When a HTTP request is received**.
- Set **method** = `POST`.
- Define the JSON schema:

```json
{
  "type": "object",
  "properties": {
    "number": {
      "type": ["integer", "null"]
    }
  },
  "required": ["number"]
}
```
<img width="1920" height="1080" alt="Screenshot (2290)" src="https://github.com/user-attachments/assets/664042ad-ae22-4bc3-be6e-42ad861ba26f" />

### 3. Add Inline JavaScript Code
- Add action: Inline Code → JavaScript.
- Paste the following code:

```javascript
// Get the number from HTTP trigger
let input = workflowContext.trigger.outputs.body;
let num = input.number;

// Check if number is undefined, null, or invalid
if (num === null || num === undefined || isNaN(num) || num === "") {
    return { result: "Input is undefined, null, or not a valid number!" };
}

// Handle negative numbers as non-palindrome
if (num < 0) {
    return { 
        number: num, 
        isPalindrome: false, 
        message: "Negative numbers are not considered palindrome" 
    };
}

// Initialize variables
let originalNum = num;
let reversedNum = 0;

// Reverse the number mathematically
while (num > 0) {
    let digit = num % 10;          
    reversedNum = reversedNum * 10 + digit;
    num = Math.floor(num / 10);    
}

// Check palindrome
let isPalindrome = originalNum === reversedNum;

return { 
    number: originalNum, 
    isPalindrome: isPalindrome, 
    message: isPalindrome ? "Number is a palindrome" : "Number is not a palindrome" 
};

```
<img width="1920" height="1080" alt="Screenshot (2294)" src="https://github.com/user-attachments/assets/51bff222-afc2-438e-9605-9cdda905fa46" />
<img width="1920" height="1080" alt="Screenshot (2295)" src="https://github.com/user-attachments/assets/d6c33218-c930-4365-88d5-012174949496" />

### 4. Add Response Action
- Add Response action.
- Set:
  - Status Code → 200
  - Body → @outputs('Execute_JavaScript_code')
<img width="1920" height="1080" alt="Screenshot (2296)" src="https://github.com/user-attachments/assets/f22bd980-6dfd-4fd9-be2a-b447fbc792cf" />
 
