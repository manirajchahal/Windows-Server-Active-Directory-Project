# Step 3: File Services and NTFS Permissions Setup

## Overview

In this step, we focus on setting up file services to manage and secure shared folders in a Windows Server 2022 environment. The guide covers:

- Creating shared folders and configuring NTFS permissions to control access by users and groups.
- Differentiating between mapped drives and network drives, along with configuration methods.
- Installing File Server Resource Manager (FSRM) and using it to set up quotas and file screens to enforce storage limits and file type restrictions.

### Section 1: Installing File Services and File Server Resource Manager (FSRM)
- **Objective:**  
  Ensure that the file services role and FSRM are installed to manage file shares, quotas, and file screens.
- **Steps Taken:**
  1. **Open Server Manager:**  
     - Launch **Server Manager** from the Start menu.
  2. **Add Roles and Features:**  
     - Click **Add Roles and Features**.
     - In the wizard, select **Role-based or feature-based installation**.
     - Choose the local server.
  3. **Select File and Storage Services:**  
     - Under **Roles**, expand **File and Storage Services**.
     - Check **File Server** to install the core file sharing components.
  4. **Install File Server Resource Manager:**  
     - Under **Features**, locate and select **File Server Resource Manager**.
     - Complete the wizard and allow the installation to finish.
  5. **Verification:**  
     - After installation, verify that FSRM appears in Server Manager under **Tools**.

### Section 2: Creating Shared Folders and Configuring NTFS Permissions
- **Objective:**  
  Create shared folders and set appropriate NTFS permissions to control access.
- **Steps Taken:**
  1. **Create a Shared Folder:**  
     - Open **File Explorer** on the server.
     - Navigate to the drive where you want to create the share (e.g., C:\).
     - Right-click in an empty area, select **New** → **Folder**, and name it (e.g., "SharedFolder").
  2. **Share the Folder:**  
     - Right-click the newly created folder and select **Properties**.
     - Go to the **Sharing** tab and click **Advanced Sharing…**.
     - Check **Share this folder**, then click **Permissions**.
  3. **Configure Share Permissions:**  
     - In the **Permissions** dialog, remove the default permissions if necessary.
     - Click **Add…** and enter the names of the users or groups you want to grant access (e.g., "IT - Security", "HR - Security", etc.).
     - Set the appropriate permissions (Read, Change, Full Control) for each group.
     - Click **OK** to confirm.
  4. **Set NTFS Permissions:**  
     - Switch to the **Security** tab in the folder properties.
     - Click **Edit…** to change NTFS permissions.
     - Adjust the permissions for each user or group to further restrict or allow access. For example:
       - Grant **Full Control** for administrative groups.
       - Allow **Modify** or **Read & Execute** for other department groups based on their roles.
     - Click **Apply** and then **OK** to save changes.
  5. **Testing Access:**  
     - Test from a client machine logged in on a user account connected to the domain to verify that permissions are applied correctly.

### Section 3: Configuring Mapped Drives vs. Network Drives
- **Objective:**  
  Explain and set up two types of drive access: mapped drives and network drives.
- **Steps Taken:**
  1. **Mapped Drives:**  
     - **Definition:** Mapped drives are drive letters assigned to shared folders, making them appear as local drives.
     - **Configuration:**  
       - On a client computer, open **File Explorer**.
       - Right-click on **This PC** and select **Map network drive…**.
       - Choose a drive letter (e.g., S:) and enter the shared folder path (e.g., `\\ServerName\SharedFolder`).
       - Check **Reconnect at sign-in** if desired, and click **Finish**.
  2. **Network Drives** Automatically assign network drives to users so that they persist across logons, using Group Policy Preferences.
- **Steps Taken:**
  1. **Open Group Policy Management Console (GPMC):**  
     - Launch **Server Manager**.
     - Click on **Tools** and select **Group Policy Management**.
  2. **Create a New Group Policy Object (GPO):**  
     - In the GPMC, right-click on the domain or an appropriate Organizational Unit (OU) where the policy should apply.
     - Select **"Create a GPO in this domain, and Link it here…"**.
     - Enter a descriptive name for the GPO (e.g., "Network Drive Mapping").
  3. **Edit the GPO to Configure Drive Maps:**  
     - Right-click the newly created GPO and select **Edit**.
     - In the Group Policy Management Editor, navigate to:
       - **User Configuration → Preferences → Windows Settings → Drive Maps**
  4. **Create a New Drive Mapping:**  
     - Right-click in the right-hand pane (the empty area) and choose **New → Mapped Drive**.
     - In the **New Drive Properties** dialog, configure the following:
       - **Action:** Set to **Create**.
       - **Location:** Enter the UNC path to the shared folder (e.g., `\\ServerName\SharedFolder`).
       - **Drive Letter:** Choose a drive letter (e.g., S:).
       - **Label as:** Optionally, provide a name for the drive (e.g., "Shared Folder").
       - **Reconnect:** Ensure the option is selected so that the drive mapping persists after a restart.
     - Click **OK** to save the drive mapping.
  5. **Apply and Test the Policy:**  
     - Close the editor and force a Group Policy update on a client machine (e.g., by running `gpupdate /force` via the Command Prompt).
     - Verify that the network drive appears automatically in **File Explorer** under the specified drive letter.
  

### Section 4: Setting Up Quotas and File Screens Using FSRM
- **Objective:**  
  Utilize File Server Resource Manager to manage storage by setting quotas and file screens.
- **Steps Taken:**
  1. **Launching FSRM:**  
     - Open **Server Manager**.
     - From the **Tools** menu, select **File Server Resource Manager**.
  2. **Creating a Quota:**  
     - In the FSRM console, expand **Quota Management**.
     - Right-click **Quotas** and choose **Create Quota…**.
     - In the **Create Quota** wizard:
       - Specify the path to the shared folder (e.g., `C:\SharedFolder`).
       - Choose to either create a new quota template or use an existing one.
       - Set the quota limit (e.g., 10GB) and configure how the quota should be enforced (hard limit or soft limit with warning notifications).
       - Complete the wizard and review the summary.
  3. **Setting Up File Screens:**  
     - In the FSRM console, expand **File Screening Management**.
     - Right-click **File Screens** and choose **Create File Screen…**.
     - In the wizard:
       - Select the path where the file screen will be applied (e.g., the same shared folder).
       - Choose to either create a new file screen template or use an existing one.
       - Configure file screening options to block certain file types (e.g., restrict executable files in document folders).
       - Complete the wizard and verify that the file screen appears in the FSRM console.
  4. **Testing and Verification:**  
     - Test the quota by attempting to copy files until the quota limit is reached, confirming that appropriate warnings or restrictions are enforced.
     - Attempt to save a file type that is blocked by the file screen to verify that it is prevented.
