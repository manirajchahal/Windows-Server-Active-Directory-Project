# Step 2: Domain Management & Group Policy Setup

## Overview

In this step, the focus is on centralizing control of your Active Directory environment by creating and configuring Group Policy Objects (GPOs) using the Group Policy Management Console (GPMC). This guide outlines each step taken to establish policies that enforce security settings, desktop configurations, and other operational standards across the domain.

### Section 1: Accessing the Group Policy Management Console (GPMC)
- **Objective:**  
  Open and familiarize yourself with the GPMC to manage GPOs effectively.
- **Steps Taken:**
  1. **Launching GPMC:**  
     - Open **Server Manager**.
     - Click on **Tools** in the upper-right corner.
     - Select **Group Policy Management** from the dropdown menu.
  2. **Navigating the Console:**  
     - In the GPMC window, expand the domain to view the organizational units and existing policy objects.
     - Familiarize yourself with the structure: the left pane shows the domain hierarchy, while the right pane displays linked GPOs and their settings.

### Section 2: Creating a New Group Policy Object (GPO)
- **Objective:**  
  Create a new GPO to enforce specific configurations across the domain or a particular OU.
- **Steps Taken:**
  1. **Initiating GPO Creation:**  
     - In the GPMC left pane, right-click on the domain or the desired OU where you want to apply the policy.
     - Select **"Create a GPO in this domain, and Link it here..."** from the context menu.
  2. **Naming the GPO:**  
     - In the dialog box that appears, enter a descriptive name (e.g., "Password Policy Enforcement" or "Desktop Configuration Policy").
     - Click **OK** to create the GPO.
  3. **Verifying GPO Creation:**  
     - Confirm that the new GPO appears in the list under the chosen domain or OU.

### Section 3: Editing the GPO to Configure Settings
- **Objective:**  
  Define policy settings that enforce security and operational standards across the target computers.
- **Steps Taken:**
  1. **Opening the GPO Editor:**  
     - Right-click the newly created GPO and select **"Edit"**. This launches the Group Policy Management Editor.
  2. **Configuring Security Settings:**  
     - Navigate to **Computer Configuration** → **Policies** → **Windows Settings** → **Security Settings**.
     - Configure settings such as:
       - **Account Policies:** Set password length, complexity requirements, and account lockout policies.
       - **Local Policies:** Adjust audit policy settings to track security events.
  3. **Configuring User Environment Settings:**  
     - Under **User Configuration** → **Policies** → **Administrative Templates**, configure settings such as:
       - **Desktop and Start Menu Options:** Enforce a specific desktop background or limit user customization.
       - **Control Panel Settings:** Restrict access to certain control panel features.
  4. **Documentation During Configuration:**  
     - For each setting changed, document the reasoning and the expected outcome. This may include noting security requirements or organizational standards.
  5. **Saving the Configuration:**  
     - Once all desired settings are configured, apply changes, and close the editor to save the changes.

### Section 4: Linking, Testing, and Verifying the GPO
- **Objective:**  
  Ensure the GPO is applied correctly across the domain and test its impact.
- **Steps Taken:**
  1. **Linking the GPO (If Not Already Linked):**  
     - If you created the GPO at the domain level, it is automatically linked. If created in isolation, right-click the target OU, choose **"Link an Existing GPO..."**, and select your new GPO.
  2. **Forcing a Policy Update:**  
     - On a client machine or within a test virtual machine, run the **gpupdate /force** command via the  **Command Prompt** to force a refresh.
  3. **Verifying Policy Application:**  
     - Open **Command Prompt** on a client and run `gpresult /r` to see if the new GPO settings are applied.
  4. **Review and Documentation:**  
     - Verify that the settings (e.g., password policy or desktop restrictions) have been implemented as configured.
     - Document any observations or necessary adjustments for future troubleshooting.
