# Logic-App-Dev (Microsoft-Azure) _by Khoj Info.Pvt. Ltd._
A collection of Azure Logic Apps workflows demonstrating automation scenarios with step-by-step explanations

1) Logic App-1: This Logic App automatically replies to emails when a new email arrives in the inbox with the subject **"testing"**.
2) Logic App-2: Address validation using an HTTP trigger (if condition)
3) Logic App-3: Order status handling using a Switch control and HTTP trigger.
4) Logic App-4: This Logic App demonstrates how to use parallel branches in Azure Logic Apps so that multiple actions run at the same time.
5) Logic App-5: This Logic App receives an array of names via an HTTP POST request, appends "Hello " to each name, and returns the greetings array.
6) Logic App-6: This Logic App validates the group of a user from an HTTP POST request. It returns “Welcome Admin” if the user belongs to the Admin group; otherwise, it returns **Access Denied**.
7) Logic App-7: This Logic App receives an array of users via HTTP POST, checks which users belong to the Admin group, and returns.
8) Logic App-8: This Logic App receives an array of users via HTTP POST, checks which users belong to the Admin group, and returns.
9) Logic App-9: This Logic App receives an array of users via HTTP POST, checks which users belong to the Admin group, and returns.
10) Logic App-10 Logic App processes an array of employees sent via HTTP POST and performs multiple operations:
  - Creates a CSV table of employees.
  - Creates an HTML table of employees.
  - Filters employees in the IT department.
  - Selects employee names and joins them as a comma-separated string.
  - Selects employee names and emails for structured output.
  
12) Logic App-11: This Logic App generates a CSV table of products and sends it via email repeatedly until a specified run count is reached.
13) Logic App-12: This Logic App runs on a scheduled recurrence, initializes variables, composes user data, and sends it via Gmail if a condition is met.
14) Logic App-13: This Logic App executes inline JavaScript code and returns the result as an HTTP response.
15) Logic App-14: This Logic App receives a number via HTTP POST request, validates the input, and returns whether the number is odd or even using inline JavaScript.
16) Logic App-15: This Logic App automatically saves attachments from incoming Outlook emails to Azure Blob Storage.

---
## Assignments
1) Assignment-0: This Logic App receives a list of products via an HTTP POST request, converts it into a CSV table, and uploads it to Azure Blob Storage.
2) Assignment-1: Create a storage account and a Container, and also upload a CSV file with three columns.
3) Assignment-2: This guide explains how to create an Azure Service Bus Topic with Subscriptions that filter messages based on the MessageType property.
4) Assignment-3: Azure Logic App – Blob Trigger with Unzip to Another Folder
5) Assignment-4: This project demonstrates how to create an Azure Logic App (Standard) with a Recurrence Trigger. The workflow is scheduled to run every Monday and Friday, every hour at exactly 00 minutes, starting from 2025-08-28T00:00:00 in the AUS Eastern Standard Time zone.
6) Assignment-5: This Azure Logic App (Standard) workflow receives a JSON payload via HTTP POST, converts it into XML, and then stores the file in an Azure Blob Storage container.
7) Assignment-6: This project contains an Azure Standard Logic App workflow that accepts JSON data via an HTTP POST request, converts the data into a CSV file, and stores it in Azure Blob Storage.
8) Assignment-8: Email to CSV Converter using Azure Logic Apps
9) Assignment-9: This project demonstrates an Azure Standard Logic App workflow that checks whether a given number is a palindrome using JavaScript inline code.
10) Assignment-10: This Logic App creates an API endpoint that generates a sequence of numbers, where each number is double the previous one.
The workflow runs for 10 iterations, starting from 1, and returns the sequence as an HTTP response.
11) Assignment-11:This Logic App is designed to validate a file in Azure Blob Storage based on the file path provided through an HTTP request.
  - It performs the following checks:
  - File existence in Blob Storage
  - File content check (whether empty or has valid data)
  - Returns appropriate HTTP status codes and messages.

12) Assignment-12:This repository contains an Azure Standard Logic App workflow that validates incoming JSON payloads for required fields.
The Logic App ensures all required fields are present and contain at least one character. If validation passes, a 200 OK response is returned. Otherwise, a 400 Bad Request response with details of the missing/invalid fields is returned.

