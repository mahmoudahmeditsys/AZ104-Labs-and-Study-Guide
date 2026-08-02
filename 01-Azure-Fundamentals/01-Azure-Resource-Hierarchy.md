# Lab 01: Azure Resource Hierarchy & Governance Basics

## 💡 Overview & Key Concepts
In Azure, all resources (like Virtual Machines, Storage Accounts, and Databases) must be organized in a structured hierarchy:

- **Management Groups:** Provide scope above subscriptions for enterprise governance.
- **Subscriptions:** An agreement with Microsoft that handles billing and access boundaries.
- **Resource Groups (RG):** A logical container that holds related Azure resources.
- **Tags:** Name/value pairs applied to resources for cost management and tracking.
- **Resource Locks:** Prevents accidental deletion (`CanNotDelete`) or modification (`ReadOnly`).

---

## 🧪 Hands-On Lab: Create Resource Group, Tagging, and Applying Locks

### Step 1: Create a Resource Group
1. Open the [Azure Portal](https://portal.azure.com).
2. Search for **Resource groups** and click **+ Create**.
3. Select your **Subscription**.
4. Resource Group name: `rg-az104-lab01-prod`
5. Region: `East US`
6. Click **Review + create** and then **Create**.

### Step 2: Apply Tags and Resource Locks
1. Open `rg-az104-lab01-prod`.
2. Select **Tags** from the left menu.
3. Add Key: `Environment`, Value: `Production`.
4. Add Key: `Owner`, Value: `CloudAdmin`. Click **Apply**.
5. Select **Locks** under *Settings*.
6. Click **+ Add**, Name: `lock-prevent-delete`, Lock type: `Delete`. Click **OK**.

---

## 💻 Commands Reference

### Azure CLI

```bash
# Create Resource Group
az group create --name rg-az104-lab01-prod --location eastus --tags Environment=Production Owner=CloudAdmin

# Apply a Delete Lock to the Resource Group
az lock create --name lock-prevent-delete --resource-group rg-az104-lab01-prod --lock-type CanNotDelete

````

### Azure PowerShell
```powershell
# Create Resource Group
New-AzResourceGroup -Name "rg-az104-lab01-prod" -Location "EastUS" -Tag @{Environment="Production"; Owner="CloudAdmin"}

# Apply Delete Lock
New-AzResourceLock -LockName "lock-prevent-delete" -LockLevel CanNotDelete -ResourceGroupName "rg-az104-lab01-prod"
```
