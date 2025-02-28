# Tutorial: Joining Your Fresh Laptop to the Domain

This guide walks you through connecting a new Windows 10 laptop to the domain set up on your domain controller. Follow these steps to join the domain and log in with your domain credentials.

## Prerequisites

- A laptop running Windows 10.
- Network connectivity to your domain controller.
- The domain name (e.g., `SERVER.local`).

**Important for the Domain Controller:**
Before joining any clients, ensure that your domain controller is configured with a static IP:
- Use the DHCP-assigned IP as the static IP address, along with its corresponding subnet mask and default gateway.
- Set the **Preferred DNS Server** to the loopback address (127.0.0.1).
- Set the **Alternate DNS Server** to Google's DNS server (8.8.8.8).

## Step 1: Configuring Static IP and DNS Settings on the Domain Controller

1. **Log in to the Domain Controller:**
   - Ensure you are logged into your Windows Server 2022 that acts as the domain controller.

2. **Open Network Connections:**
   - Open the **Control Panel**.
   - Navigate to **Network and Internet** > **Network and Sharing Center**.
   - Click on **Change adapter settings** on the left side.

3. **Access the Properties of the Active Network Adapter:**
   - Right-click the active network adapter (e.g., Ethernet) and select **Properties**.

4. **Configure IPv4 Settings:**
   - In the list, select **Internet Protocol Version 4 (TCP/IPv4)** and click **Properties**.
   - Choose **Use the following IP address:**
     - **IP address:** Enter the current DHCP-assigned IP address.
     - **Subnet mask:** Enter the appropriate subnet mask (as provided by your DHCP).
     - **Default gateway:** Enter the default gateway.
   - Under **Use the following DNS server addresses:**
     - **Preferred DNS server:** Enter `127.0.0.1` (the loopback address).
     - **Alternate DNS server:** Enter `8.8.8.8`.
   - Click **OK** to apply the settings, and then close out of the network adapter properties.

5. **Verify Configuration:**
   - Open a Command Prompt and run `ipconfig /all` to confirm that the static IP and DNS settings have been applied correctly.

## Step 2: Connect the Laptop to the Network
- Ensure that your laptop is connected to the same network as your domain controller (via Ethernet or Wi-Fi).

## Step 3: Configure DNS Settings on the Laptop (if necessary)
- Open **Settings** > **Network & Internet**.
- Select **Change adapter options**.
- Right-click your active network connection and choose **Properties**.
- Select **Internet Protocol Version 4 (TCP/IPv4)** and click **Properties**.
- Under **Use the DNS server addresses that was set as the servers IP**, enter the IP address of your domain controller.
- Click **OK** to save the settings.

## Step 4: Join the Domain
1. **Open System Properties:**
   - Right-click **This PC** on the desktop and select **Properties**, then scroll down and click **Rename this PC (Advanced)**.
2. **Change Computer Name/Domain:**
   - In **Computer Name** tab click **Change…**.
3. **Enter Domain Information:**
   - Under **Member of**, select **Domain** and enter your domain name (e.g., `SERVER.local`).
   - Click **OK**.
4. **Enter Credentials:**
   - When prompted, enter the username and password of an account that has permission to join the domain.
   - Click **OK**.
5. **Restart the Laptop:**
   - After receiving a confirmation message, restart your laptop to apply the changes.

## Step 5: Log in with Domain Credentials
- At the login screen after restarting:
  - Click **Other user**.
  - Enter your domain username in the format `DOMAIN\username` (e.g., `SERVER\mchahal`) and your password.
  - Log in to access your domain account.

## Final Notes
Once joined, the laptop will receive any Group Policy settings configured for your domain, such as drive mappings and security settings, ensuring a consistent configuration across your environment.
