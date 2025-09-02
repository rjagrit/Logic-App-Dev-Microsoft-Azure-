# Logic App-8: Multi-User Admin Check (variable demonstration)

## Step 1 — Create the Logic App (Consumption)
1.	Azure Portal → Create a resource → Logic App (Consumption) → Create
2.	Fill: Name (e.g., VarsAllInOneDemo), Resource Group, Region → Review + Create → Create
3.	Open the resource → Logic App Designer → Blank Logic App

## Step 2 — Add HTTP Trigger
1.	In Designer, select When an HTTP request is received
2.	(Optional) Leave Request Body JSON Schema empty
3.	Click Save (top-right) → Copy the generated HTTP POST URL (for Postman)
<img width="900" height="905" alt="image" src="https://github.com/user-attachments/assets/9baa6e04-d3d4-4bef-93dc-19818bc0c1eb" />

## Step 3 — Initialize Variables (All Data Types)
Add each action via + New step → “Initialize variable”.
Naming is important—exactly as written below.
1.	String
•	Action: Initialize variable
•	Name: greeting
•	Type: String
•	Value: Hello Jagrit

<img width="900" height="476" alt="image" src="https://github.com/user-attachments/assets/4d341c93-4af7-4959-9f27-934b4854f6d2" />

2.	Integer
•	Action: Initialize variable
•	Name: count
•	Type: Integer
•	Value: 10
<img width="1090" height="421" alt="image" src="https://github.com/user-attachments/assets/2019d23f-fc2d-4ec4-9cab-32934594940d" />

3.	Float (2 vars to avoid self-reference)
•	Action: Initialize variable
•	Name: priceOriginal
•	Type: Float
•	Value: 100.5
<img width="1090" height="408" alt="image" src="https://github.com/user-attachments/assets/4b5cca8c-e003-4205-b7c2-fc78a32dbf40" />

•	Action: Initialize variable
•	Name: priceWithTax
•	Type: Float
•	Value: 0
<img width="1090" height="417" alt="image" src="https://github.com/user-attachments/assets/e9c862c6-e22e-4236-97c1-1acbf2a3b15f" />

4.	Boolean
•	Action: Initialize variable
•	Name: isAdmin
•	Type: Boolean
•	Value: true
<img width="1090" height="338" alt="image" src="https://github.com/user-attachments/assets/25b4cd67-b6f2-4b76-9b10-8746d0bacfdc" />

5.	Array
•	Action: Initialize variable
•	Name: fruits
•	Type: Array
•	Value: ["Apple"]
<img width="1090" height="410" alt="image" src="https://github.com/user-attachments/assets/e9be9bc2-a26d-44e9-b102-16735be6ce6c" />

6.	Object
•	Action: Initialize variable
•	Name: user
•	Type: Object
•	Value:
<img width="1090" height="483" alt="image" src="https://github.com/user-attachments/assets/781d2cbf-c1c2-46b8-9910-070af3cb7d19" />

7.	String (for append demo)
•	Action: Initialize variable
•	Name: note
•	Type: String
•	Value: Today: 
Tip: Aap Run after set na bhi karein to Designer sequence me actions chal jayenge; varna har next action ke … (More) → Configure run after me previous = Succeeded set kar sakte ho.
<img width="1090" height="357" alt="image" src="https://github.com/user-attachments/assets/d60d72fd-9099-4749-9400-609cc5965f35" />

Step 4 — Set / Increment / Append Actions
Ab variable actions add karein (exact action names):
A) Set variable (String overwrite)
•	Action: Set variable
•	Name: greeting
•	Value: Welcome Jagrit
<img width="1090" height="469" alt="image" src="https://github.com/user-attachments/assets/0a277e11-fc6a-4c76-91ea-a13e0627d4bc" />

B) Increment variable (Integer)
•	Action: Increment variable
•	Name: count
•	Value: 5
Result: count = 15
<img width="1090" height="449" alt="image" src="https://github.com/user-attachments/assets/2f3393ae-ab66-4b86-820d-fd31d9af3e77" />

C) Set variable (Float computed from another var)
•	Action: Set variable
•	Name: priceWithTax
•	Value (Expression): mul(variables('priceOriginal'), 1.18)
o	Click Expression tab, type: mul(variables('priceOriginal'), 1.18) → OK
✔️ Ye self-reference nahi hai (dusre var se compute ho raha).
<img width="1090" height="284" alt="image" src="https://github.com/user-attachments/assets/1ec34e73-8ff9-4420-b76d-0472aaed3d15" />

D) Append to string variable
•	Action: Append to string variable
•	Name: note
•	Value: Sunny
Result: note = "Today: Sunny"
<img width="1090" height="431" alt="image" src="https://github.com/user-attachments/assets/7840a71c-bf5e-4e32-8273-ea160775abbf" />

E) Append to array variable
•	Action: Append to array variable
•	Name: fruits
•	Value: Banana
Result: fruits = ["Apple", "Banana"]
<img width="1090" height="417" alt="image" src="https://github.com/user-attachments/assets/d28ed701-ac15-4a66-991e-702998a8a22c" />

## Response
<img width="1090" height="885" alt="image" src="https://github.com/user-attachments/assets/a9da1d6b-fdf1-4eec-b11c-8f04b9e7c255" />

The Output:
<img width="1090" height="617" alt="image" src="https://github.com/user-attachments/assets/7e2a8e37-1b66-40c8-86dc-c4942635ac4a" />
<img width="1090" height="542" alt="image" src="https://github.com/user-attachments/assets/62184a43-7d70-4f4e-8c96-d2ff82a5edc1" />
