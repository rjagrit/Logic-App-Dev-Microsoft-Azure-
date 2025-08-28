# ProductCSVLogicApp — Step-by-step README

## Overview

**ProductCSVLogicApp** is an Azure **Consumption Logic App** that receives a JSON payload (list of products) via an HTTP endpoint, converts the JSON product array into a CSV file, and uploads that CSV to an Azure Blob Storage container as `Product.csv`.

---

## Prerequisites

- An **Azure subscription** with permissions to create Logic Apps and Storage Accounts.
- A **Storage Account** and a blob **container** (example name: `product-data`).
- Optional: Azure CLI or Postman / curl to test the HTTP trigger.

---

## Files included

- `README.md` (this file)
- Example request body (use this as `input.json` when testing)

### Example Input (input.json)

```json
{
  "products": [
    {
      "productId": 1,
      "productName": "Chair",
      "description": "Comfortable chair for home or office",
      "price": 49.99,
      "quantity": 100
    },
    {
      "productId": 2,
      "productName": "Desk",
      "description": "Large desk with plenty of workspace",
      "price": 149.99,
      "quantity": 50
    },
    {
      "productId": 3,
      "productName": "Bookshelf",
      "description": "Tall bookshelf for storing books and decorations",
      "price": 79.99,
      "quantity": 75
    }
  ]
}
```

---

## Step-by-step: Create the Logic App & Blob flow

### Step 1 — Create (or use) an Azure Storage Account + Container

1. In Azure Portal, go to **Storage accounts** → **+ Create**.
2. Fill required fields (Subscription, Resource group, Region). Create the account.
3. After creation, open the storage account → **Containers** → **+ Container**.
4. Name the container `product-data` (or your preferred name) and set access level (usually **Private**).

> **Optional (CLI)**:
>
> ```bash
> az storage account create --name MyStorageAcct --resource-group MyRG --location eastus
> az storage container create --name product-data --account-name MyStorageAcct
> ```

---

### Step 2 — Create a Consumption Logic App

1. In Azure Portal, search **Logic App** and click **+ Create**.
2. Choose **Consumption** (NOT Standard) and fill:
   - **Subscription**
   - **Resource group**
   - **Logic App name**: `ProductCSVLogicApp` (suggested)
   - **Region**
3. Click **Review + create** → **Create**.

---

### Step 3 — Add the HTTP Trigger (When an HTTP request is received)

1. Open the created Logic App and click **Logic App Designer**.
2. Choose the template **When an HTTP request is received** (HTTP trigger).
3. Click **Use sample payload to generate schema** and paste the **Example Input** JSON (from above). This will create the request JSON schema.

**Generated JSON Schema (example)**

```json
{
  "type": "object",
  "properties": {
    "products": {
      "type": "array",
      "items": {
        "type": "object",
        "properties": {
          "productId": { "type": "integer" },
          "productName": { "type": "string" },
          "description": { "type": "string" },
          "price": { "type": "number" },
          "quantity": { "type": "integer" }
        }
      }
    }
  }
}
```

> After saving the trigger, Logic Apps will show an HTTP POST URL (copy it for testing).

---

### Step 4 — Add Data Operation: Create CSV Table

1. Click **+ New step** → search **Data Operations** → select **Create CSV table**.
2. In **From** field, provide the products array. Two options:
   - **Dynamic content**: choose the `products` token from the trigger (if available), or
   - **Expression**: click **Expression** and enter:
     ```text
     triggerBody()?['products']
     ```
     then click **OK** (this will appear as `@triggerBody()?['products']`).
3. (Optional) For predictable column order, set **Columns** to **Custom** and add these columns in this order: `productId`, `productName`, `description`, `price`, `quantity`.

**Note:** If `From` is empty or wrong, you will get validation errors (e.g. `WorkflowRunActionInputsMissingProperty`) — ensure you're passing the `products` array exactly.

---

### Step 5 — Add Azure Blob Storage Action: Create Blob

1. Click **+ New step** → search **Azure Blob Storage** → choose **Create blob**.
2. If not connected, create a connection. You can:
   - **Sign in with account key / connection string** (simple), **OR**
   - Use **System-assigned managed identity** for the Logic App and grant it the **Storage Blob Data Contributor** role on the Storage Account.
3. Configure the action:
   - **Folder / Container**: `product-data` (the container you created)
   - **Blob name**: `Product.csv` (or use an expression to add timestamp)
   - **Blob content**: use the output of the _Create CSV table_ action. Enter the expression or dynamic content:
     ```text
     outputs('Create_CSV_table')
     ```
   - (Optional) Set **Content type** to `text/csv` if the connector exposes this property.

**Optional Dynamic filename with timestamp**: If you want unique filenames,
use a Compose or expression for the blob name, e.g.:

```text
concat('Product_', replace(replace(replace(utcNow(),':','-'),'T','_'),'.','-'), '.csv')
```

This avoids invalid characters in the filename.

---

### Step 6 — Save and Test the Logic App

1. Click **Save** in the Logic App designer.
2. Copy the HTTP POST URL from the HTTP trigger.
3. Test with curl or Postman.

**cURL Example**

```bash
curl -X POST '<YOUR_HTTP_TRIGGER_URL>' \
  -H 'Content-Type: application/json' \
  -d @input.json
```

(Replace `<YOUR_HTTP_TRIGGER_URL>` with the trigger URL and ensure `input.json` contains the Example Input.)

**Postman**

- Create a POST request to the trigger URL.
- Set `Content-Type: application/json`.
- Paste the Example Input JSON in the body and send.

---

### Step 7 — Verify Blob

1. In Azure Portal, open your **Storage Account** → **Containers** → `product-data`.
2. You should see `Product.csv` (or `Product_YYYY...csv` if you used timestamp).
3. Click to download and open — it should look like:

```csv
productId,productName,description,price,quantity
1,Chair,Comfortable chair for home or office,49.99,100
2,Desk,Large desk with plenty of workspace,149.99,50
3,Bookshelf,Tall bookshelf for storing books and decorations,79.99,75
```

---

## Troubleshooting & Tips

- **Validation error (Create_CSV_table inputs missing)**: Ensure `Create CSV table` → **From** is set to `@triggerBody()?['products']` or the correct dynamic token.
- **Blob connector errors / permission denied**: If you used managed identity, grant **Storage Blob Data Contributor** role to the Logic App's identity on the storage account. If using a connection string/key, verify the key and account name.
- **Incorrect CSV headers or order**: Use **Custom** columns in the Create CSV Table action to force the header order.
- **Large payloads / timeouts**: Consumption Logic Apps have runtime limits. For very large files, consider chunking or using an integration service.

---

## Optional Enhancements

- Add a **Response** action to return a 200 response with a short message or the blob URL.
- Use a **Compose** action to create custom CSV headers or do string replacements before upload.
- Add **error handling** (Scope + Configure run after + Send email) to capture failures.

---

## Summary

This Logic App receives product JSON, transforms it into CSV, and stores `Product.csv` in Azure Blob Storage. Follow the steps above to build, test, and verify. Adjust container names, action names, and filename expressions to match your environment.

---

If you want, I can:

- Add a ready-to-paste Logic Apps workflow definition (ARM template) for automation,
- Add screenshots for each step, or
- Add a small diagram of the flow for the README.
