# Setting Up a Local NAS Using MeLE Quieter3C Fanless Mini PC with Windows 11

## Introduction
This guide provides step-by-step instructions on setting up a local NAS (Network-Attached Storage) using the **MeLE Quieter3C Fanless Mini PC** running Windows 11. This NAS will allow you to share files across your local network securely using the **SMB 2.0 protocol**.

## Hardware Requirements
- MeLE Quieter3C Fanless Mini PC with Windows 11 installed
- External storage (USB hard drive, SSD, or NAS-grade external HDD)
- Ethernet cable (recommended for stable connection)
- Router with local network access

## Setting Up Network Connection with an Ethernet Cable
For better network stability and speed, it is recommended to use an Ethernet cable instead of WiFi.

1. Plug one end of the Ethernet cable into the **RJ45 Ethernet port** on the MeLE Quieter3C Mini PC.
2. Connect the other end of the Ethernet cable to an available **LAN port** on your router.
3. Ensure the router is powered on and functioning correctly.
4. Windows should automatically detect the wired connection. You can check the network status by:
   - Clicking on the **Network icon** in the taskbar.
   - Navigating to **Settings > Network & Internet > Ethernet** to confirm connectivity.
5. If the connection does not work, restart both the Mini PC and the router.

## Setting Up File Sharing on Windows 11

### Step 1: Connect and Prepare External Storage
1. Plug in your USB storage device.
2. Open **File Explorer** (`Win + E`), right-click the drive, and select **Properties**.
3. Navigate to the **Sharing** tab and click **Advanced Sharing**.
4. Check **Share this folder**, then click **Permissions**.
5. Add specific users or select **"Everyone"** for open access (recommended for home networks).
6. Click **OK**, then **Apply**, and close the window.

### Step 2: Configure Network and Sharing Settings
1. Open **Control Panel** and navigate to **Network and Sharing Center**.
2. Click **Change advanced sharing settings**.
3. Under the **Private (current profile)** section, enable:
   - ✅ Turn on **network discovery**
   - ✅ Turn on **file and printer sharing**
4. Under **All Networks**:
   - ⛔ **Turn off password-protected sharing** (optional, for easier access on a home network).
   - ✅ Ensure **Public folder sharing** is enabled.

## Disabling SMB 1.0 and Enabling SMB 2.0
To ensure security, we will **disable SMB 1.0** and **enable SMB 2.0**.

### Step 1: Disable SMB 1.0
1. Open **Control Panel** and navigate to **Programs > Turn Windows features on or off**.
2. Scroll down and **uncheck** `SMB 1.0/CIFS File Sharing Support`.
3. Click **OK** and restart your PC.


### Step 2: Ensure SMB 2.0 is Enabled
1. Open **PowerShell as Administrator** (`Win + X` → Select **Windows Terminal (Admin)**).
2. Run the following command to check SMB 2.0 status:
   ```powershell
   Get-SmbServerConfiguration | Select EnableSMB2Protocol

3. If it's disabled, enable it by running:
4. ```powershell
   Set-SmbServerConfiguration -EnableSMB2Protocol $true -Force

5. Restart your PC to apply changes.

## Mapping the NAS Drive on Other Devices
To access the shared folder from another PC:

1. Open File Explorer on the client PC.
2. In the address bar, type \\<Your MeLE Quieter3C IP>\<Shared Folder Name>.
3. Press Enter to access the folder.
4. To map the drive permanently, right-click on the shared folder, select Map network drive, choose a drive letter, and click Finish.

## Conclusion
Your MeLE Quieter3C Mini PC is now a functioning NAS, allowing you to store and share files securely across your network with SMB 2.0 enabled. With Tailscale, you can securely access your NAS remotely without exposing it to the open internet. Regularly update your system and backups to maintain security and data integrity.


Troubleshooting Tips:
If you cannot access the shared folder, check the Windows Firewall settings to allow File and Printer Sharing.
Use ipconfig in Command Prompt to find your PC’s IP address (IPv4 Address).

