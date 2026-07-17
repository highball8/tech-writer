---
layout: page
title: "Create VMware Private Virtual Networks for the Security Onion Environment"
nav_order: 12
parent: "Security Onion: Creating a Virtual Lab Environment—macOS, 2022"
---

# Create VMware Private Virtual Networks for Your Lab
{: .no_toc }

{: .important }
I created this tutorial in mid-2022. In mid-2026 the content is over four years old and has accuracy and currency issues, particularly when it describes older versions of Security Onion and OPNsense. While this tutorial is no longer current, I am leaving it up because it is a professional writing sample that I put a lot of work into and it may still be useful to some readers. For more information, see [Security Onion: Creating a Virtual Lab Environment---macOS, 2022]({% link _security-onion-series-macos-2022/so-00-tutorial-intro-macos-2022.md %}).

1. TOC
{:toc}

These steps detail how you can use VMware Fusion Pro's networking capabilities to create two private virtual networks. You will connect your different virtual machines (VMs) to these networks so that the VMs can interact with one another, and reach out to the public internet to download updates, browse the internet, etc.

**Note:** Per [VMware's documentation](https://techdocs.broadcom.com/us/en/vmware-cis/desktop-hypervisors/fusion-pro/26H1/using-vmware-fusion/configuring-vmware-fusion/setting-fusion-preferences/creating-custom-networks/add-a-private-network-configuration.html){:target="_blank"}, "private virtual networks (vmnet) configurations... only allow communication between virtual machines and the host system."

## Private Virtual Network Overview and Topology

In this scenario you use the VMware's networking feature to create two private virtual networks:

* **EXTERNAL_NET_LAN**: This will be a private virtual network that you will connect a Kali VM to. The Kali VM will access the management web user interface of the OPNsense router. It is *also* the network that will ***simulate*** a public wide area network (WAN) from which the Kali VM will reconnoiter and attack the network monitored by the Security Onion deployment. In this tutorial, you assign this network the EXTERNAL_NET_LAN network an IP address range of **10.10.9.0/24**.
* **HOME_NET_LAN:** This private virtual network acts as the local-area network (LAN) that Security Onion will monitor. This network is assigned the IP address range of **10.10.10.0/24**. You will use that same address range when configuring Security Onion. We will connect virtual machines like Metasploitable to this network, where they can act as targets monitored by Security Onion.

Once you have created the private virtual networks, you will attach the virtual network adapters of the various virtual machines to these networks.

{: .note}
A note on the network names: I got the names **EXTERNAL_NET** and **HOME_NET** from one of the most important parts of Security Onion, the Suricata intrusion detection system (IDS). Suricata signature-based detection rules (which are, in turn, based on Snort, an earlier IDS), use `$EXTERNAL_NET` and `$HOME_NET` to establish traffic directionality---what is on the network that you manage and are seeking to monitor and detect is `$HOME_NET`. What is outside of your network is everything else, `$EXTERNAL_NET`. In many cases, malicious traffic needs to either come from or go to `$EXTERNAL_NET` for it to match a Suricata rule, which is why you need to declare both networks to build the lab environment.

* OPNsense router:

  * **Network Adapter:** Connects to the host MacBook Pro using **Bridged Networking** > **Autodetect** to provide a WAN interface so that your OPNsense VM can connect to the internet through the host operating system's internet connection.
  * **Network Adapter 2:** This will connect to the **EXTERNAL_NET_LAN** (10.10.9.0/24) subnet.
  * **Network Adapter 3:** This will connect to the **HOME_NET_LAN** (10.10.10.0/24) subnet.

* Security Onion network intrusion detection system:

  * **Network Adapter:** Connect to the host MacBook Pro using **Bridged Networking** > **Autodetect** so that you can access Security Onion via SSH and the Security Onion Console using your browser on your host Mac. Think of this as the "management network" connection.
  * **Network Adapter 2:** This network adapter acts as a "sniffer" interface and will connect to the **HOME_NET_LAN** (10.10.10.0/24) subnet to monitor traffic.

* Kali virtual machine:

  **Network Adapter:** This will connect to the **EXTERNAL_NET_LAN** (10.10.9.0/24) subnet. From here it can access the web management interface of OPNsense for network management, and also reconnoiter and launch attacks against hosts on **HOME_NET_LAN**.

* Metasploitable virtual machines and other "targets:"

  * **Network Adapter:** Any virtual machines that we want to practice attacks against will be connected to **HOME_NET_LAN**.

This diagram depicts the network components and topology that I am using in this scenario:
![This is a network diagram depicting the network described in this section.](/assets/images/security-onion-images-macos-2022/02-vmw-network-setup-macos-2022/network-diagram-1-macos-2022.png)

## Create the Private Virtual Networks

1. Open VMware Fusion, and then open its **Preferences**.
   ![](/assets/images/security-onion-images-macos-2022/02-vmw-network-setup-macos-2022/02-vmw-network-setup-macos-2022-001.png)
2. Within **Preferences**, click **Network**.
   ![](/assets/images/security-onion-images-macos-2022/02-vmw-network-setup-macos-2022/02-vmw-network-setup-macos-2022-002.png)
3. Click the padlock icon in the bottom-left corner of the **Network** window.
   ![](/assets/images/security-onion-images-macos-2022/02-vmw-network-setup-macos-2022/02-vmw-network-setup-macos-2022-003.png)
4. Enter the host machine's administrator password and click **OK**.
   ![](/assets/images/security-onion-images-macos-2022/02-vmw-network-setup-macos-2022/02-vmw-network-setup-macos-2022-004.png)
5. Click the plus icon (**+**) to create a private virtual network for your lab environment.
   ![](/assets/images/security-onion-images-macos-2022/02-vmw-network-setup-macos-2022/02-vmw-network-setup-macos-2022-005.png)
6. A network appears under **Custom** > **Private to my Mac**. The name will start with **vmnet**. Click the network name once so that the name becomes editable.
   ![](/assets/images/security-onion-images-macos-2022/02-vmw-network-setup-macos-2022/02-vmw-network-setup-macos-2022-006.png)
7. Name this network **HOME_NET_LAN**. Press `Enter` to set the name.
   ![](/assets/images/security-onion-images-macos-2022/02-vmw-network-setup-macos-2022/02-vmw-network-setup-macos-2022-007.png)
8. Enter a **Subnet IP**. I am using **10.10.10.0**. Leave the **Subnet Mask** as **255.255.255.0** and click **Apply**.
   ![](/assets/images/security-onion-images-macos-2022/02-vmw-network-setup-macos-2022/02-vmw-network-setup-macos-2022-008.png)
9. Clear the checkboxes for **Connect the host Mac to this network** (because I am trying to create an isolated network for the lab) and **Provide addresses on this network via DHCP** (because the OPNsense router will provide the DHCP service), then click **Apply**.
   ![](/assets/images/security-onion-images-macos-2022/02-vmw-network-setup-macos-2022/02-vmw-network-setup-macos-2022-009.png)
10. Click the plus icon (**+**) again to create a second private virtual network.
   ![](/assets/images/security-onion-images-macos-2022/02-vmw-network-setup-macos-2022/02-vmw-network-setup-macos-2022-010.png)
11. A new network that starts with start with **vmnet** appears under **Custom** > **Private to my Mac**. Click the network name once so that the name becomes editable.
   ![](/assets/images/security-onion-images-macos-2022/02-vmw-network-setup-macos-2022/02-vmw-network-setup-macos-2022-011.png)
12. Enter **EXTERNAL_NET_LAN** as the name for this network and press `Enter`.
   ![](/assets/images/security-onion-images-macos-2022/02-vmw-network-setup-macos-2022/02-vmw-network-setup-macos-2022-012.png)
13. Enter a **Subnet IP** value of **10.10.9.0**. Leave the **Subnet Mask** as **255.255.255.0**. Click **Apply**.
   ![](/assets/images/security-onion-images-macos-2022/02-vmw-network-setup-macos-2022/02-vmw-network-setup-macos-2022-013.png)
14. Clear the checkboxes for **Connect the host Mac to this network** and **Provide addresses on this network via DHCP**, then click **Apply** and close the **Preferences** window.
   ![](/assets/images/security-onion-images-macos-2022/02-vmw-network-setup-macos-2022/02-vmw-network-setup-macos-2022-014.png)