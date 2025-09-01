# Azure Service Bus Topic & Subscription with Filter

This guide explains how to create an **Azure Service Bus Topic** with **Subscriptions** that filter messages based on the `MessageType` property.

---

## 🚀 Steps

### 1. Create a Service Bus Namespace
1. Go to **Azure Portal** → Search for **Service Bus**.
2. Click **+ Create**.
3. Fill in:
   - **Resource Group** → Choose or create one.
   - **Namespace Name** → e.g., `myservicebusns`.
   - **Pricing Tier** → Select **Standard** (needed for Topics & Subscriptions).
   - **Region** → Select nearest region.
4. Click **Review + Create** → **Create**.

---

### 2. Create a Topic
1. Open your **Service Bus Namespace** → **Topics**.
2. Click **+ Topic**.
3. Enter a name → e.g., `orders-topic`.
4. Save.

---

### 3. Create a Subscription
1. Inside the topic → Go to **Subscriptions**.
2. Click **+ Subscription**.
3. Provide a name → e.g., `electronics-subscription`.
4. Save.

---

### 4. Add a Filter Rule
1. Inside the subscription → Go to **Rules**.
2. Delete the default rule (`1=1`) if you don’t want all messages.
3. Click **+ Add Rule**:
   - **Name** → `MessageTypeFilter`.
   - **Filter Type** → SQL Filter.
   - **SQL Filter Condition**:
     ```sql
     MessageType = 'Electronics'
     ```
   - Save.

Now, this subscription will **only receive messages** where the `MessageType` property equals `Electronics`.

---

### 5. Send a Message with `MessageType` Property

#### Example in **C#**
```csharp
using Azure.Messaging.ServiceBus;

var client = new ServiceBusClient("<connection-string>");
var sender = client.CreateSender("orders-topic");

var message = new ServiceBusMessage("Order details for Laptop");
message.ApplicationProperties.Add("MessageType", "Electronics");

await sender.SendMessageAsync(message);
