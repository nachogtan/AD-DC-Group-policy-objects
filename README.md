![petr-magera-Ugnm0F4e00U-unsplash](https://github.com/user-attachments/assets/16ff9ec4-6f15-49c2-a5df-e9a80d50bb4a)

# AD-DC-Group-policy-objects
This project demonstrates the proper administration of policies and configurations for objects within a Windows Server domain controller.

---
## Contents
* [Project Goals](#project-goals)
* [Requirements](#requirements)
* [GPO Implementation](#gpo-implementation)
* [Repository Structure](#repository-structure)
* [Author](#author)

---

## Project Goals

Active Directory is a cornerstone for efficient user and device management in enterprise environments. For a sys admin, it's crucial to understand how to quickly and efficiently deploy and enforce policies on endpoints, ensuring best security practices are followed.

This project focuses on demonstrating the process of creating and implementing Group Policy Objects (GPOs) to manage configurations and apply policies to specific organizational units and objects within a domain.

## Requirements

- Virtualization Software: A hypervisor like Oracle VirtualBox or VMware Workstation.
- Domain Controller: A virtual machine running Windows Server 2022 (or 2019+). This will act as the primary domain controller and host for Active Directory.
- Client Machine: A virtual machine running a client OS, such as Windows 10 or Windows 11, joined to the domain.
- Software: An .msi package for centralized software deployment

## GPO Implementation

In alignment with the Principle of Least Privilege, we ensure that users have only the minimum permissions necessary to perform their tasks. Using Group Policy Objects (GPOs), we can centrally assign permissions and enforce security policies across different objects within the domain,  as well as control the appearance and configurations of the user environment.

For this project, we configured a GPO to block key actions that could compromise system security. This includes:

### Security Policies

- Administrative Templates:
  - Remove Add or Remove Programs
  - Prevent changing desktop background
  - Hide "Installed Updates" page
  - Hide "Programs and Features" page
  - Hide "Windows Features"
  - Hide the Programs Control Panel
  - Hide "Installed Updates" page
  - Hide "Programs and Features" page
  - Hide "Windows Features"
  - Hide the Programs Control Panel
  - Prohibit User from manually redirecting Profile Folders
  - Don't run specified Windows applications
    - powershell.exe
    - mmc.exe
    - cmd.exe
    - regedit.exe
  - Disallow changing of geographic location
  - Prompt for password on resume from hibernate/suspend
  - All Removable Storage classes: Deny all access
  - Do not display the password reveal button
  - Prevent removable media source for any installation
  - Turn on PowerShell Transcription
    
Additionally, we utilized GPOs for centralized software deployment, ensuring that essential applications are automatically installed on client machines without user intervention. We also enforced a strong password policy and manually configured inbound firewall rules to block incoming requests for crucial services such as SSH and RDP.

### Centralized Software Deployment

We utilized Group Policy to automate the deployment of essential software to client machines. This method ensures that applications are installed automatically and silently on target computers without the need for manual intervention from an administrator.

For this project, we:
- Deployed `7-Zip` by linking its installer file (`.msi`) to the GPO.
- Prevented standard users from installing their own software by disabling the use of removable media sources for any installation.

## Repository Structure


## Author
