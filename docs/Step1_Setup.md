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
     - Chose to create a new forest and entered a domain name, `MANIRAJCHAHAL.local`.
  2. **DNS Configuration:**  
     - Accepted the defaults for DNS Server and made sure the DNS server was installed.
  3. **Final Steps & Verification:**  
     - Completed the wizard and rebooted the server.
     - Logged in to confirm the domain controller status.
    
  ### Section 4: Organizational Unit (OU) and Group/User Structure Setup (Graphical Interface)
- **Objective:**  
  Build a detailed Active Directory structure using the Windows Server 2022 graphical interface.
- **Steps Taken:**
  1. **Creating Top-Level Geographic OUs:**
     - Open **Active Directory Users and Computers** from the Tools menu in Server Manager.
     - In the console tree, right-click your domain, then select **New** → **Organizational Unit**.
     - In the dialog box, enter "USA" as the name and click **OK**.
     - Repeat the process to create two additional top-level OUs named "Europe" and "Asia".
  
  2. **Creating Functional OUs Within Each Geographic OU:**
     - For each geographic OU (e.g., USA), expand the OU by clicking the plus sign.
     - Right-click the geographic OU and choose **New** → **Organizational Unit**.
     - Create three OUs within each geographic container named "Users", "Computers", and "Servers".
     - Confirm that each new OU appears under the respective geographic OU.
  
  3. **Setting Up Departmental Groups via the GUI:**
     - Within the appropriate **Users** OU (for example, under USA), right-click and select **New** → **Group**.
     - In the Group dialog box, enter a departmental group name (e.g., "IT - Security") and choose **Global** as the group scope and **Security** as the group type.
     - Click **OK** to create the group.
     - Repeat these steps to create similar groups for HR, Accounting, Admissions, Management, and a group called "All Employees"—ensuring that each department has a corresponding Security group.
     - To create Distribution groups for each department:
       - Again, right-click in the same Users OU, select **New** → **Group**.
       - Enter the department name with an indicator (e.g., "IT - Distribution"), choose **Global** for scope, and select **Distribution** for the group type.
       - Repeat for HR, Accounting, Admissions, and Management.
  
  4. **Adding Users Through the Graphical Interface:**
     - In the appropriate **Users** OU (e.g., under USA), right-click and select **New** → **User**.
     - Complete the New Object – User wizard by entering the first name, last name, and user logon name.
     - Set a temporary password, and choose the configuration option such as changing password on first log-in.
     - Click **Next** and then **Finish**.
     - Repeat this process to create as many sample user accounts for each department.
  
  5. **Adding All Users to the 'All Employees' Group:**
     - Open the properties for each user account (by right-clicking the user and selecting **Properties**).
     - Navigate to the **Member Of** tab and click **Add**.
     - In the dialog box, type the name of the "All Employees" Security group, then click **Check Names** to confirm and **OK**.
     - Repeat for each user to ensure that every account is a member of the "All Employees" group.
