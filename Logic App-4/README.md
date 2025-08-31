## Logic App-4

Overview: This Logic App demonstrates how to use parallel branches in Azure Logic Apps so that multiple actions run at the same time.

1. Create Logic App (Consumption)

Trigger → HTTP Request
Add a sample JSON body (so you can test from Postman):
<img width="642" height="196" alt="image" src="https://github.com/user-attachments/assets/fa9cf86e-f608-4412-b7a1-325c3a0cd196" />
<img width="929" height="685" alt="image" src="https://github.com/user-attachments/assets/a9122d5b-1eff-4ae5-901e-7e922a81d4ce" />

2. Add Parallel Branch

After the HTTP trigger → click "+" → Add a parallel branch.
Now you’ll see two columns (branches).

Compose (branch-1)
<img width="1090" height="343" alt="image" src="https://github.com/user-attachments/assets/89269f16-472e-440c-95ca-12450302524f" />

Compose 1(branch-2)
<img width="1090" height="326" alt="image" src="https://github.com/user-attachments/assets/04568ab9-4989-433a-a196-90554100db03" />

3. Join the Branches

Below both branches, add a Response action.
In the Response Body, include both results:
<img width="1090" height="701" alt="image" src="https://github.com/user-attachments/assets/8b654673-b498-42e6-a647-c37c83cf6ce9" />

Now, if you want to merge it, go to settings->run after (then choose the desired action)
<img width="1090" height="589" alt="image" src="https://github.com/user-attachments/assets/05179166-5163-43ea-b9f3-8c8d1225cc80" />

Output:
<img width="1090" height="472" alt="image" src="https://github.com/user-attachments/assets/87605d94-ed59-42e0-9db0-d21ea843890e" />

Workflow
<img width="1090" height="690" alt="image" src="https://github.com/user-attachments/assets/b06a5c3c-7b46-4f9e-ba33-f2f2a0676bf3" />
