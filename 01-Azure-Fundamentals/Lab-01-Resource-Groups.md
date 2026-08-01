# Lab 01: Subscriptions, Resource Group Governance, Tags & Resource Locks

---

## 01 Overview
This lab establishes the foundational administrative hierarchy in Microsoft Azure. It demonstrates how to organize enterprise workloads using **Resource Groups**, enforce cost attribution through **Tags**, and prevent accidental resource deletion using **Resource Locks**.

---

## 02 Business Scenario
**Company:** Contoso Health  
**Problem:** Workloads are deployed without cost center visibility, and accidental deletions have caused minor outages in non-production environments.  
**Solution:** Implement standardized Resource Groups (`rg-core-prod-eastus-01`), mandatory metadata tagging (`Environment`, `Department`, `CostCenter`), and apply a `CanNotDelete` lock to protect core infrastructure.

---

## 03 On-Premises to Azure Mapping

| On-Premises Concept | Azure Equivalent | Operational Function |
| :--- | :--- | :--- |
| Data Center Billing Unit | Azure Subscription | Primary scope for billing, limits, and quotas. |
| Folder / Organizational Unit | Resource Group | Lifecycle boundary for related resources. |
| CMDB Asset Tags | Azure Tags | Key-value pairs for metadata and cost tracking. |
| NTFS Read-Only Permission | Resource Lock | Protects resources from deletion or modifications. |

---

## 04 Architectural Blueprint

```text
+-------------------------------------------------------------------------+
|                          Azure Subscription                             |
+-------------------------------------------------------------------------+
                                     |
                                     v
+-------------------------------------------------------------------------+
| Resource Group: rg-core-prod-eastus-01                                  |
|                                                                         |
| Tags:                                                                   |
|   - Environment : Production                                            |
|   - Department  : IT-Infrastructure                                     |
|   - CostCenter  : CC-1001                                               |
|                                                                         |
| Lock: lock-prevent-accidental-delete (Type: CanNotDelete)               |
+-------------------------------------------------------------------------+
