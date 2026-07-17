---
layout: page
title: "Configure the Security Onion Virtual Machine"
nav_order: 16
parent: "Security Onion: Creating a Virtual Lab Environment—Windows 11, 2026"
---

# Configure the Security Onion Virtual Machine
{: .no_toc }

1. TOC
{:toc}

## Complete Base OS Installation on the Security Onion Virtual Machine

Just as with OPNsense, the first phase of setting up Security Onion is booting the virtual machine and running the installation media contained in the ISO file.

1. Click the play icon to run the virtual machine (VM) in the VMware Workstation Pro menu bar. (You can also select the **Virtual Machine** menu and click **Power on this virtual machine**.)
   ![](/assets/images/security-onion-images-win11-2026/06-onion-config-win11-2026/06-onion-config-win11-2026-001.png)
2. Select **Install Security Onion \<version\>** when the Security Onion prompt screen loads.
   ![](/assets/images/security-onion-images-win11-2026/06-onion-config-win11-2026/06-onion-config-win11-2026-002.png)
3. If you are prompted to begin installation, press `Enter`.
4. There is a drive-erasure warning. Type `yes` and press `Enter`.
   ![](/assets/images/security-onion-images-win11-2026/06-onion-config-win11-2026/06-onion-config-win11-2026-003.png)
5. You will be prompted to create an administrative user for the Oracle Linux 9 operating system that will run Security Onion. Enter a username and press `Enter`.
   ![](/assets/images/security-onion-images-win11-2026/06-onion-config-win11-2026/06-onion-config-win11-2026-004.png)
6. Set an administrative password and press `Enter`.
   ![](/assets/images/security-onion-images-win11-2026/06-onion-config-win11-2026/06-onion-config-win11-2026-005.png)
7. Re-enter the administrative password and press `Enter`.
   ![](/assets/images/security-onion-images-win11-2026/06-onion-config-win11-2026/06-onion-config-win11-2026-006.png)
8. The output represents the installation of the base Oracle Linux 9 operating system. When I took these screenshots, the installation ran for over 20 minutes, even with the 24GB of RAM and four dual-core virtual processors. When you see the `Initial Install Complete` prompt, press `Enter`.
9. When the reboot is complete, shut down the VM and take a snapshot.
   ![](/assets/images/security-onion-images-win11-2026/06-onion-config-win11-2026/06-onion-config-win11-2026-007.png)

## Install Security Onion 

1. Restart the Security Onion VM. When the `localhost login` prompt displays, enter the username and password you just set for the VM.
   ![](/assets/images/security-onion-images-win11-2026/06-onion-config-win11-2026/06-onion-config-win11-2026-008.png)
2. The setup wizard should start automatically. Select **Yes** to continue.
   ![](/assets/images/security-onion-images-win11-2026/06-onion-config-win11-2026/06-onion-config-win11-2026-009.png)
3. Leave **Install Run the standard Security Onion installation** and use the tab key to select **Ok** then press `Enter`.  
   ![](/assets/images/security-onion-images-win11-2026/06-onion-config-win11-2026/06-onion-config-win11-2026-010.png)
4. **IMPORT** is selected by default. Use the down arrow key to select **STANDALONE**, which is a production installation of a single Security Onion host, then use the `Tab` key to select **Ok** and press `Enter`.
   ![](/assets/images/security-onion-images-win11-2026/06-onion-config-win11-2026/06-onion-config-win11-2026-011.png)

   * **Note:** If you have been taking snapshots of your virtual machine, you can roll it back or create clones of the virtual machine, or both, to explore each type of installation and the different configurations.

5. Type `agree` to agree to the terms of the Elastic license, then select **Ok**.
   ![](/assets/images/security-onion-images-win11-2026/06-onion-config-win11-2026/06-onion-config-win11-2026-012.png)
6. You are not air-gapping this system or this network. Leave **Standard** selected and select **Ok**.
   ![](/assets/images/security-onion-images-win11-2026/06-onion-config-win11-2026/06-onion-config-win11-2026-013.png)
7. Give your Security Onion deployment a name and select **Ok**.
   ![](/assets/images/security-onion-images-win11-2026/06-onion-config-win11-2026/06-onion-config-win11-2026-014.png)
8. You can also enter a short description for your Security Onion, or just leave it blank, select **Ok** and press `Enter`.  
   ![](/assets/images/security-onion-images-win11-2026/06-onion-config-win11-2026/06-onion-config-win11-2026-015.png)
9. You are prompted to select the **NIC you would like to use for management**.
   ![](/assets/images/security-onion-images-win11-2026/06-onion-config-win11-2026/06-onion-config-win11-2026-016.png)
10. Open the **Virtual Machine Settings** for the Security Onion VM in VMware Workstation Pro, select your first network adapter on the **Device** list and click **Advanced**. Note the **MAC Address** in the **Network Adapter Advanced Settings** dialog. In this example, the MAC address ends in **11:97**.
   ![](/assets/images/security-onion-images-win11-2026/06-onion-config-win11-2026/06-onion-config-win11-2026-017.png)
11. In this example, **ens160** has the MAC address ending in **11:97** that matches the virtual network adapter connected to my NAT network, which is what I want as the management interface. Use the down arrow key and spacebar to select **DHCP** and then select **Ok**.
   ![](/assets/images/security-onion-images-win11-2026/06-onion-config-win11-2026/06-onion-config-win11-2026-018.png)
12. I am connecting the management interface to VMware Workstation Pro's default NAT network which already uses DHCP addressing. Use the down arrow key to select **DHCP** and then select **Ok**.
   ![](/assets/images/security-onion-images-win11-2026/06-onion-config-win11-2026/06-onion-config-win11-2026-019.png)
13. When you select DHCP, you will get a warning from Security Onion reminding you that a DHCP-assigned address could change, and you might have problems connecting to the management interface of Security Onion. For this virtual lab, it should not be an issue. Select **Yes** to keep DHCP.
   ![](/assets/images/security-onion-images-win11-2026/06-onion-config-win11-2026/06-onion-config-win11-2026-020.png)
14. When asked **How would you like to connect to the Internet?**, select **Direct**, then **Ok**.
   ![](/assets/images/security-onion-images-win11-2026/06-onion-config-win11-2026/06-onion-config-win11-2026-021.png)
15. Select **Yes** to keep the default Docker IP range.
   ![](/assets/images/security-onion-images-win11-2026/06-onion-config-win11-2026/06-onion-config-win11-2026-022.png)
16. When asked to **add NICs to the Monitor Interface**, there is only one option.
   ![](/assets/images/security-onion-images-win11-2026/06-onion-config-win11-2026/06-onion-config-win11-2026-023.png)
17. Check the MAC address of the VM's second network adapter connected to the **HOME_NET_LAN**, which ends in **11:a1**. 
   ![](/assets/images/security-onion-images-win11-2026/06-onion-config-win11-2026/06-onion-config-win11-2026-024.png)
18. This MAC address matches that displayed in the wizard, **ens192**. Press the spacebar to select it, use tab to select **Ok** and press `Enter`.
   ![](/assets/images/security-onion-images-win11-2026/06-onion-config-win11-2026/06-onion-config-win11-2026-025.png)
19. Enter an email address. The email address only acts as the username for the account that you will use to log in to the Security Onion web interface. It will not send emails to this address. So you can use **email@email.com**.  
   ![](/assets/images/security-onion-images-win11-2026/06-onion-config-win11-2026/06-onion-config-win11-2026-026.png)
20. Enter a password for this Security Onion account.  
   ![](/assets/images/security-onion-images-win11-2026/06-onion-config-win11-2026/06-onion-config-win11-2026-027.png)
21. Enter the password again.  
   ![](/assets/images/security-onion-images-win11-2026/06-onion-config-win11-2026/06-onion-config-win11-2026-028.png)
22. The wizard asks if you want to use an IP address or a hostname to navigate to the Security Onion Console. Since you have assigned the management interface to the VMware NAT network, which is assigning an address using DHCP, leave **IP** selected and then select **Ok**.
   ![](/assets/images/security-onion-images-win11-2026/06-onion-config-win11-2026/06-onion-config-win11-2026-029.png)
23. You are asked if you want to allow access to the Security Onion through its web management interface. Select **Yes** and press `Enter`.
   ![](/assets/images/security-onion-images-win11-2026/06-onion-config-win11-2026/06-onion-config-win11-2026-030.png)
24. This example uses VMware's NAT network as the "management network." Check the NAT network's IP address range in the VMware Virtual Network Editor. In this case, it is **192.168.22.0**.
   ![](/assets/images/security-onion-images-win11-2026/06-onion-config-win11-2026/06-onion-config-win11-2026-031.png)
25. Enter **192.168.22.0/24** in CIDR notation so that devices on that network can navigate to the Security Onion web management interface and select **Ok**.
   ![](/assets/images/security-onion-images-win11-2026/06-onion-config-win11-2026/06-onion-config-win11-2026-032.png)
26. The next prompt asks if you want to share usage data from your Security Onion deployment, or "SOC Telemetry," with the Security Onion. Select **No** and press `Enter`.
   ![](/assets/images/security-onion-images-win11-2026/06-onion-config-win11-2026/06-onion-config-win11-2026-033.png)
27. A summary screen shows the configuration items you have selected. As instructed, use the `Tab` key to select **Yes** and press `Enter` to complete the installation process.
   ![](/assets/images/security-onion-images-win11-2026/06-onion-config-win11-2026/06-onion-config-win11-2026-034.png)

      {: .important }
      When I performed this installation and configuration of Security Onion version 3.1.0 in mid-2026, it **took over two hours for this installation to complete**, even with 24GB of memory and eight processor cores assigned to the VM. From looking at the Windows Task Manager for the host machine running VMware Workstation Pro, it did not even appear that the VMware processes were constrained in any way.

28. You will see a lot of text output on the command line throughout the installation process: downloading and installing Linux packages, container images, Salt state configuration, and more. 
   ![](/assets/images/security-onion-images-win11-2026/06-onion-config-win11-2026/06-onion-config-win11-2026-035.png)
29. After the installation is complete you will see the wizard screen again, confirming what IP address can be used to access the web interface and your username. When you use the `Tab` key to select **Yes** and press `Enter` to exit, you will see the command line returns to the bottom of the screen.
   ![](/assets/images/security-onion-images-win11-2026/06-onion-config-win11-2026/06-onion-config-win11-2026-036.png)
30. Shut down the VM. In VMware Workstation Pro, click **Edit virtual machine settings**.
   ![](/assets/images/security-onion-images-win11-2026/06-onion-config-win11-2026/06-onion-config-win11-2026-037.png)
31. Select the **CD/DVD (IDE)** drive on the **Device** list and click **Remove**. Just as with the OPNsense VM, you have installed the software and don't need the drive. Removing the drive prevents the possibility of it booting from the installation media.
   ![](/assets/images/security-onion-images-win11-2026/06-onion-config-win11-2026/06-onion-config-win11-2026-038.png)
32. Click **Ok** to close the **Virtual Machine Settings** window.
   ![](/assets/images/security-onion-images-win11-2026/06-onion-config-win11-2026/06-onion-config-win11-2026-039.png)
33. A lot of work went into getting this far. Make sure you take a snapshot of the VM and notate it. In this example I added some notes saying that installation took over two hours but the PC I am running VMware Workstation Pro on did not seem to be particularly affected.
   ![](/assets/images/security-onion-images-win11-2026/06-onion-config-win11-2026/06-onion-config-win11-2026-040.png)

This completes the creation of the virtual lab where you will operate OPNsense, Security Onion, and your other virtual machines. Now you can start using Security Onion.