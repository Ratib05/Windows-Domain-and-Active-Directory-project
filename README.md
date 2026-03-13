# Windows-Domain-and-Active-Directory-project

## Overview

This project demonstrates the deployment and administration of a **Windows Active Directory domain environment** within a virtual lab. The goal was to simulate a small enterprise network and perform common IT administration tasks such as domain setup, user and group management, file sharing, permission configuration, and centralized policy management.

The environment was built using **VMware Workstation**, with a Windows Server acting as the **Domain Controller** and a Windows 10 virtual machine acting as a **domain client**.

This lab demonstrates hands-on experience with **Active Directory administration, Windows Server management, Group Policy, and enterprise access control practices**.

---

## Technologies Used

* Windows Server 2025
* Windows 10 (Domain Client)
* VMware Workstation
* Active Directory Domain Services (AD DS)
* Group Policy Management
* NTFS Permissions
* SMB File Sharing

---

## Lab Architecture

The lab consists of a **Domain Controller** and a **domain-joined client workstation**.

```
Domain: corp.local

                ┌──────────────────────┐
                │  Domain Controller   │
                │  Windows Server      │
                │                      │
                │  Active Directory    │
                │  DNS Server          │
                │  File Server         │
                └──────────┬───────────┘
                           │
                           │ Domain Join
                           │
                ┌──────────▼───────────┐
                │   Windows 10 Client  │
                │   Domain Workstation │
                └──────────────────────┘
```

The Domain Controller also functions as a **file server hosting shared departmental directories**.

---

## Project Objectives

* Deploy a Windows Active Directory domain
* Configure Active Directory Domain Services
* Create users and security groups
* Organize domain objects using Organizational Units
* Configure shared folders
* Implement group-based access control
* Apply NTFS permissions
* Manage user resources using Group Policy

---

### Active Directory Deployment

Active Directory Domain Services was installed on the Windows Server machine and promoted to a **Domain Controller**.

```
Domain Name: corp.local
```

Installed services:

* Active Directory Domain Services
* DNS Server

The server now provides **centralized authentication, identity management, and directory services** for domain users and computers.



---

### Organizational Unit Structure

Organizational Units (OUs) were created to organize users and computers within the domain.

```
corp.local
│
├── Finance
├── HR
├── IT
├── Servers
└── Workstations
```

The **Workstations OU** was created to store domain-joined computers.

After joining the Windows 10 machine to the domain, the computer object was moved from the default **Computers container** into the **Workstations OU** to maintain a structured domain environment.

---

### User and Group Management

Users were created within their respective departmental Organizational Units.

Example:

```
Finance
└── Emma Lee
```

Security groups were created to implement **group-based access control**.

Groups created:

```
Finance_Users
HR_Users
IT_Users
```

Users were then added to their respective department groups.

Example:

```
Emma Lee → Finance_Users
```

Using groups instead of assigning permissions directly to users follows **enterprise security best practices** and simplifies permission management.

---

### Shared Company Folder

A shared directory was created on the domain controller to simulate a **company file server**.

```
C:\Departments
│
├── Finance
├── HR
└── IT
```

The parent directory was shared across the network to allow domain users to access departmental resources.

Example network path:

```
\\DC1\Departments
```

---

### NTFS Permission Configuration

NTFS permissions were configured to ensure that **only authorized groups can access their department folders**.

Example configuration for the Finance folder:

```
C:\Departments\Finance
```

Permissions assigned:

```
Administrators
SYSTEM
CREATOR OWNER
Finance_Users
```

Finance group permissions:

```
Modify
Read & Execute
List Folder Contents
Read
```

This configuration ensures that only members of the **Finance_Users security group** can modify files in the Finance directory.

---

### Network Drive Mapping with Group Policy

To simulate enterprise resource management, a **Group Policy Object (GPO)** was created to automatically map department network drives for users.

This allows users to access shared resources without manually browsing network paths.

The drive mapping policy was configured using **Group Policy Preferences**.

Path used:

```
User Configuration
→ Preferences
→ Windows Settings
→ Drive Maps
```

Drive mapping configuration:

```
Location: \\DC1\Departments\Finance
Drive Letter: F:
Label: Finance Drive
Action: Create
```

Item-level targeting was configured to ensure that **only members of the Finance_Users security group receive the mapped drive**.

After applying the policy, the client machine updated its policies using:

```
gpupdate /force
```

When Finance users log into the domain workstation, the shared folder automatically appears as a mapped network drive.

Example:

```
F:\ Finance Drive
```

This demonstrates how **Group Policy can centrally manage user resources in an enterprise environment**.

---

### Domain Client Integration

A Windows 10 virtual machine was joined to the domain.

```
Domain: corp.local
```

After joining the domain, users could authenticate using their **domain credentials**.

Example login:

```
CORP\emma
```

This confirms that the **domain authentication system is functioning correctly**.

---

# Password Policy Enforcement

To simulate enterprise security practices, a **domain password policy** was configured using Group Policy.

Password policies allow administrators to enforce secure password standards across all domain users.

The policy was configured in **Group Policy Management** by editing the **Default Domain Policy**.

Configuration path:

```
Computer Configuration
→ Policies
→ Windows Settings
→ Security Settings
→ Account Policies
→ Password Policy
```

Example configuration used in the lab:

```
Minimum password length: 12 characters
Password must meet complexity requirements: Enabled
Maximum password age: 90 days
Minimum password age: 1 day
```

With complexity requirements enabled, passwords must include a combination of:

* Uppercase letters
* Lowercase letters
* Numbers
* Special characters

Example of a valid password:

```
Summer2026!
```

After updating the policy, domain machines were refreshed using:

```
gpupdate /force
```

This demonstrates how **Group Policy can enforce security standards across all domain users in an enterprise environment**.

---

## Key Concepts Demonstrated

This lab demonstrates several fundamental enterprise IT practices:

* Active Directory domain administration
* Organizational Unit management
* User and group administration
* Group-based access control
* NTFS permission configuration
* Network file sharing using SMB
* Domain client integration
* Group Policy configuration
* Network drive mapping

---

## Skills Demonstrated

Active Directory Administration
Windows Server Management
Group Policy Management
Network Drive Mapping
NTFS Permission Configuration
User and Group Administration
Domain Authentication
Enterprise File Sharing
Virtual Lab Infrastructure
Password Policy Enforcement

---

## Possible Improvements

Future improvements to the lab may include:

* Login security banners
* Software deployment via Group Policy
* Security auditing and event logging
* Multiple domain controllers
* Domain trust configuration

---

# Conclusion

This project demonstrates the deployment and administration of a Windows Active Directory domain environment using common enterprise practices. The lab showcases hands-on experience with directory management, group-based permissions, shared network resources, and centralized configuration using Group Policy.

The environment provides a solid foundation for further experimentation with **enterprise network administration, security policies, and domain infrastructure management**.

---
