# Lab 01: Configuring Microsoft Entra ID Device Settings & Conditional Access MFA

---

## 01 Overview
Device identity is a critical component of Zero Trust access control. This lab focuses on controlling hardware join limits in Microsoft Entra ID and deploying a **Conditional Access Policy** to enforce Multi-Factor Authentication (MFA) and compliant device access for administrative accounts.

---

## 02 Business Scenario
**Company:** Contoso Health  
**Problem:** Administrative accounts are vulnerable to credential theft when accessed from unmanaged devices or untrusted locations. Legacy per-user MFA is too static and does not evaluate device health or location context.  
**Solution:** 1. Restrict the maximum number of devices a user can join to Microsoft Entra ID to `20`.
2. Deploy a Conditional Access policy requiring **Global Administrators** to complete MFA **AND** use an **Entra hybrid joined device** when connecting from untrusted locations.

---

## 03 On-Premises to Azure Mapping

| On-Premises Concept | Azure Cloud Equivalent | Operational Value |
| :--- | :--- | :--- |
| **Active Directory Domain Join** | **Microsoft Entra Hybrid Join** | Registers devices in the cloud while retaining local AD domain controllers. |
| **GPO / Firewall Location Rules** | **Conditional Access Named Locations** | Scopes access rules based on trusted corporate public IP ranges. |
| **Static User Permissions** | **Conditional Access Grant Controls** | Dynamically evaluates user role, device state, and location risk at login time. |

---

## 04 Architectural Blueprint

```text
+-------------------------------------------------------------------------+
|                        Microsoft Entra ID Tenant                        |
+-------------------------------------------------------------------------+
                                     |
    User: Global Administrator       |       Location: Untrusted IP
                                     v
+-------------------------------------------------------------------------+
| Conditional Access Policy: "CA-Enforce-Admin-MFA-CompliantDevice"       |
|                                                                         |
| Conditions:                                                             |
|   - Users     : Global Administrator Role                               |
|   - Apps      : All Cloud Apps                                          |
|   - Location  : Exclude Trusted Office IP Range                         |
|                                                                         |
| Grant Controls (REQUIRE ALL):                                           |
|   [✓] Require Multi-Factor Authentication                               |
|   [✓] Require Microsoft Entra Hybrid Joined Device                      |
+-------------------------------------------------------------------------+
                                     |
              +----------------------+----------------------+
              |                                             |
              v                                             v
     Valid MFA + Hybrid Device                     Unmanaged / Non-Joined
     [ ACCESS GRANTED ✅ ]                        [ ACCESS BLOCKED ❌ ]
