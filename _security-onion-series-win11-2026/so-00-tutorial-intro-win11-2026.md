---
layout: page
title: "Security Onion: Creating a Virtual Lab Environment—Windows 11, 2026"
nav_order: 10
has_children: true
---

# Security Onion: Creating a Virtual Lab Environment---Windows 11, 2026

{: .important }
This is an updated version of my original tutorial about how to set up a virtualized lab environment monitored by Security Onion. You can see the original version from 2022, which uses macOS and VMware Fusion Pro, at [Security Onion Virtual Lab Tutorial: Introduction (MacOS, 2022)]({% link _security-onion-series-macos-2022/so-00-tutorial-intro-macos-2022.md %}).

This series of how-to articles walks you through how to set up your own virtual lab for information security research using virtual machines (VMs). I am using [VMware Workstation Pro](https://www.vmware.com/products/desktop-hypervisor/workstation-and-fusion){:target="_blank"}, which is a Type 2 hypervisor used for desktop virtualization on host operating systems running Windows.

The centerpiece of the lab is a virtual machine (VM) running [Security Onion](https://securityonionsolutions.com/){:target="_blank"}, which is an open-source network intrusion detection system (NIDS) and network security monitor (NSM). Security Onion uses containers to give users a wide variety of tools that allow for network monitoring and alerting, threat hunting, and more. It utilizes well-known, widely used open-source applications, including:

* [Zeek](https://docs.zeek.org/en/master/about.html){:target="_blank"} (formerly known as Bro) analyzes traffic on the network, collects metadata about that traffic and logs all of it, making it a powerful tool for network detection and forensics.
* [Suricata](https://suricata.readthedocs.io/en/suricata-6.0.5/what-is-suricata.html){:target="_blank"} is a signature-based network intrusion detection system originally developed by the Open Information Security Foundation.
* The [ELK](https://www.elastic.co/what-is/elk-stack){:target="_blank"} stack, for Elasticsearch, Logstash, and Kibana. The ELK stack serves as a security information and event management (SIEM) platform, receiving events in Security Onion logs from Logstash (as well as Filebeat). Elasticsearch is the search and analytics engine. Kibana is a user-interface and visualization tool.

Security Onion is set up to monitor a private network using a network interface card (NIC) that works in promiscuous mode to "sniff" all the traffic traversing the network. In practice this can be done by connecting Security Onion to a SPAN or TAP port. Since I am creating my environment virtually on my MacBook Pro, I will need to create some network infrastructure that will allow me to sniff traffic with Security Onion.

The basic components of my virtual lab will be:

* A virtual machine running [OPNsense](https://docs.opnsense.org/intro.html){:target="_blank"}, an open-source firewall and networking platform. I will use the OPNsense VM as a virtual router to create isolated virtual networks within VMware Workstation Pro, including a local area network (LAN) that the other lab virtual machines will connect to. OPNsense provides the LAN so that these virtual machines can talk to each other, and it can also connect them to the wide area network (WAN), or public internet, for things like updates. Using OPNsense also gives me the ability to connect Security Onion to the LAN and sniff traffic.
* A virtual machine running Security Onion. This tutorial will go over how to set up a Security Onion deployment that monitors the virtual lab and some basics on what Security Onion does and how to use it. Then we will create some malicious traffic on the network and see if Security Onion detects it.
* A [Kali Linux](https://www.kali.org/){:target="_blank"} virtual machine. I'm going to use Kali as an endpoint on the network that I can use to monitor and manage the network and interact with it. But the primary use of Kali Linux is for penetration testing and other security research, so I will also be using Kali to reconnoiter and attack other virtual machines on the network, generating traffic that Security Onion will identify as malicious.
* Target virtual machines. I will start with [Metasploitable 3](https://github.com/rapid7/metasploitable3){:target="_blank"} VMs running both Ubuntu and Windows Server 2008. I may also use [Metasploitable 2](https://sourceforge.net/projects/metasploitable/){:target="_blank"}. These are virtual machines that intentionally include many security vulnerabilities that can be exploited with tools in Kali such as [Metasploit](https://www.metasploit.com/){:target="_blank"}.

## Overview

This set of how-to articles will make up a tutorial on everything I needed to do to create a Security Onion-monitored virtual lab on a Windows computer. Just that part itself is a considerable amount of work... and it doesn't always work for me. I think the articles provide good lessons on a variety of skills needed to administer virtual machines, manage a network, and more. Here's what the first articles will cover:

1. [Prepare OPNsense and Security Onion Installation Media]({% link _security-onion-series-win11-2026/so-01-prepare-media-win11-2026.md %}): Instructions on downloading and validating OPNsense and Security Onion and preparing them for installation in VMware Fusion Pro.

   * **Note:** Installation instructions for other VMs, like Kali or Metasploitable, are out of scope for this tutorial, but I hope to come back and cover them later.

2. [Create VMware Private Virtual Networks for the Security Onion Environment]({% link _security-onion-series-win11-2026/so-02-vmw-network-setup-win11-2026.md %}): Create a private virtual network within VMware Fusion Pro.
3. [Create the OPNsense Virtual Machine]({% link _security-onion-series-win11-2026/so-03-opn-sense-vm-creation-win11-2026.md %}): Create a virtual machine where you will install and configure OPNsense.
4. [Configure the OPNsense Virtual Machine]({% link _security-onion-series-win11-2026/so-04-opn-sense-config-win11-2026.md %}): Set up OPNsense and use it to create the routing capabilities you need for your private virtual network.
5. [Create the Security Onion Virtual Machine]({% link _security-onion-series-win11-2026/so-05-onion-vm-creation-win11-2026.md %}): Create a virtual machine where you will install and configure Security Onion.
6. [Configure the Security Onion Virtual Machine]({% link _security-onion-series-win11-2026/so-06-onion-config-win11-2026.md %}): Walk through Security Onion's installation wizard to deploy the tool.

## Prerequisites

This tutorial requires you to have some familiarity with and knowledge of desktop virtualization and the Linux and Windows command lines. I created the virtual lab for this tutorial using:

* **Host Computer:** A Lenovo ThinkStation P520 running Windows 11. At the time of writing, my ThinkStation has 64GB of RAM, which is a lot, but perhaps not enough to do this right. I've been exploring Security Onion since late 2020, and over that time its architecture has changed a lot. Depending on the deployment type, [Security Onion has a *minimum* RAM requirement of as much as 24GB](https://docs.securityonion.net/en/3/main/hardware/#minimum-specs){:target="_blank"}, so a virtual lab running Security Onion and the other VMs (OPNsense, Kali, Metasploitable) will be slow if your host machine running the VMs does not have the processor power and RAM.
* **Virtualization Platform:** [VMware Workstation Pro](https://www.vmware.com/products/desktop-hypervisor/workstation-and-fusion), a Type 2 hypervisor for Windows. When I started using virtual machines at home, I tried [VirtualBox](https://www.virtualbox.org/){:target="_blank"}, which is free, and [Parallels](https://www.parallels.com/){:target="_blank"}, which I paid for. I've had lots of problems with both. That could be my fault. But the $199 I paid for VMware Fusion Pro for my Mac was definitely worth it. VMs I create on Fusion Pro on a Mac or on Workstation Pro on a PC work so much faster and more reliably for me.

   {: .note }
   I started using VMware Fusion Pro for Mac in 2020, and have also used more professional-grade VMware virtualization products in the workplace. VMware generally set the standard for virtualization. Since its acquisition by Broadcom peoples' opinions have been changing about the VMware products, although both Workstation Pro and Fusion Pro are now free. I'm not sure what I think; the situation is certainly evolving.

* **Command-line Interface:** I use Windows PowerShell as my command-line interface on the Windows host machine.
* **Web Browser:** You will also need a web browser, both on the host operating system and in at least one of the VMs connected to the lab. I typically use [Firefox](https://www.firefox.com/){:target="_blank"}.

{: .note }
I use angle brackets (`<` and `>`) to enclose placeholder text for filenames, paths, URLs, software versions, or anything where the value may be different for you than it is for me.
