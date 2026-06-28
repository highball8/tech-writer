---
layout: page
title: Configure the OPNsense Virtual Machine
nav_order: 14
parent: "Security Onion Virtual Lab Tutorial: Introduction (MacOS, 2022) (MacOS, 2022)"
---

# Configure the OPNsense Virtual Machine

1. Now click the play icon to run the virtual machine (VM). (You can also select the **Virtual Machine** menu and click **Start**.)
   ![](/assets/images/security-onion-images-macos-2022/04-opn-sense-config-macos-2022/04-opn-sense-config-macos-2022-001.png)
2. When you see the login prompt after the VM starts, use the credentials for installation:

   * **Username**: installer
   * **Password**: opnsense
     ![](/assets/images/security-onion-images-macos-2022/04-opn-sense-config-macos-2022/04-opn-sense-config-macos-2022-002.png)

3. On the **Keymap Selection** pane, leave the default option **Continue with default keymap** and press `Enter` to choose the **Select** option.
   ![](/assets/images/security-onion-images-macos-2022/04-opn-sense-config-macos-2022/04-opn-sense-config-macos-2022-003.png)
4. Leave the **Install (UFS)** option and press `Enter` to select **OK**.
   ![](/assets/images/security-onion-images-macos-2022/04-opn-sense-config-macos-2022/04-opn-sense-config-macos-2022-004.png)
5. I received a warning that I had not assigned enough RAM to the VM, but I selected **Proceed anyway**.
   ![](/assets/images/security-onion-images-macos-2022/04-opn-sense-config-macos-2022/04-opn-sense-config-macos-2022-005.png)
6. Use the down-arrow key to select **da0**, the VMware default virtual hard disk with a size of 20GB (OPNsense's minimum recommended size is 8GB), then selected **OK**.
   ![](/assets/images/security-onion-images-macos-2022/04-opn-sense-config-macos-2022/04-opn-sense-config-macos-2022-006.png)
7. There is a drive-erasure warning. Use the left arrow key to select **Yes** and press `Enter`.
   ![](/assets/images/security-onion-images-macos-2022/04-opn-sense-config-macos-2022/04-opn-sense-config-macos-2022-007.png)
8. Various panes will display progress for the installation.
   ![](/assets/images/security-onion-images-macos-2022/04-opn-sense-config-macos-2022/04-opn-sense-config-macos-2022-008.png)
9. On the **Final Configuration** pane, press enter for **Root Password Change root password**.
   ![](/assets/images/security-onion-images-macos-2022/04-opn-sense-config-macos-2022/04-opn-sense-config-macos-2022-009.png)
10. Enter a new password for the root account and select **OK**.
   ![](/assets/images/security-onion-images-macos-2022/04-opn-sense-config-macos-2022/04-opn-sense-config-macos-2022-010.png)
11. Re-enter the new root password and select **OK**.
   ![](/assets/images/security-onion-images-macos-2022/04-opn-sense-config-macos-2022/04-opn-sense-config-macos-2022-011.png)
12. Back on the **Final Configuration** pane, select **Complete Install Exit and reboot** and press `Enter` to select **OK**.
   ![](/assets/images/security-onion-images-macos-2022/04-opn-sense-config-macos-2022/04-opn-sense-config-macos-2022-012.png)
13. The system will reboot. You will see a lot of output as it comes back up.
   ![](/assets/images/security-onion-images-macos-2022/04-opn-sense-config-macos-2022/04-opn-sense-config-macos-2022-013.png)
14. Now you need to change the VM's settings to remove that installation media and make sure that it is booting from the virtual hard disk. In the VMware Fusion menu, click the **Virtual Machine** menu and select **Shut Down**.
   ![](/assets/images/security-onion-images-macos-2022/04-opn-sense-config-macos-2022/04-opn-sense-config-macos-2022-014.png)
15. Click the wrench icon at the top of the VM's window to enter the settings.
   ![](/assets/images/security-onion-images-macos-2022/04-opn-sense-config-macos-2022/04-opn-sense-config-macos-2022-015.png)
16. Click **CD/DVD (IDE)**.
   ![](/assets/images/security-onion-images-macos-2022/04-opn-sense-config-macos-2022/04-opn-sense-config-macos-2022-016.png)
17. Twirl down **Advanced options**.
   ![](/assets/images/security-onion-images-macos-2022/04-opn-sense-config-macos-2022/04-opn-sense-config-macos-2022-017.png)
18. Click **Remove CD/DVD Drive**.
   ![](/assets/images/security-onion-images-macos-2022/04-opn-sense-config-macos-2022/04-opn-sense-config-macos-2022-018.png)
19. Click **Remove** to confirm that you want to remove the drive.
   ![](/assets/images/security-onion-images-macos-2022/04-opn-sense-config-macos-2022/04-opn-sense-config-macos-2022-019.png)
20. You are returned to the main **Settings** window. Click **Startup Disk**.
   ![](/assets/images/security-onion-images-macos-2022/04-opn-sense-config-macos-2022/04-opn-sense-config-macos-2022-020.png)
21. Click **Hard Disk (SCSI)** and select **Restart** window to reboot the VM.
   ![](/assets/images/security-onion-images-macos-2022/04-opn-sense-config-macos-2022/04-opn-sense-config-macos-2022-021.png)
22. When the `login:` prompt displays, enter `root` and press `Enter`.
   ![](/assets/images/security-onion-images-macos-2022/04-opn-sense-config-macos-2022/04-opn-sense-config-macos-2022-022.png)
23. Enter your new password for the root account and press `Enter`.
   ![](/assets/images/security-onion-images-macos-2022/04-opn-sense-config-macos-2022/04-opn-sense-config-macos-2022-023.png)
24. From the menu, select `1) Assign interfaces`.
   ![](/assets/images/security-onion-images-macos-2022/04-opn-sense-config-macos-2022/04-opn-sense-config-macos-2022-024.png)
25. The next option is `Do you want to configure LAGGs now`. Select `n` unless you want to configure link aggregation.
26. Enter `n` for `Do you want to configure VLANs now?`.
27. You are prompted to `Enter the WAN interface name`. You can choose from three interfaces: `em0`, `em1`, and `em2`, each of which display their MAC address. To confirm the MAC address, open the VM's **Settings** and click **Network Adapter**.
   ![](/assets/images/security-onion-images-macos-2022/04-opn-sense-config-macos-2022/04-opn-sense-config-macos-2022-025.png)
28. Twirl down **Advanced options** in the **Network Adapter** window.
   ![](/assets/images/security-onion-images-macos-2022/04-opn-sense-config-macos-2022/04-opn-sense-config-macos-2022-026.png)
29. The **Network Adapter**, which is the network adapter that intended for WAN traffic to the public internet, matches the MAC address for `em0`.
   ![](/assets/images/security-onion-images-macos-2022/04-opn-sense-config-macos-2022/04-opn-sense-config-macos-2022-027.png)
30. Go back to the prompt, type `em0` and press `Enter`.
   ![](/assets/images/security-onion-images-macos-2022/04-opn-sense-config-macos-2022/04-opn-sense-config-macos-2022-028.png)
31. Next you are prompted to `Enter the LAN interface name`. Use the same steps to check the MAC addresses in the VM's settings. In this example, the VM's **Network Adapter 2**, which has the same MAC as `em1`, is the interface intended for the LAN, so type `em1` and press `Enter`.
   ![](/assets/images/security-onion-images-macos-2022/04-opn-sense-config-macos-2022/04-opn-sense-config-macos-2022-029.png)
32. The prompt asks for the name for Optional interface 1. This would be `em2`, the interface intended for the **HOME_NET_LAN**. However, you can set this up through the web management interface, so press `Enter` for nothing.
33. Type `y` and press `Enter` when prompted `Do you want to proceed?`
    ![](/assets/images/security-onion-images-macos-2022/04-opn-sense-config-macos-2022/04-opn-sense-config-macos-2022-030.png)
    * **Note:** When I perform this step, the output from the VM sometimes halts at `Starting router advertisement service...done.` If this happens, press `Control + C` to get it to proceed.

34. The OPNsense prompt reloads, displaying the LAN (em1) and WAN (em0) IP addresses. Press `2) to Set interface IP address` and then press `Enter`.
    ![](/assets/images/security-onion-images-macos-2022/04-opn-sense-config-macos-2022/04-opn-sense-config-macos-2022-031.png)

35. To assign the IP address for the LAN interface, enter `1` for `1 - LAN` for `em1`. (The WAN IP has already been set by my home network's router.)
36. Enter `n` for `Configure IPv4 address LAN interface via DHCP?`. (In this scenario you will assign a static IP address).
37. Enter the `new LAN IPv4 address`. This example uses `10.10.9.1`.
38. Enter `24` as the `LAN IPv4 subnet`.
39. Since this is for the LAN, press `Enter` for no upstream gateway address.
40. Enter `n` for `IPv6 address... via WAN tracking`.
41. Enter `n` for `IPv6 address... via DHCP6`.
42. Press `Enter` for no `LAN IPv6 address`.
43. Enter `y` to `enable the DHCP server on LAN`.
    ![](/assets/images/security-onion-images-macos-2022/04-opn-sense-config-macos-2022/04-opn-sense-config-macos-2022-032.png)
44. For the `start address for IPv4 client address range`, enter `10.10.9.2`.
45. Enter `10.10.9.254` for the `end address for IPv4 client address range`.
46. Enter `n` for `Do you want to revert to HTTP as the web GUI protocol?`
47. Enter `n` since there is no need `to generate a new self-signed web GUI certificate`.
48. Since there is no need to `Restore web GUI access defaults`, enter `n`.
    ![](/assets/images/security-onion-images-macos-2022/04-opn-sense-config-macos-2022/04-opn-sense-config-macos-2022-033.png)
49. The output shows the banner. It says you can access the web GUI at `https://10.10.9.1`, the address I statically assigned to the OPNsense VM on the LAN. It also shows a LAN IP address of `10.10.9.1` and a WAN IP of `192.168.1.111`.
    ![](/assets/images/security-onion-images-macos-2022/04-opn-sense-config-macos-2022/04-opn-sense-config-macos-2022-034.png)
50. At this point, I need another VM to connect to the OPNsense router's Web GUI. Since I already have a Kali VM that I will be using as part of this series of tutorials, I drag that into my **localLab** folder.
    ![](/assets/images/security-onion-images-macos-2022/04-opn-sense-config-macos-2022/04-opn-sense-config-macos-2022-035.png)
51. Open the Kali VM's **Settings** and select **Network Adapter**.
    ![](/assets/images/security-onion-images-macos-2022/04-opn-sense-config-macos-2022/04-opn-sense-config-macos-2022-036.png)
52. Click **EXTERNAL_NET_LAN** and close the window.
    ![](/assets/images/security-onion-images-macos-2022/04-opn-sense-config-macos-2022/04-opn-sense-config-macos-2022-037.png)
53. Start the Kali VM.
    ![](/assets/images/security-onion-images-macos-2022/04-opn-sense-config-macos-2022/04-opn-sense-config-macos-2022-038.png)
54. Once you have logged in to the Kali VM, launch the Terminal.
    ![](/assets/images/security-onion-images-macos-2022/04-opn-sense-config-macos-2022/04-opn-sense-config-macos-2022-039.png)
55. Here are some commands to check basic networking and connectivity:

    * The output of `ip a` for the network interface `eth0` displays an IP address on the EXTERNAL_NET_LAN network, `10.10.9.2`, which is within the IP address range set for OPNsense's DHCP service.

        ```bash
        2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
            link/ether 00:0c:29:d2:d3:2b brd ff:ff:ff:ff:ff:ff
            inet 10.10.9.2/24 brd 10.10.9.255 scope global dynamic noprefixroute eth0
            valid_lft 7126sec preferred_lft 7126sec
            inet6 fe80::20c:29ff:fed2:d32b/64 scope link noprefixroute 
            valid_lft forever preferred_lft forever
        ```

    * The `arp -a` command shows that there is another host on the network, the OPNsense router at 10.10.9.1, which is the static IP assigned to it earlier.\
    `OPNsense.localdomain (10.10.9.1) at 00:0c:29:cc:d3:63 [ether] on eth0`
    * `$ ping -c 4 google.com`: The output indicates that I can connect to the public internet and that DNS is working.

        ```bash
        PING google.com (142.250.65.174) 56(84) bytes of data.
        64 bytes from lga25s71-in-f14.1e100.net (142.250.65.174): icmp_seq=1 ttl=117 time=16.5 ms
        64 bytes from lga25s71-in-f14.1e100.net (142.250.65.174): icmp_seq=2 ttl=117 time=19.7 ms
        64 bytes from lga25s71-in-f14.1e100.net (142.250.65.174): icmp_seq=3 ttl=117 time=12.3 ms
        64 bytes from lga25s71-in-f14.1e100.net (142.250.65.174): icmp_seq=4 ttl=117 time=15.1 ms

        --- google.com ping statistics ---
        4 packets transmitted, 4 received, 0% packet loss, time 3005ms
        rtt min/avg/max/mdev = 12.294/15.903/19.722/2.671 ms
        ```

56. Now open a browser in the Kali VM and navigate to `https://10.10.9.1`, the web interface for the OPNsense router.
    ![](/assets/images/security-onion-images-macos-2022/04-opn-sense-config-macos-2022/04-opn-sense-config-macos-2022-040.png)
57. You get a self-signed certificate warning. Click **Advanced**.
    ![](/assets/images/security-onion-images-macos-2022/04-opn-sense-config-macos-2022/04-opn-sense-config-macos-2022-041.png)
58. If you read the warning, it will indicate that the Firefox browser does not trust the OPNsense's web user interface's self-signed certificate. Click **Accept the Risk and Continue**.
    ![](/assets/images/security-onion-images-macos-2022/04-opn-sense-config-macos-2022/04-opn-sense-config-macos-2022-042.png)
59. On the **Login | OPNsense** page, enter your root credentials and click **Login**.
    ![](/assets/images/security-onion-images-macos-2022/04-opn-sense-config-macos-2022/04-opn-sense-config-macos-2022-043.png)
60. Click **Next** to run through the setup wizard. (You can also run the setup wizard by clicking **Wizard** in the left sidebar.)
    ![](/assets/images/security-onion-images-macos-2022/04-opn-sense-config-macos-2022/04-opn-sense-config-macos-2022-044.png)
61. You can change properties such as the **Hostname**, or the DNS server information, or make no changes and click **Next**.
    ![](/assets/images/security-onion-images-macos-2022/04-opn-sense-config-macos-2022/04-opn-sense-config-macos-2022-045.png)
62. If you like you can change the **Timezone** and click **Next**.
    ![](/assets/images/security-onion-images-macos-2022/04-opn-sense-config-macos-2022/04-opn-sense-config-macos-2022-046.png)
63. On the **System: Wizard: Configure WAN Interface** screen, scroll to the bottom and click **Next**.
    ![](/assets/images/security-onion-images-macos-2022/04-opn-sense-config-macos-2022/04-opn-sense-config-macos-2022-047.png)
64. You do not need to make any changes on the **System: Wizard: Configure LAN Interface** screen. The screen displays the **LAN IP Address** (**10.10.9.1**) and **Subnet Mask** (**24**) that you previously configured. Click  **Next**.
    ![](/assets/images/security-onion-images-macos-2022/04-opn-sense-config-macos-2022/04-opn-sense-config-macos-2022-048.png)
65. You already changed the root password, so click **Next** on the **System: Wizard: Set Root Password**.
    ![](/assets/images/security-onion-images-macos-2022/04-opn-sense-config-macos-2022/04-opn-sense-config-macos-2022-049.png)
66. Click **Reload** on the **System: Wizard: Reload Configuration** screen.
    ![](/assets/images/security-onion-images-macos-2022/04-opn-sense-config-macos-2022/04-opn-sense-config-macos-2022-050.png)
67. You will see a **System: Wizard: Reload in progress** message, and then the page will reload. After the page reloads, click **Interfaces** in the left sidebar, then click **Assignments**.
    ![](/assets/images/security-onion-images-macos-2022/04-opn-sense-config-macos-2022/04-opn-sense-config-macos-2022-051.png)
68. On the **Interfaces: Assignments** page, you will see three interfaces, **LAN**, **WAN**, and **New interface**. This is the third network adapter on the OPNsense VM that you did not configure earlier. Now you will set it up as the HOME_NET_LAN that will be monitored by Security Onion. The drop-down next to **New interface** will default to that third interface.
    ![](/assets/images/security-onion-images-macos-2022/04-opn-sense-config-macos-2022/04-opn-sense-config-macos-2022-052.png)

    * **Note:** You can confirm this is the correct interface by comparing it with the MAC address for OPNsense **Network Adapter 3**.
      ![](/assets/images/security-onion-images-macos-2022/04-opn-sense-config-macos-2022/04-opn-sense-config-macos-2022-053.png)  

69. Enter a **Description** of **HOME_NET** and click the plus icon (**+**) to the right of **New interface**.
    ![](/assets/images/security-onion-images-macos-2022/04-opn-sense-config-macos-2022/04-opn-sense-config-macos-2022-054.png)
70. Click the **Save** button.
    ![](/assets/images/security-onion-images-macos-2022/04-opn-sense-config-macos-2022/04-opn-sense-config-macos-2022-055.png)
71. When the page reloads, click the new **[HOME_NET]** entry under **Interfaces** in the left sidebar.
    ![](/assets/images/security-onion-images-macos-2022/04-opn-sense-config-macos-2022/04-opn-sense-config-macos-2022-056.png)
72. On the **Interfaces: [HOME_NET]** page, select **Enable Interface**.
    ![](/assets/images/security-onion-images-macos-2022/04-opn-sense-config-macos-2022/04-opn-sense-config-macos-2022-057.png)
73. Click the **IPv4 Configuration Type** drop-down and select **Static IPv4**.
    ![](/assets/images/security-onion-images-macos-2022/04-opn-sense-config-macos-2022/04-opn-sense-config-macos-2022-058.png)
74. Scroll down to the bottom of the page, which now displays a Static IPv4 configuration section. Enter the IPv4 address for the HOME_NET_LAN of **10.10.10.1** and select **24** as the subnet value, then click **Save**.
    ![](/assets/images/security-onion-images-macos-2022/04-opn-sense-config-macos-2022/04-opn-sense-config-macos-2022-059.png)
75. A banner displays at the top of the page explaining that the new changes need to be applied. Click **Apply changes**.
    ![](/assets/images/security-onion-images-macos-2022/04-opn-sense-config-macos-2022/04-opn-sense-config-macos-2022-060.png)
76. When the page reloads, scroll down the left sidebar to **Services** and click it to expand it, click **DHCPv4**, then click **[HOME_NET]**.
    ![](/assets/images/security-onion-images-macos-2022/04-opn-sense-config-macos-2022/04-opn-sense-config-macos-2022-061.png)
77. On the **Services: DHCPv4: [HOME_NET]** page, select **Enable DHCP server on the HOME_NET interface**.
    ![](/assets/images/security-onion-images-macos-2022/04-opn-sense-config-macos-2022/04-opn-sense-config-macos-2022-062.png)
78. Enter the **Range** for DHCP leases: enter **10.10.10.2** in the **from** field and **10.10.10.254** in the **to** field.
    ![](/assets/images/security-onion-images-macos-2022/04-opn-sense-config-macos-2022/04-opn-sense-config-macos-2022-063.png)
79. Scroll to the bottom of the page and click **Save**.
    ![](/assets/images/security-onion-images-macos-2022/04-opn-sense-config-macos-2022/04-opn-sense-config-macos-2022-064.png)
80. When the page reloads, click **Firewall**. When it expands, click **Settings**, then **Advanced**.
    ![](/assets/images/security-onion-images-macos-2022/04-opn-sense-config-macos-2022/04-opn-sense-config-macos-2022-065.png)
81. Scroll down the **Firewall: Settings: Advanced** page to the **Miscellaneous** section. Click the question mark icon next to **Disable Firewall**.
    ![](/assets/images/security-onion-images-macos-2022/04-opn-sense-config-macos-2022/04-opn-sense-config-macos-2022-066.png)
82. The help text says that selecting the **Disable Firewall** option will convert OPNsense into a routing-only platform. This is the desired use for OPNsense -- using it as a router -- that this tutorial requires at this time. Select **Disable all packet filtering**.
    ![](/assets/images/security-onion-images-macos-2022/04-opn-sense-config-macos-2022/04-opn-sense-config-macos-2022-067.png)
83. Scroll to the bottom of the page and click **Save**.
    ![](/assets/images/security-onion-images-macos-2022/04-opn-sense-config-macos-2022/04-opn-sense-config-macos-2022-068.png)
84. A message displays at the top of the page: **The changes have been applied successfully**. In the left sidebar, click **Lobby**, then **Dashboard**.
    ![](/assets/images/security-onion-images-macos-2022/04-opn-sense-config-macos-2022/04-opn-sense-config-macos-2022-069.png)
85. When the page reloads, click **Dashboard** under **Lobby**.
    ![](/assets/images/security-onion-images-macos-2022/04-opn-sense-config-macos-2022/04-opn-sense-config-macos-2022-070.png)
86. On the **Lobby: Dashboard** page, click the link for **Click to check for updates**.
    ![](/assets/images/security-onion-images-macos-2022/04-opn-sense-config-macos-2022/04-opn-sense-config-macos-2022-071.png)
87. The **System: Firmware** page loads. It will display some terminal output and you may also see some release notes in a pop-up. When the system knows what packages need to be upgraded, scroll to the bottom of the **Updates** tab and click **Update**.
    ![](/assets/images/security-onion-images-macos-2022/04-opn-sense-config-macos-2022/04-opn-sense-config-macos-2022-072.png)
88. You will see a **Reboot required** dialog explaining that when the update is done, OPNsense will reboot. Click **OK**.
    ![](/assets/images/security-onion-images-macos-2022/04-opn-sense-config-macos-2022/04-opn-sense-config-macos-2022-073.png)
89. After the update, you will see a **Your device is rebooting** warning.
    ![](/assets/images/security-onion-images-macos-2022/04-opn-sense-config-macos-2022/04-opn-sense-config-macos-2022-074.png)
90. The initial configuration of OPNsense is now complete. Shut the VM down so you can take a snapshot.
    ![](/assets/images/security-onion-images-macos-2022/04-opn-sense-config-macos-2022/04-opn-sense-config-macos-2022-075.png)
91. Click the **Snapshot** icon.
    ![](/assets/images/security-onion-images-macos-2022/03-opn-sense-vm-creation-macos-2022/03-opn-sense-vm-creation-macos-2022-027.png)
92. In the **Snapshots** window, click the camera icon in the top-left corner.
    ![](/assets/images/security-onion-images-macos-2022/04-opn-sense-config-macos-2022/04-opn-sense-config-macos-2022-076.png)
93. Give your snapshot a name (I used **fully-configured**) and click **Take**, then close the **Snapshots** window.
    ![](/assets/images/security-onion-images-macos-2022/04-opn-sense-config-macos-2022/04-opn-sense-config-macos-2022-077.png)

**Note:** Remember to store the credentials for the OPNsense somewhere so that you can log in using the console or the web interface. The username is `root` and the password is whatever you set. One place you can record this and other useful information is in the **Notes** field of the General item in the virtual machine's **Settings**.
![](/assets/images/security-onion-images-macos-2022/04-opn-sense-config-macos-2022/04-opn-sense-config-macos-2022-078.png)
