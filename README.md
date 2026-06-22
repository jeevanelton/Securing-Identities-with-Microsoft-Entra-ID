# 🔐 Microsoft Entra ID Identity Security Lab

## Exercises: Securing Finance Team Identities in Azure

This lab demonstrates how a Cloud Security Engineer can onboard a new department into Microsoft Entra ID and apply identity security controls based on:

- Least Privilege Access
- Role-Based Access Control (RBAC)
- Multi-Factor Authentication (MFA)
- Conditional Access
- Sign-in Monitoring

---

# Exercise 1: Create Users for the Finance Team

## 🎯 Objective

Create user identities for new Finance department employees in Microsoft Entra ID.

---

## Steps

### 1. Open Microsoft Entra Admin Center

Navigate:

```
Identity
   |
Users
   |
All users
```

---

### 2. Create First User

Click:

```
+ New user
      |
Create new user
```

Configure:

```
User principal name:
priya.finance

Display name:
Priya Sharma
```

Allow Entra ID to generate a password.

Save the generated password securely.

Click:

```
Review + create
        |
Create
```

---

### 3. Create Second User

Repeat the same process:

```
User principal name:
raj.finance

Display name:
Raj Mehta
```

---

## Expected Output

The Entra ID user list should contain:

```
Priya Sharma
Raj Mehta
```

Example:

```
Users
 |
 +-- Priya Sharma
 |
 +-- Raj Mehta

```

---

# Exercise 2: Create Finance Security Group

## 🎯 Objective

Organize users into a security group to simplify access management.

Instead of assigning permissions individually:

```
User 1  ---> Permission
User 2  ---> Permission
User 3  ---> Permission
```

Use:

```
Finance-Team Group
          |
          |
     Permissions

```

---

## Steps

Navigate:

```
Identity

Groups

All groups
```

Select:

```
+ New Group
```

Configure:

```
Group Type:
Security

Group Name:
Finance-Team

Membership Type:
Assigned
```

---

Add members:

```
Priya Sharma

Raj Mehta
```

Click:

```
Create
```

---

## Expected Output

Security group created:

```
Finance-Team

Members:

- Priya Sharma
- Raj Mehta

```

---

# Exercise 3: Assign RBAC Role (Least Privilege)

## 🎯 Objective

Provide Finance users only the access required.

Azure RBAC follows:

```
Who?
 |
Finance-Team Group

What?
 |
Reader Role

Where?
 |
Azure Resource

```

---

## Steps

Open:

```
Azure Portal

Resource Group

Access Control (IAM)

```

Select:

```
+ Add

Add role assignment
```

---

Choose role:

```
Reader
```

Avoid excessive permissions:

❌ Owner  
❌ Contributor  
❌ Administrator  

---

Members:

Select:

```
User, group, or service principal
```

Choose:

```
Finance-Team
```

Click:

```
Review + assign
```

---

## Expected Output

Finance-Team receives:

```
Role:
Reader

Permission:

✔ View resources
✖ Modify resources
✖ Delete resources

```

---

# Exercise 4: Enable MFA with Conditional Access

## 🎯 Objective

Protect Finance accounts by requiring Multi-Factor Authentication.

---

## Requirement

Conditional Access requires:

```
Microsoft Entra ID P1/P2 License
```

If unavailable:

Use Security Defaults.

---

# Conditional Access Setup

Navigate:

```
Microsoft Entra Admin Center

Protection

Conditional Access

Policies
```

Create:

```
+ New Policy
```

Name:

```
Require MFA - Finance Team
```

---

## Assign Users

Include:

```
Finance-Team
```

---

## Target Resources

Select:

```
All cloud apps
```

---

## Access Control

Grant:

```
Require multifactor authentication
```

---

Enable:

```
Policy State:

ON
```

Create policy.

---

## Expected Output

Finance users must complete MFA registration.

Login flow:

```
Username
    |
Password
    |
MFA Verification
    |
Access Granted

```

---

# Fallback: Enable Security Defaults

If Conditional Access is unavailable:

Navigate:

```
Identity

Overview

Properties

Manage Security Defaults

```

Set:

```
Enabled
```

Save.

---

# Exercise 5: Block Foreign Sign-ins Using Named Locations

## 🎯 Objective

Prevent Finance users from signing in from unauthorized countries.

Example:

Allow:

```
New Zealand
```

Block:

```
Other Countries
```

---

# Step 1: Create Named Location

Navigate:

```
Protection

Conditional Access

Named Locations
```

Select:

```
+ Countries location
```

Create:

```
Name:

Allowed-Country

Country:

Your Country

```

Save.

---

# Step 2: Create Blocking Policy

Navigate:

```
Conditional Access

Policies

+ New Policy
```

Name:

```
Block Foreign Sign-ins - Finance
```

---

## Assign Users

Include:

```
Finance-Team
```

---

## Conditions

Locations:

Include:

```
Any location
```

Exclude:

```
Allowed-Country
```

---

## Access Control

Select:

```
Block access
```

Enable:

```
ON
```

Create.

---

## ⚠️ Security Recommendation

Always exclude an emergency admin account:

Example:

```
breakglass-admin
```

Otherwise you may lock yourself out.

---

## Expected Output

Authentication result:

Inside allowed country:

```
Login
 |
Allowed
```

Outside allowed country:

```
Login Attempt

     |
Conditional Access

     |
Blocked

```

---

# Exercise 6: Review Sign-in Logs

## 🎯 Objective

Verify security policies are working.

---

## Steps

Navigate:

```
Identity

Monitoring & health

Sign-in logs

```

Filter:

```
User:

priya.finance
```

---

Review:

| Field | Purpose |
|-|-|
| Status | Success / Failure |
| Location | Login country |
| MFA | Authentication result |
| Conditional Access | Applied policies |

---

Open a login event:

View:

```
Activity Details

        |

Conditional Access

```

---

## Expected Output

Example:

```
User:
priya.finance

Status:
Success

MFA:
Passed

Conditional Access:
Require MFA - Finance Team

Location Policy:
Evaluated

```

---

# Exercise 7: Create User Using Azure CLI

## 🎯 Objective

Create Entra ID users through automation.

---

## Login to Azure

```bash
az login
```

---

## Create User

Replace:

```
<your-tenant-domain>
```

with your Azure tenant domain.

```bash
az ad user create \
--display-name "Anita Verma" \
--user-principal-name "anita.finance@<your-tenant-domain>.onmicrosoft.com" \
--password "StrongP@ssw0rd!" \
--force-change-password-next-sign-in true
```

---

## Verify User Creation

```bash
az ad user list \
--filter "displayName eq 'Anita Verma'" \
--output table
```

---

## Expected Output

Example:

```
DisplayName
------------
Anita Verma

AccountEnabled
--------------
True

```

User is created successfully and must change password during first login.

---

# ✅ Lab Completion Checklist

| Task | Completed |
|-|-|
| Created Finance users | ✅ |
| Created Finance security group | ✅ |
| Applied RBAC least privilege | ✅ |
| Enabled MFA | ✅ |
| Configured Conditional Access | ✅ |
| Blocked foreign sign-ins | ✅ |
| Verified sign-in logs | ✅ |
| Created user using Azure CLI | ✅ |

---

# Skills Demonstrated

- Microsoft Entra ID Administration
- Azure Identity Security
- RBAC
- Conditional Access
- MFA Implementation
- Zero Trust Security
- Cloud Security Monitoring
- Azure CLI Automation
