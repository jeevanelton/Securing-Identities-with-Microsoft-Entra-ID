# 🔐 Microsoft Azure Basics: Securing Identities with Microsoft Entra ID

![Azure](https://img.shields.io/badge/Microsoft-Azure-blue)
![Security](https://img.shields.io/badge/Cloud-Security-green)
![Identity](https://img.shields.io/badge/Identity-Microsoft%20Entra%20ID-purple)

## 📌 Project Overview

This project simulates the role of a **Junior Cloud Security Engineer** at **Contoso Ltd.**, where the organization is migrating its workforce to the cloud using **Microsoft Entra ID (formerly Azure Active Directory)** as the identity provider.

The goal of this lab is to implement identity security best practices by:

- Creating and managing user identities
- Organizing users into security groups
- Applying least privilege access using RBAC
- Enforcing Multi-Factor Authentication (MFA)
- Blocking risky sign-ins using Conditional Access
- Monitoring authentication activity through sign-in logs

> **Security Principle:**  
> Identity is the new security perimeter in cloud environments. If an attacker compromises a valid identity, traditional network security controls may not prevent unauthorized access.

---

# 🎯 Scenario

Contoso Ltd. is onboarding a new **Finance Team**.

The security requirement from management:

> "Create finance user accounts, organize them into a group, provide only required access, enforce MFA, block risky external sign-ins, and verify activity through monitoring."

---

# 🏗️ Architecture Overview

```
                 Users
                   |
                   |
          +----------------+
          | Finance Group  |
          +----------------+
                   |
                   |
          Microsoft Entra ID
                   |
     +-------------+-------------+
     |                           |
 Conditional Access        RBAC Permissions
     |                           |
     |                           |
 MFA Enforcement          Least Privilege Access
     |
 Sign-in Risk Protection

```

---

# 🛠️ Lab Environment

## Requirements

Before starting, ensure:

- Microsoft Azure Account
- Microsoft Entra ID Tenant
- Global Administrator / Security Administrator permissions
- Microsoft Entra ID P1/P2 license for Conditional Access

Alternative:

- Enable Security Defaults if Conditional Access is unavailable

---

# 🔧 Tools Used

| Tool | Purpose |
|---|---|
| Azure Portal | Cloud resource management |
| Microsoft Entra Admin Center | Identity management |
| Azure CLI | Command-line administration |
| Microsoft Entra ID | Identity and access management |

---

# 🚀 Implementation Steps

---

# Exercise 1: Create Finance User Accounts

## Objective

Create new employee identities for the Finance department.

### Steps

1. Open Azure Portal

2. Navigate:

```
Microsoft Entra ID
        |
        Users
        |
        New User
```

3. Create users:

Example:

```
finance.user1@contoso.com
finance.user2@contoso.com
finance.manager@contoso.com
```

4. Configure:

- Display Name
- Username
- Password
- Department = Finance

---

# Exercise 2: Create Finance Security Group

## Objective

Organize finance users into a single security boundary.

Navigate:

```
Microsoft Entra ID
        |
        Groups
        |
        New Group
```

Configuration:

```
Group Type:
Security

Group Name:
Finance-Team

Membership Type:
Assigned
```

Add:

```
finance.user1
finance.user2
finance.manager
```

---

# Exercise 3: Implement Least Privilege Access (RBAC)

## Objective

Provide only required permissions.

Azure RBAC follows:

```
Who?
 |
User / Group

What?
 |
Role

Where?
 |
Resource Scope
```

Example:

Finance users require storage access:

Assign:

```
Role:
Storage Blob Data Reader

Scope:
Finance Storage Account
```

Avoid:

```
Owner
Global Administrator
Contributor
```

unless required.

---

# Exercise 4: Enable Multi-Factor Authentication (MFA)

## Objective

Protect identities even if passwords are compromised.

## Option 1: Conditional Access MFA

Navigate:

```
Microsoft Entra ID

Security

Conditional Access

Create Policy
```

Policy:

```
Name:
Require MFA for Finance Users

Users:
Finance-Team

Cloud Apps:
All Applications

Grant:
Require Multi-Factor Authentication

Enable:
On
```

---

## Option 2: Security Defaults

If Conditional Access is unavailable:

Enable:

```
Microsoft Entra ID

Properties

Manage Security Defaults

Enable
```

This automatically requires MFA registration.

---

# Exercise 5: Block Risky Sign-ins Outside Country

## Objective

Prevent suspicious authentication attempts.

Create Conditional Access Policy:

```
Name:
Block Risky Foreign Sign-ins
```

Users:

```
Finance-Team
```

Locations:

Example:

```
Trusted Location:
New Zealand
```

Condition:

```
Countries outside NZ
```

Access:

```
Block Access
```

Enable:

```
On
```

---

# Exercise 6: Monitor Sign-in Activity

## Objective

Verify security controls are working.

Navigate:

```
Microsoft Entra ID

Monitoring

Sign-in Logs
```

Review:

- User login attempts
- Location
- IP Address
- MFA status
- Risk detection
- Authentication method

Example:

```
User:
finance.user1

Status:
Success

MFA:
Passed

Location:
New Zealand
```

Risk example:

```
User:
finance.user2

Location:
Unknown Country

Result:
Blocked
```

---

# 🔍 Security Validation Checklist

| Security Control | Status |
|-|-|
| Finance users created | ✅ |
| Finance group created | ✅ |
| RBAC least privilege applied | ✅ |
| MFA enabled | ✅ |
| Conditional Access configured | ✅ |
| Risky sign-ins blocked | ✅ |
| Sign-in logs reviewed | ✅ |

---

# 🧠 Key Security Concepts Learned

## Identity Security

Modern cloud security focuses on:

```
Verify Identity
       +
Limit Access
       +
Monitor Activity
```

---

## Least Privilege

Users receive:

```
Minimum permissions
+
Only required resources
+
Limited duration
```

---

## Zero Trust Approach

Implemented principles:

```
Never Trust
Always Verify

Verify:
- Identity
- Location
- Device
- Risk
```

---

# 📚 Skills Demonstrated

- Microsoft Entra ID Administration
- Azure Identity Security
- RBAC Implementation
- Conditional Access Policies
- MFA Enforcement
- Cloud Security Monitoring
- Zero Trust Security Model

---

# 👨‍💻 Author

**Jeevan Elton**

Cloud Security | Network Security | Cybersecurity
