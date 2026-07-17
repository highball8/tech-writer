---
layout: page
title: "Create the OPNsense Virtual Machine"
nav_order: 13
parent: "Security Onion: Creating a Virtual Lab Environment—Windows 11, 2026"
---

# Create the OPNsense Virtual Machine

1. For this tutorial, I will create my virtual machines (VMs) in a folder called **Security-Onion-2026**. In the left sidebar of VMware Workstation, right-click **My Computer** and select **New Folder**.
   ![](/assets/images/security-onion-images-win11-2026/03-opn-sense-vm-creation-win11-2026/03-opn-sense-vm-creation-win11-2026-001.png)
2. Right-click the name of the new folder in the sidebar, select **Rename...** and type in a name for your folder and press `Enter`.
   ![](/assets/images/security-onion-images-win11-2026/03-opn-sense-vm-creation-win11-2026/03-opn-sense-vm-creation-win11-2026-002.png)
3. Click the **File** menu and then click **New Virtual Machine**.
   ![](/assets/images/security-onion-images-win11-2026/03-opn-sense-vm-creation-win11-2026/03-opn-sense-vm-creation-win11-2026-003.png)
4. When the **New Virtual Machine Wizard** opens, leave the **Typical (recommended)** radio button selected and click **Next**.
   ![](/assets/images/security-onion-images-win11-2026/03-opn-sense-vm-creation-win11-2026/03-opn-sense-vm-creation-win11-2026-004.png)
5. On the **Guest Operating System Installation** screen, select **Installer from disk image (iso)** and click **Browse** underneath it.
   ![](/assets/images/security-onion-images-win11-2026/03-opn-sense-vm-creation-win11-2026/03-opn-sense-vm-creation-win11-2026-005.png)
6. In the **Browse for ISO Image** dialog, navigate to the OPNsense ISO that you extracted earlier, select it, and click **Open**.
   ![](/assets/images/security-onion-images-win11-2026/03-opn-sense-vm-creation-win11-2026/03-opn-sense-vm-creation-win11-2026-006.png)
7. VMware will detect the operating system type based on the ISO. Click **Next**.
   ![](/assets/images/security-onion-images-win11-2026/03-opn-sense-vm-creation-win11-2026/03-opn-sense-vm-creation-win11-2026-007.png)
8. On the **Name the Virtual Machine** screen, enter a name for the OPNsense VM. I named mine **OPNsense2026**. Then click the **Browse** button to select the location where the VM and its files will be saved to and stored.  
   ![](/assets/images/security-onion-images-win11-2026/03-opn-sense-vm-creation-win11-2026/03-opn-sense-vm-creation-win11-2026-008.png)
9. When you create a virtual machine, VMware stores a collection of files and other data in a folder. I have created a folder on my local drive called **onion-virtual-machines**. Within that, I created a new folder and gave it the same name as the VM. Navigate to the location where you want the VM stored and click **OK**. 
   ![](/assets/images/security-onion-images-win11-2026/03-opn-sense-vm-creation-win11-2026/03-opn-sense-vm-creation-win11-2026-009.png)
10. Click **Next**.\\
   ![](/assets/images/security-onion-images-win11-2026/03-opn-sense-vm-creation-win11-2026/03-opn-sense-vm-creation-win11-2026-010.png)
11. On the **Specify Disk Capacity** screen, you can leave the default **Maximum disk size (GB)** at 20GB. Once created, the OPNsense router will not need much storage. Leave the **Split virtual disk into multiple files** radio button selected and click **Next**.
   ![](/assets/images/security-onion-images-win11-2026/03-opn-sense-vm-creation-win11-2026/03-opn-sense-vm-creation-win11-2026-011.png)
12. The **Ready to Create Virtual Machine** screen displays a summary of the VM's properties. Click **Customize Hardware**.\\
   ![](/assets/images/security-onion-images-win11-2026/03-opn-sense-vm-creation-win11-2026/03-opn-sense-vm-creation-win11-2026-012.png)
13. The **Hardware** dialog opens. This is where you can add virtualized hardware to a virtual machine, or change the specifications and resources for that hardware.
   ![](/assets/images/security-onion-images-win11-2026/03-opn-sense-vm-creation-win11-2026/03-opn-sense-vm-creation-win11-2026-013.png)
14. The first thing to change is **Memory**. VMware defaults to 256MB. Since I started using OPNsense to create these virtual labs, OPNsense has increased its resource requirements significantly. I'm going to increase **Memory for this virtual machine** to 4GB of memory (4,096MB in computer math), which is a lot, but I may decrease it later after creating and configuring the virtual machine.

      {: .note}
      As of OPNsense version 26 in mid-2026, the [minimum required RAM/memory](https://docs.opnsense.org/manual/hardware.html#hardware-requirements){:target="_blank"} for an OPNsense host is 3GB.

      ![](/assets/images/security-onion-images-win11-2026/03-opn-sense-vm-creation-win11-2026/03-opn-sense-vm-creation-win11-2026-014.png)

15. Next, click **Processors**. OPNsense should be good with a single virtualized processor for the amount of traffic we will be creating, but I do want to make it a dual-core processor. Click the **Number of cores per processor** dialog and select **2**.

      {: .note}
      As of OPNsense version 26 in mid-2026, the [minimum processor requirement](https://docs.opnsense.org/manual/hardware.html#hardware-requirements){:target="_blank"} for an OPNsense host is a single dual-core processor ("1 GHz dual-core CPU0").

      ![](/assets/images/security-onion-images-win11-2026/03-opn-sense-vm-creation-win11-2026/03-opn-sense-vm-creation-win11-2026-015.png)

16. Click **Network Adapter** in the sidebar. By default, a virtual machine has one network adapter, a virtualized network interface card (NIC). And by default, this adapter is given a **NAT** connection. With Network Address Translation, or NAT, VMware uses the host PC's IP address to allow virtual machines to connect to other networks and hosts, including the public internet. Leave this network adapter as is, but you need to create two more to connect the OPNsense VM to the two virtual private networks you created. So click **Add** at the bottom of the sidebar.
   ![](/assets/images/security-onion-images-win11-2026/03-opn-sense-vm-creation-win11-2026/03-opn-sense-vm-creation-win11-2026-016.png)
17. When the **Add Hardware Wizard** displays, select **Network Adapter** and click **Finish**.
   ![](/assets/images/security-onion-images-win11-2026/03-opn-sense-vm-creation-win11-2026/03-opn-sense-vm-creation-win11-2026-017.png)
18. **Network Adapter 2** displays on the **Device** list. Click it.
   ![](/assets/images/security-onion-images-win11-2026/03-opn-sense-vm-creation-win11-2026/03-opn-sense-vm-creation-win11-2026-018.png)
19. Select the **Custom: Specific virtual network** radio button, then click the drop-down menu and select **EXTERNAL_NET_LAN** from the list of VMnets.
   ![](/assets/images/security-onion-images-win11-2026/03-opn-sense-vm-creation-win11-2026/03-opn-sense-vm-creation-win11-2026-019.png)
20. Click **Add** again to add a third network adapter to the OPNsense VM.
   ![](/assets/images/security-onion-images-win11-2026/03-opn-sense-vm-creation-win11-2026/03-opn-sense-vm-creation-win11-2026-020.png)
21. Repeat the steps to add a network adapter through the **Add Hardware Wizard**.
   ![](/assets/images/security-onion-images-win11-2026/03-opn-sense-vm-creation-win11-2026/03-opn-sense-vm-creation-win11-2026-021.png)
22. After creating **Network Adapter 3**, select it in the **Device** list, and then the **Custom: Specific virtual network** radio button and select **HOME_NET_LAN** from the list of VMnets.
   ![](/assets/images/security-onion-images-win11-2026/03-opn-sense-vm-creation-win11-2026/03-opn-sense-vm-creation-win11-2026-022.png)
23. You're done adding hardware to the OPNsense VM. Click **Close**.
   ![](/assets/images/security-onion-images-win11-2026/03-opn-sense-vm-creation-win11-2026/03-opn-sense-vm-creation-win11-2026-023.png)
24. Click **Finish** to close the **New Virtual Machine Wizard** and complete the creation of the OPNsense VM.
   ![](/assets/images/security-onion-images-win11-2026/03-opn-sense-vm-creation-win11-2026/03-opn-sense-vm-creation-win11-2026-024.png)
25. The OPNsense VM appears in the left sidebar. Drag it into the **Security-Onion-2026** folder.
   ![](/assets/images/security-onion-images-win11-2026/03-opn-sense-vm-creation-win11-2026/03-opn-sense-vm-creation-win11-2026-025.png)
26. Create a snapshot of the VM so that you can revert to this state if something goes wrong in the future. Look for the clock icon with the red plus sign in the menu bar to **Take a snapshot of this virtual machine**.
   ![](/assets/images/security-onion-images-win11-2026/03-opn-sense-vm-creation-win11-2026/03-opn-sense-vm-creation-win11-2026-026.png)
27. In the **Take snapshot** dialog, enter a **Name** and **Description** for the snapshot and click **Take Snapshot**.
   ![](/assets/images/security-onion-images-win11-2026/03-opn-sense-vm-creation-win11-2026/03-opn-sense-vm-creation-win11-2026-027.png)
28. You are now ready to start your OPNsense VM, install it, and configure it to handle the traffic for your local lab.
   ![](/assets/images/security-onion-images-win11-2026/03-opn-sense-vm-creation-win11-2026/03-opn-sense-vm-creation-win11-2026-028.png)