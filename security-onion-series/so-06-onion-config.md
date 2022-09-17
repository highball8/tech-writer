---
layout: page
title: Configure the Security Onion Virtual Machine
permalink: /security-onion-series/security-onion-configure-security-onion
nav_order: 16
parent: "Security Onion Virtual Lab Tutorial: Introduction"
---

# Configure the Security Onion Virtual Machine

1. Start the VM by clicking the playhead icon or from the **Virtual Machine** menu.
   ![06-onion-config-001.png](./images/06-onion-config/06-onion-config-001.png)
2. Select **Install Security Onion \<version\>** when the Security Onion prompt screen loads.
   ![06-onion-config-002.png](./images/06-onion-config/06-onion-config-002.png)
3. Press `Enter` at the prompt to begin installation.
   ![06-onion-config-003.png](./images/06-onion-config/06-onion-config-003.png)
4. There is a drive-erasure warning. Type `yes` and press `Enter`.
   ![06-onion-config-004.png](./images/06-onion-config/06-onion-config-004.png)
5. Enter an administrative username for the CentOS 7 operating system that will run Security Onion.
   ![06-onion-config-005.png](./images/06-onion-config/06-onion-config-005.png)
6. Set an administrative password and press `Enter`.
   ![06-onion-config-006.png](./images/06-onion-config/06-onion-config-006.png)
7. Re-enter the administrative password and press `Enter`.
   ![06-onion-config-007.png](./images/06-onion-config/06-onion-config-007.png)
8. The output represents the installation of the base CentOS 7 operating system. It will take about 10 minutes. When you see the `Initial Install Complete` prompt, press `Enter`.
   ![06-onion-config-008.png](./images/06-onion-config/06-onion-config-008.png)
9. When the VM comes online, log in with the new credentials you created for the VM.
   ![06-onion-config-009.png](./images/06-onion-config/06-onion-config-009.png)
10. The setup wizard should start automatically. Select **Yes** to continue.
   ![06-onion-config-010.png](./images/06-onion-config/06-onion-config-010.png)
11. Leave **Install Run the standard Security Onion installation** and use the tab key to select **Ok** then press `Enter`.
   ![06-onion-config-011.png](./images/06-onion-config/06-onion-config-011.png)
12. **EVAL** is selected by default. While the evaluation installation should work for the defined use case, use the down arrow key to select **STANDALONE**, which is a production installation of a single Security Onion host, then select **OK** and press `Enter`.
   ![06-onion-config-012.png](./images/06-onion-config/06-onion-config-012.png)
13. Type `agree` to agree to the terms of the Elastic license, then select **OK**.
   ![06-onion-config-013.png](./images/06-onion-config/06-onion-config-013.png)
14. Give your Security Onion deployment a name and select **OK**.
   ![06-onion-config-014.png](./images/06-onion-config/06-onion-config-014.png)
15. You can also enter a short description for your Security Onion, or just leave it blank, select **OK** and press `Enter`.
   ![06-onion-config-015.png](./images/06-onion-config/06-onion-config-015.png)
16. You are prompted to select the **management NIC**. As we did with the OPNsense VM, use the VM's **Network Adapter** settings to confirm the MAC address for the correct network adapter. In this case, I am choosing **ens33**, which has a MAC address ending in **39:54**, which matches the first network adapter on the VM, which I have in bridged mode. In the Security Onion setup wizard, use the spacebar to select **ens33**, then select **OK**.
   ![06-onion-config-016.png](./images/06-onion-config/06-onion-config-016.png)
17. Because I don't have a real management network and I am connecting the management interface to my home, physical network which already uses DHCP addressing, I use the down arrow key and spacebar to select **DHCP** and then select **OK**.
   ![06-onion-config-017.png](./images/06-onion-config/06-onion-config-017.png)
18. If you select DHCP, you will get a warning from Security Onion reminding you that a DHCP-assigned address could change, and you might have problems connecting to the management interface of Security Onion. This is not an issue in my case, so I select **Yes** to keep DHCP.
   ![06-onion-config-018.png](./images/06-onion-config/06-onion-config-018.png)
19. Select **OK** when you see **Setup will now initialize networking** and press `Enter`.
   ![06-onion-config-019.png](./images/06-onion-config/06-onion-config-019.png)
20. Since we are not airgapping this system or this network, leave **Standard** selected and select **OK**.
   ![06-onion-config-020.png](./images/06-onion-config/06-onion-config-020.png)
21. When asked **How would you like to connect to the Internet?** I select **Direct** since I am not using a proxy.
   ![06-onion-config-021.png](./images/06-onion-config/06-onion-config-021.png)
22. A progress bar displays.
   ![06-onion-config-022.png](./images/06-onion-config/06-onion-config-022.png)
23. When asked to select the **Monitor Interface**, I only have one option, which matches with the VM network adapter connected to the HOME_NET_LAN. This is what I want, so I select **ens34** and proceed.
   ![06-onion-config-023.png](./images/06-onion-config/06-onion-config-023.png)
24. For **Choose OS patch schedule**, leave **Automatic** selected and select **OK**.
   ![06-onion-config-024.png](./images/06-onion-config/06-onion-config-024.png)
25. The field for **your home network(s)** is prepopulated with RFC1918 IP addresses using CIDR notation. Since this Security Onion will monitor a single network created with VMware Fusion Pro and the OPNsense VM, HOME_NET_LAN, clear the default values. (You can use `Control` + `u`.) Then enter the IP address range for the HOME_NET_LAN using the correct CIDR notation: **10.10.10.0/24**, select **OK** and press `Enter`.
   ![06-onion-config-025.png](./images/06-onion-config/06-onion-config-025.png)
26. Keep the default manager type, **Basic**, selected, select **OK** and press `Enter`.
   ![06-onion-config-026.png](./images/06-onion-config/06-onion-config-026.png)
27. When you are prompted for which tool you want to generate metadata, keep **Zeek** selected, select **OK** and press `Enter`.
   ![06-onion-config-027.png](./images/06-onion-config/06-onion-config-027.png)
28. You are asked to select the ruleset that Suricata will use to detect malicious activity on the network. Keep **ETOPEN** selected since it is a free, open-source ruleset, then select **OK** and press `Enter`.
   ![06-onion-config-028.png](./images/06-onion-config/06-onion-config-028.png)
29. Security Onion lets you choose whether or not you want to run additional, optional services. The understanding is that more services use more RAM, and you can deselect some of the services to conserve resources. All items are selected by default. You can use the spacebar to unselect items, then select **OK**.
   ![06-onion-config-029.png](./images/06-onion-config/06-onion-config-029.png)
30. Select **Yes** to keep the default Docker IP range.
   ![06-onion-config-030.png](./images/06-onion-config/06-onion-config-030.png)
31. Enter an email address. The email address only acts as the username for the account that you will use to log in to the Security Onion dashboard. It will not send emails to this address. So you can use **email@email.com**.
   ![06-onion-config-031.png](./images/06-onion-config/06-onion-config-031.png)
32. Enter a password for this Security Onion account.
   ![06-onion-config-032.png](./images/06-onion-config/06-onion-config-032.png)
33. Enter the password again.
   ![06-onion-config-033.png](./images/06-onion-config/06-onion-config-033.png)
34. The wizard asks if you want to use an IP address or a hostname to navigate to the Security Onion Console. This example skips the management network approach and am assigns the Security Onion management NIC an IP address on my home network, so I leave **IP** selected and then select **OK**.
   ![06-onion-config-034.png](./images/06-onion-config/06-onion-config-034.png)
35. You are prompted to set a password for the **soremote** user, which you would use in a distributed deployment of multiple Security Onion hosts. Select **OK**.
   ![06-onion-config-035.png](./images/06-onion-config/06-onion-config-035.png)
36. Enter a password for the **soremote** account.
   ![06-onion-config-036.png](./images/06-onion-config/06-onion-config-036.png)
37. Enter the password again.
   ![06-onion-config-037.png](./images/06-onion-config/06-onion-config-037.png)
38. When asked for the type of configuration you want for you Security Onion deployment, keep **Basic** selected, then select **OK** and press `Enter`.
   ![06-onion-config-038.png](./images/06-onion-config/06-onion-config-038.png)
39. You are prompted for the number of **Zeek processes** that you want running. Because this is for demonstration and I don't want it to consume too many resources, I leave the default of **1**.
   ![06-onion-config-039.png](./images/06-onion-config/06-onion-config-039.png)
40. Leave the number of **Suricata processes** at **1**.
   ![06-onion-config-040.png](./images/06-onion-config/06-onion-config-040.png)
41. Select **Yes** to **configure ntp servers**.
   ![06-onion-config-041.png](./images/06-onion-config/06-onion-config-041.png)
42. Leave the default NTP servers and select **OK**,
   ![06-onion-config-042.png](./images/06-onion-config/06-onion-config-042.png)
43. Leave the **config** type of **NODEBASIC Install Search Node with recommended settings** defaults and select **OK**.
   ![06-onion-config-043.png](./images/06-onion-config/06-onion-config-043.png)
44. The **so-allow** command opens up the management interface of your Security Onion installation to an IP address range from which clients can navigate to the web management interface or connect over SSH. Select **Yes**.
   ![06-onion-config-044.png](./images/06-onion-config/06-onion-config-044.png)
45. Because I am using my home network as the "management network," I enter **192.168.1.0/24** in CIDR notation so that devices on that network can navigate to the Security Onion web management interface.
   ![06-onion-config-045.png](./images/06-onion-config/06-onion-config-045.png)
46. The final pane summarizes all of the options you have configured and gives you the choice to accept these configurations and proceed.
   ![06-onion-config-046.png](./images/06-onion-config/06-onion-config-046.png)
47. Use the down arrow key if you want to scroll to the bottom of the pane to see all of the information. When you are done, use the `Tab` key to select **Yes** and press `Enter` to complete the Security Onion installation.
   ![06-onion-config-047.png](./images/06-onion-config/06-onion-config-047.png)
48. A progress bar displays Security Onion installation phases. In my experience, the process takes at least 20 minutes to complete, depending on host system resources.
   ![06-onion-config-048.png](./images/06-onion-config/06-onion-config-048.png)
49. When the process is complete, you see a confirmation message saying that the installation succeeded. It also provides the URL you use to access the Security Onion Console. Press `Enter` to select **OK** and reboot the VM.
   ![06-onion-config-049.png](./images/06-onion-config/06-onion-config-049.png)

**Note:** Consider shutting down the Security Onion VM and taking a snapshot.