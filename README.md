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
 
 <img width="951" height="1103" alt="Screenshot 2025-09-24 113242" src="https://github.com/user-attachments/assets/22a44e41-f67e-43c1-aaf3-8ea479998071" />
 <img width="939" height="368" alt="Screenshot 2025-09-24 113251" src="https://github.com/user-attachments/assets/a1c0595d-bd96-40f0-863f-3301a1c9b57c" />
 

Additionally, we utilized GPOs for centralized software deployment, ensuring that essential applications are automatically installed on client machines without user intervention. We also enforced a strong password policy and manually configured inbound firewall rules to block incoming requests for crucial services such as SSH and RDP.

### Centralized Software Deployment

We utilized Group Policy to automate the deployment of essential software to client machines. This method ensures that applications are installed automatically and silently on target computers without the need for manual intervention from an administrator.

For this project, we:
- Deployed `7-Zip` by linking its installer file (`.msi`) to the GPO.
- Prevented standard users from installing their own software by disabling the use of removable media sources for any installation.

To automatically deploy software to multiple computers, we utilized Group Policy Objects (GPOs) to push application installers directly to the target machines. This process ensures that software is installed consistently and without manual intervention.

To begin, we created a dedicated folder within the SYSVOL shared folder on the domain controller. This is the recommended location for GPO-related files because its contents are automatically replicated across all domain controllers and are accessible to all domain computers via a standard UNC path. Then, 

<img width="669" height="46" alt="Screenshot 2025-09-24 103709" src="https://github.com/user-attachments/assets/f7823d7b-6115-4686-8e9a-d5a31dca5b14" />

<img width="164" height="49" alt="Screenshot 2025-09-24 213207" src="https://github.com/user-attachments/assets/bd2075ce-34af-4dcb-97aa-e4ea14d4e1d0" />

Then we configured the sharing and NTFS permissions for domain computers to ensure that client machines could access the shared folder that contains the .msi binary file.

<img width="479" height="596" alt="Screenshot 2025-09-24 105247" src="https://github.com/user-attachments/assets/a82c1ea5-4777-4792-97e4-1f7092be6336" />

<img width="473" height="595" alt="Screenshot 2025-09-24 105316" src="https://github.com/user-attachments/assets/259a5aff-6a06-454f-b8bd-50d9dfffb727" />


When configuring the software deployment policy, we selected the .msi file by referencing its UNC path (e.g., \\corp.com\SYSVOL\corp.com\Policies\Software\7-Zip.msi). This path ensures that the client computers can locate the installer on the network during the policy application process.


<img width="933" height="296" alt="Screenshot 2025-09-24 125434" src="https://github.com/user-attachments/assets/58020b06-abab-4b01-93ff-04b077a7e424" />

## Repository Structure

```
/AD-DC-Group-policy-objects/
├── README.md 
├── LICENSE
├── /screenshots/
├── /gpo-backups/
```

## Author
[nachogtan](https://github.com/nachogtan)
