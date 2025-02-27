# Episode 1: Home Lab Setup & Initial Active Directory Installation

## Overview

In this first section, I installed Windows Server 2022 and install Active Directory Domain Services (AD DS).

### Section 1: Home Lab Overview & Requirements
- **Objective:**  
  Establish the foundation of my server.
- **Steps Taken:**
  1. **Hardware & Virtualization Software:**  
      - Installed Windows Server 2022 .iso file.
      - Imaged a spare Lenovo ThinkPad T490 with Windows Server 2022 .iso.
  2. **Lab Planning:**  
     - Used a Laptop with Intel i5-8365U CPU and 24 GB of RAM.
     - Used my Desktop PC to be able to simulate user accounts via VMWare Workstation.
     
  3. **Documentation:**  
     - Documented all steps and progress on GitHub.

### Section 2: Windows Server Installation & Role Assignment
- **Objective:**  
  Install the Windows Server OS on my Laptops HDD and prepare it for AD DS.
- **Steps Taken:**
  1. **Creating the Windows Server:** 
     - Created a Windows Server 2022 USB using Rufus to flash the USB.
     - Booted Laptop from USB.
  2. **Windows Server Installation:**  
     - Followed the installation wizard.
     - Configured basic settings such as hostname.
  3. **Initial Configuration:**  
     - Installed updates and drivers.
     - Ensured network connectivity.
  4. **Adding the AD DS Role:**  
     - Opened **Server Manager**.
     - Navigated to **Add Roles and Features**, selected **Active Directory Domain Services**, **DNS Server**, and **Remote Desktop Services**.
     - Followed the wizard, reviewing prerequisites and letting the server install required features.
  5. **Post-Installation Checks:**  
     - Verified that AD DS installation completed without errors.
     - Reviewed event logs for any warnings.

### Section 3: Initial Active Directory Configuration
- **Objective:**  
  Configure AD DS by creating a new domain and promoting the server as a domain controller.
- **Steps Taken:**
  1. **Promoting the Server:**
     - In Server Manager, clicked the notification flag and selected **Promote this server to a domain controller**.
     - Chose to create a new forest and entered a domain name (e.g., `homelab.local`).
  2. **Configuration Options:**  
     - Set the **Forest** and **Domain functional levels**.
     - Provided a Directory Services Restore Mode (DSRM) password.
  3. **DNS Configuration:**  
     - Accepted the defaults for DNS delegation (if any) and ensured the DNS server was installed.
  4. **Final Steps & Verification:**  
     - Completed the wizard and rebooted the server.
     - Logged in to confirm the domain controller status.
     - Ran `dcdiag` and checked event logs to ensure the configuration was successful.
