---
layout: page
title: Create the OPNsense Virtual Machine
permalink: /security-onion-series/security-onion-create-opnsense
nav_order: 13
parent: "Security Onion Virtual Lab Tutorial: Introduction"
---

# Create the OPNsense Virtual Machine

1. For this tutorial, I will create my virtual machines (VMs) in a folder called **localLab**. Click the plus icon in the top-left corner of VMware Fusion and select **Folder**.
   ![03-opn-sense-vm-creation-001.png](./images/03-opn-sense-vm-creation/03-opn-sense-vm-creation-001.png)
2. Enter the folder name (**localLab**) and press `Enter`.
   ![03-opn-sense-vm-creation-002.png](./images/03-opn-sense-vm-creation/03-opn-sense-vm-creation-002.png)
3. Click the plus icon and select **New...**.
   ![03-opn-sense-vm-creation-003.png](./images/03-opn-sense-vm-creation/03-opn-sense-vm-creation-003.png)
4. Select **Create a custom virtual machine**, then click **Continue**.
   ![03-opn-sense-vm-creation-004.png](./images/03-opn-sense-vm-creation/03-opn-sense-vm-creation-004.png)
5. In the **Choose Operating System** dialog, select **Other**, then select **FreeBSD 12 64-bit** and click **Continue**.
   ![03-opn-sense-vm-creation-005.png](./images/03-opn-sense-vm-creation/03-opn-sense-vm-creation-005.png)
6. In the **Choose Firmware Type** dialog you can leave the default of **Legacy BIOS**, but OPNsense's amd64 architecture supports UEFI, so I am selecting that. Click **Continue**.
   ![03-opn-sense-vm-creation-006.png](./images/03-opn-sense-vm-creation/03-opn-sense-vm-creation-006.png)
7. In the **Choose a Virtual Disk** dialog, leave the radio button set to **Create a new virtual disk** and click **Continue**.
   ![03-opn-sense-vm-creation-007.png](./images/03-opn-sense-vm-creation/03-opn-sense-vm-creation-007.png)
8. On the **Finish** dialog, click **Customize Settings**.
   ![03-opn-sense-vm-creation-008.png](./images/03-opn-sense-vm-creation/03-opn-sense-vm-creation-008.png)
9. Change the name of the virtual machine file to something that indicates what it is (such as `OPNsense-2022`) and click **Save** to save it with your other VMware Fusion virtual machines.
   ![03-opn-sense-vm-creation-009.png](./images/03-opn-sense-vm-creation/03-opn-sense-vm-creation-009.png)
10. A window for the VM itself and its **Settings** window should open. If the **Settings** window does not open, open it with `Command + E` or click the wrench icon that displays at the top of the window.
   ![03-opn-sense-vm-creation-010.png](./images/03-opn-sense-vm-creation/03-opn-sense-vm-creation-010.png)
11. Click **Startup Disk**.
   ![03-opn-sense-vm-creation-011.png](./images/03-opn-sense-vm-creation/03-opn-sense-vm-creation-011.png)
12. Select **CD/DVD**. This means that when the VM starts, it will use the installation media in the virtual CD/DVD drive. Click **Show All**.
   ![03-opn-sense-vm-creation-012.png](./images/03-opn-sense-vm-creation/03-opn-sense-vm-creation-012.png)
13. Click **CD/DVD (IDE)**.
   ![03-opn-sense-vm-creation-013.png](./images/03-opn-sense-vm-creation/03-opn-sense-vm-creation-013.png)
14. Click the drop-down menu and select **Choose a disc or disc image**.
   ![03-opn-sense-vm-creation-014.png](./images/03-opn-sense-vm-creation/03-opn-sense-vm-creation-014.png)
15. Navigate to your unzipped OPNsense ISO file in the **isos** directory, select it so that the VM will boot from it, and click **Open**.
   ![03-opn-sense-vm-creation-015.png](./images/03-opn-sense-vm-creation/03-opn-sense-vm-creation-015.png)
16. Make sure **Connect CD/DVD Drive** is selected and click **Show All**.
   ![03-opn-sense-vm-creation-016.png](./images/03-opn-sense-vm-creation/03-opn-sense-vm-creation-016.png)
17. Click **Network Adapter**.
   ![03-opn-sense-vm-creation-017.png](./images/03-opn-sense-vm-creation/03-opn-sense-vm-creation-017.png)
18. Select **Bridged Networking** > **Autodetect** so that your OPNsense VM can connect to the internet through the host operating system's internet connection.
   ![03-opn-sense-vm-creation-018.png](./images/03-opn-sense-vm-creation/03-opn-sense-vm-creation-018.png)
19. Click **Add Device...**.
   ![03-opn-sense-vm-creation-019.png](./images/03-opn-sense-vm-creation/03-opn-sense-vm-creation-019.png)
20. Click **Network Adapter** and click **Add...**.
   ![03-opn-sense-vm-creation-020.png](./images/03-opn-sense-vm-creation/03-opn-sense-vm-creation-020.png)
21. A dialog for **Network Adapter 2** displays. Under **Custom**, select **EXTERNAL_NET_LAN**, then click **Add Device...**.
   ![03-opn-sense-vm-creation-021.png](./images/03-opn-sense-vm-creation/03-opn-sense-vm-creation-021.png)

    * **Note:** **EXTERNAL_NET_LAN** is the network you will access OPNsense's web interface for management, and also use Kali to send malicious traffic to **HOME_NET_LAN**.

22. Add a third network adapter by clicking **Network Adapter**, then **Add...**.
   ![03-opn-sense-vm-creation-020.png](./images/03-opn-sense-vm-creation/03-opn-sense-vm-creation-020.png)
23. A dialog for **Network Adapter 3** displays. Under **Custom**, select **HOME_NET_LAN**, click **Add Device...**, then click **Show All**.
   ![03-opn-sense-vm-creation-022.png](./images/03-opn-sense-vm-creation/03-opn-sense-vm-creation-022.png)

    * **Note:** **HOME_NET_LAN** is the network where you will deploy Security Onion.

24. Click **Processors & Memory**.
   ![03-opn-sense-vm-creation-023.png](./images/03-opn-sense-vm-creation/03-opn-sense-vm-creation-023.png)
25. Because this is a small virtual network on the host Mac and we will have only a few VMs and not a lot of traffic, you can use less processing power for the OPNsense router. (You will need it for the other VMs.) Click **Processors** and select **2 processor cores**.
   ![03-opn-sense-vm-creation-024.png](./images/03-opn-sense-vm-creation/03-opn-sense-vm-creation-024.png)
26. Change the **Memory** to **1024**.
   ![03-opn-sense-vm-creation-025.png](./images/03-opn-sense-vm-creation/03-opn-sense-vm-creation-025.png)
27. You are done configuring your OPNsense VM. You can close the **Settings** window. In the window for the VM itself (the window will be labeled with what you named the VM when you saved it), click the icon next to the playhead in the top-left corner of the window. (If you hover over the icon, it will display the text **Manage this virtual machine's snapshots**.
   ![03-opn-sense-vm-creation-026.png](./images/03-opn-sense-vm-creation/03-opn-sense-vm-creation-026.png)
28. In the **Snapshots** window, click the camera icon towards the top-left corner.
   ![03-opn-sense-vm-creation-027.png](./images/03-opn-sense-vm-creation/03-opn-sense-vm-creation-027.png)
29. Give your snapshot a name and description (for example, **v0_pre_boot**) and click **Take**. A snapshot allows you to roll back to the VM's state at the time of the snapshot. If anything goes wrong, you can roll back to this snapshot and start over but still skip the above steps.
   ![03-opn-sense-vm-creation-028.png](./images/03-opn-sense-vm-creation/03-opn-sense-vm-creation-028.png)
30. When you are done you can close the **Snapshots** window.
   ![03-opn-sense-vm-creation-029.png](./images/03-opn-sense-vm-creation/03-opn-sense-vm-creation-029.png)
31. In your Virtual Machine library, select your OPNsense VM and drag it into the **localLab** folder.
   ![03-opn-sense-vm-creation-030.png](./images/03-opn-sense-vm-creation/03-opn-sense-vm-creation-030.png)

You are ready to boot your OPNsense router VM and configure it to handle the traffic for your local lab.