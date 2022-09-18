---
layout: page
title: Create a VMware Private Virtual Network for Your Lab
# permalink: /security-onion-series/security-onion-create-networks
slug: security-onion-create-networks
nav_order: 12
parent: "Security Onion Virtual Lab Tutorial: Introduction"
---

# Create VMware Private Virtual Networks` for Your Lab

These steps detail how you can use VMware Fusion Pro's networking capabilities to create two private virtual networks. You will connect your different virtual machines (VMs) to these networks so that the VMs can interact with one another, and reach out to the public internet to download updates, browse the internet, etc.

**Note:** Per [VMware's documentation](https://docs.vmware.com/en/VMware-Fusion/12/com.vmware.fusion.using.doc/GUID-DEB1FB99-0E44-4AAA-9693-6C2687098F13.html){:target="_blank"}, "private virtual networks (vmnet) configurations... only allow communication between virtual machines and the host system."

Follow the steps below to create two private virtual networks:

* **EXTERNAL_NET_LAN**: This will be a private virtual network that you will connect a Kali VM to, and then use the browser of the Kali VM to access the management web user interface of the OPNsense router. It is *also* the network that will simulate a public wide area network (WAN) from which the Kali VM will reconnoiter and attack the network monitored by the Security Onion deployment. In this article, you assign this network the IP address range of 10.10.9.0/24.
* **HOME_NET_LAN:** This private virtual network acts as the local-area network that Security Onion will monitor. This network is assigned the IP address range of 10.10.10.0/24. You will use that same address range when configuring Security Onion. We will connect virtual machines like Metasploitable to this network, where they can act as targets monitored by Security Onion.

Once you have created the private virtual networks, you will attach the virtual network adapters of the various virtual machines to these networks.

A note on the network names: I got the names **EXTERNAL_NET** and **HOME_NET** from one of the most important parts of Security Onion, the Suricata intrusion detection system (IDS). When setting up Security Onion, you are asked to provide your network segments you want to monitor in CIDR notation (using RFC1918 network addresses). These are your "home networks." Suricata signature-based detection rules (which are, in turn, based on Snort, an earlier IDS), use `$EXTERNAL_NET` and `$HOME_NET` to establish traffic directionality -- what is on your network is `$HOME_NET`, what is outside of your network is everything else, `$EXTERNAL_NET`. In many cases, malicious traffic needs to either come from or go to `$EXTERNAL_NET` for it to match a Suricata rule, which is why this tutorial needs both networks.

* OPNsense router:

  * **Network Adapter:** Connect to the host MacBook Pro using **Bridged Networking** > **Autodetect** so that your OPNsense VM can connect to the internet through the host operating system's internet connection.
  * **Network Adapter 2:** This will connect to the **EXTERNAL_NET_LAN** (10.10.9.0/24) subnet.
  * **Network Adapter 3:** This will connect to the **HOME_NET_LAN** (10.10.10.0/24) subnet.

* Security Onion network intrusion detection system:

  * **Network Adapter:** Connect to the host MacBook Pro using **Bridged Networking** > **Autodetect** so that you can access Security Onion via SSH and the Security Onion Console using your browser on your Mac. Think of this as the "management network" connection.
  * **Network Adapter 2:** This network adapter acts as a "sniffer" interface and will connect to the **HOME_NET_LAN** (10.10.10.0/24) subnet to monitor traffic.

* Kali virtual machine:

  **Network Adapter:** This will connect to the **EXTERNAL_NET_LAN** (10.10.9.0/24) subnet. From here it can access the web management interface of OPNsense for network management, and also reconnoiter and launch attacks against hosts on **HOME_NET_LAN**.

* Metasploitable virtual machines and other "targets:"

  * **Network Adapter:** Any virtual machines that we want to practice attacks against will be connected to **HOME_NET_LAN**.

1. Open VMware Fusion, and then open its **Preferences**.
   ![02-vmw-network-setup-001.png](./images/02-vmw-network-setup/02-vmw-network-setup-001.png)
2. Within **Preferences**, click **Network**.
   ![02-vmw-network-setup-002.png](./images/02-vmw-network-setup/02-vmw-network-setup-002.png)
3. Click the padlock icon in the bottom-left corner of the **Network** window.
   ![02-vmw-network-setup-003.png](./images/02-vmw-network-setup/02-vmw-network-setup-003.png)
4. Enter the host machine's administrator password and click **OK**.
   ![02-vmw-network-setup-004.png](./images/02-vmw-network-setup/02-vmw-network-setup-004.png)
5. Click the plus icon (**+**) to create a private virtual network for your lab environment.
   ![02-vmw-network-setup-005.png](./images/02-vmw-network-setup/02-vmw-network-setup-005.png)
6. A network appears under **Custom** > **Private to my Mac**. The name will start with **vmnet**. Click the network name once so that the name becomes editable.
   ![02-vmw-network-setup-006.png](./images/02-vmw-network-setup/02-vmw-network-setup-006.png)
7. Name this network **HOME_NET_LAN**. Press `Enter` to set the name.
   ![02-vmw-network-setup-007.png](./images/02-vmw-network-setup/02-vmw-network-setup-007.png)
8. Enter a **Subnet IP**. I am using **10.10.10.0**. Leave the **Subnet Mask** as **255.255.255.0** and click **Apply**.
   ![02-vmw-network-setup-008.png](./images/02-vmw-network-setup/02-vmw-network-setup-008.png)
9. Clear the checkboxes for **Connect the host Mac to this network** (because I am trying to create an isolated network for the lab) and **Provide addresses on this network via DHCP** (because the OPNsense router will provide the DHCP service), then click **Apply**.
   ![02-vmw-network-setup-009.png](./images/02-vmw-network-setup/02-vmw-network-setup-009.png)
10. Click the plus icon (**+**) again to create a second private virtual network.
   ![02-vmw-network-setup-010.png](./images/02-vmw-network-setup/02-vmw-network-setup-010.png)
11. A new network that starts with start with **vmnet** appears under **Custom** > **Private to my Mac**. Click the network name once so that the name becomes editable.
   ![02-vmw-network-setup-011.png](./images/02-vmw-network-setup/02-vmw-network-setup-011.png)
12. Enter **EXTERNAL_NET_LAN** as the name for this network and press `Enter`.
   ![02-vmw-network-setup-012.png](./images/02-vmw-network-setup/02-vmw-network-setup-012.png)
13. Enter a **Subnet IP** value of **10.10.9.0**. Leave the **Subnet Mask** as **255.255.255.0**. Click **Apply**.
   ![02-vmw-network-setup-013.png](./images/02-vmw-network-setup/02-vmw-network-setup-013.png)
14. Clear the checkboxes for **Connect the host Mac to this network** and **Provide addresses on this network via DHCP**, then click **Apply** and close the **Preferences** window.
   ![02-vmw-network-setup-014.png](./images/02-vmw-network-setup/02-vmw-network-setup-014.png)