# Storage Account & CSV Upload — Step-by-step README

## Overview

This README shows **exact, step-by-step** instructions to:

1. Create an **Azure Storage Account** (Portal + CLI).
2. Create a **Blob Container**.
3. Create a **CSV file (StudentDetails.csv)** and upload it to the container (Portal + CLI).

Use this when you want to store student details as CSV in Azure Blob Storage.

---

## Prerequisites

- An **Azure subscription** with permission to create resources.
- (Optional but recommended) **Azure CLI** installed locally. See https://docs.microsoft.com/cli/azure/install-azure-cli for installation.
- Basic familiarity with Azure Portal.

---

## Example CSV (StudentDetails.csv)

Create a file named `StudentDetails.csv` with the following content:

```csv
Name,Age
Rahul,25
Anita,30
```

You can create this file with any text editor or run (macOS / Linux / WSL / Git Bash):

```bash
cat > StudentDetails.csv <<'CSV'
Name,Age
Rahul,25
Anita,30
CSV
```

---

## PART A — Using Azure Portal (GUI)

### Step-1: Create a Resource Group (optional but recommended)

1. Sign in to the **Azure Portal** (https://portal.azure.com).
2. Search for **Resource groups** and click **+ Create**.
3. Select Subscription, give it a name (example: `rg-student-csv`), pick a Region, then **Review + create** → **Create**.

### Step-2: Create a Storage Account

1. In Portal search box type **Storage accounts** → click **+ Create**.
2. Under **Basics** fill the required fields:
   - **Subscription**: your subscription.
   - **Resource group**: choose the RG created above (or select an existing one).
   - **Storage account name**: must be globally unique, lowercase, 3–24 characters (example: `jagritstorageacct123`).
   - **Region**: nearest region (e.g., `Central India`).
   - **Performance**: **Standard** (default).
   - **Redundancy**: **Locally-redundant storage (LRS)** is cheapest and fine for testing.
3. Leave other defaults unless you have network/security requirements.
4. Click **Review + create** → ensure validation passes → **Create**.

Wait a couple minutes for deployment.

### Step-3: Create a Blob Container

1. Open the created Storage Account from the Portal (search the account name).
2. In the left menu under **Data storage** click **Containers**.
3. Click **+ Container**.
   - **Name**: `csvfiles` (or any valid lowercase name).
   - **Public access level**: set to **Private (no anonymous access)**.
4. Click **Create**.

### Step-4: Upload the CSV via Portal

1. Inside the `csvfiles` container click **Upload**.
2. **Browse** → choose the `StudentDetails.csv` file you created.
3. (Optional) Under Advanced make sure **Content type** shows `text/csv`.
4. Click **Upload**.

### Step-5: Verify

1. After upload you will see `StudentDetails.csv` listed in the container.
2. Click the blob name → click **Download** to open it locally and inspect the CSV contents.

---
