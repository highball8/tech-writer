---
layout: page
title: "Create the Security Onion Virtual Machine"
nav_order: 15
parent: "Security Onion: Creating a Virtual Lab Environment—Windows 11, 2026"
---

# Create the Security Onion Virtual Machine

Now it's time to create the Security Onion virtual machine (VM).

{: .note}
> As I mentioned in the introduction, Security Onion is very resource intensive, particularly for RAM/memory. Review their [Minimum Specs for hardware](https://docs.securityonion.net/en/3/main/hardware/#minimum-specs){:target="_blank"}. 
> In this tutorial series, I am going to deploy a **Standalone** instance of Security Onion using:
> * 8 CPU cores (4 recommended)
> * 24GB of RAM
> * 200GB of disk storage
> * 2 network interface cards

1. In VMware Workstation Pro, click the **File** menu and then click **New Virtual Machine**.
   ![](/assets/images/security-onion-images-win11-2026/05-onion-vm-creation-win11-2026/05-onion-vm-creation-win11-2026-001.png)
2. When the **New Virtual Machine Wizard** opens, leave the **Typical (recommended)** radio button selected and click **Next**.
   ![](/assets/images/security-onion-images-win11-2026/05-onion-vm-creation-win11-2026/05-onion-vm-creation-win11-2026-002.png)
3. On the **Guest Operating System Installation** screen, select **Installer from disk image (iso)** and click **Browse** underneath it.
   ![](/assets/images/security-onion-images-win11-2026/05-onion-vm-creation-win11-2026/05-onion-vm-creation-win11-2026-003.png)
4. In the **Browse for ISO Image** dialog, navigate to the Security Onion ISO that you downloaded earlier, select it, and click **Open**.
   ![](/assets/images/security-onion-images-win11-2026/05-onion-vm-creation-win11-2026/05-onion-vm-creation-win11-2026-004.png)
5. VMware will detect the operating system type based on the ISO. Click **Next**.
   ![](/assets/images/security-onion-images-win11-2026/05-onion-vm-creation-win11-2026/05-onion-vm-creation-win11-2026-005.png)
6. On the **Name the Virtual Machine** screen, enter a name for the OPNsense VM. I named mine **onion2026**. Then click the **Browse** button to select the location where the VM and its files will be saved to and stored.
   ![](/assets/images/security-onion-images-win11-2026/05-onion-vm-creation-win11-2026/05-onion-vm-creation-win11-2026-006.png)
7. Select the folder where VMware stores the collection of files and other data that make up the virtual machine. I have created a folder on my local drive called **onion-virtual-machines**. Within that, I created a new folder and gave it the same name as the VM, **onion2026**. Navigate to the location where you want the VM stored and click **OK**. 
   ![](/assets/images/security-onion-images-win11-2026/05-onion-vm-creation-win11-2026/05-onion-vm-creation-win11-2026-007.png)
8. Click **Next**.\\
   ![](/assets/images/security-onion-images-win11-2026/05-onion-vm-creation-win11-2026/05-onion-vm-creation-win11-2026-008.png)
9. On the **Specify Disk Capacity** screen, increase the default **Maximum disk size (GB)** from 20GB to **200GB**, which is the recommended disk size for Security Onion, which produces a lot of log data. Leave the **Split virtual disk into multiple files** radio button selected and click **Next**. 

      {: .note}
      As of Security Onion version 3.1.0 in mid-2026, the [recommended storage/disk size](https://docs.securityonion.net/en/3/main/hardware/#minimum-specs){:target="_blank"} for a Standalone Security Onion deployment is 200 GB.

      ![](/assets/images/security-onion-images-win11-2026/05-onion-vm-creation-win11-2026/05-onion-vm-creation-win11-2026-009.png)

10. The **Ready to Create Virtual Machine** screen displays a summary of the VM's properties. Click **Customize Hardware**.\\
    ![](/assets/images/security-onion-images-win11-2026/05-onion-vm-creation-win11-2026/05-onion-vm-creation-win11-2026-010.png)
11. The **Hardware** dialog opens. Click **Memory**. Security Onion needs a lot of RAM for a personal computer. Increase **Memory for this virtual machine** to 24GB of memory (24,576MB in computer math).

      {: .note}
      As of Security Onion version 3.1.0 in mid-2026, the [minimum required RAM/memory](https://docs.securityonion.net/en/3/main/hardware/#minimum-specs){:target="_blank"} for a Standalone Security Onion deployment is 24GB.

      ![](/assets/images/security-onion-images-win11-2026/05-onion-vm-creation-win11-2026/05-onion-vm-creation-win11-2026-011.png)

12. Next, click **Processors**. Click the **Number of processors** drop-down menu and select **4**, then click the **Number of cores per processor** dialog and select **2** for **Total processor cores: 8**.

      {: .note}
      As of Security Onion version 3.1.0 in mid-2026, the [number of CPU cores](https://docs.securityonion.net/en/3/main/hardware/#minimum-specs){:target="_blank"} for a Standalone Security Onion deployment is 4 cores.


      ![](/assets/images/security-onion-images-win11-2026/05-onion-vm-creation-win11-2026/05-onion-vm-creation-win11-2026-012.png)

13. Click **Network Adapter** in the sidebar. The virtual machine's single network adapter already has a **NAT** connection. We're going to use this as the management interface for the Security Onion VM. You need to add another network adapter that Security Onion will use to monitor network traffic, so click **Add** at the bottom of the sidebar.
   ![](/assets/images/security-onion-images-win11-2026/05-onion-vm-creation-win11-2026/05-onion-vm-creation-win11-2026-013.png)
14. When the **Add Hardware Wizard** displays, select **Network Adapter** and click **Finish**.
   ![](/assets/images/security-onion-images-win11-2026/05-onion-vm-creation-win11-2026/05-onion-vm-creation-win11-2026-014.png)
15. **Network Adapter 2** displays on the **Device** list. Click it and select the **Custom: Specific virtual network** radio button, then click the drop-down menu and select **HOME_NET_LAN** from the list of VMnets.
   ![](/assets/images/security-onion-images-win11-2026/05-onion-vm-creation-win11-2026/05-onion-vm-creation-win11-2026-015.png)
16. You're done adding hardware to the OPNsense VM. Click **Close**.
   ![](/assets/images/security-onion-images-win11-2026/05-onion-vm-creation-win11-2026/05-onion-vm-creation-win11-2026-016.png)
17. Click **Finish** to close the **New Virtual Machine Wizard** and complete the creation of the OPNsense VM.
   ![](/assets/images/security-onion-images-win11-2026/05-onion-vm-creation-win11-2026/05-onion-vm-creation-win11-2026-017.png)
18. The OPNsense VM appears in the left sidebar. Drag it into the **Security-Onion-2026** folder.
   ![](/assets/images/security-onion-images-win11-2026/05-onion-vm-creation-win11-2026/05-onion-vm-creation-win11-2026-018.png)
19. Create a snapshot of the VM so that you can revert to this state if something goes wrong in the future. Look for the clock icon with the red plus sign in the menu bar to **Take a snapshot of this virtual machine**.
   ![](/assets/images/security-onion-images-win11-2026/05-onion-vm-creation-win11-2026/05-onion-vm-creation-win11-2026-019.png)
20. In the Take snapshot dialog, enter a **Name** and **Description** for the snapshot and click **Take Snapshot**.
   ![](/assets/images/security-onion-images-win11-2026/05-onion-vm-creation-win11-2026/05-onion-vm-creation-win11-2026-020.png)
21. You are now ready to start your OPNsense VM, install it, and configure it to handle the traffic for your local lab.
   ![](/assets/images/security-onion-images-win11-2026/05-onion-vm-creation-win11-2026/05-onion-vm-creation-win11-2026-021.png)