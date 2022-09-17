---
layout: page
title: 'Security Onion Virtual Lab Tutorial: Introduction'
permalink: /security-onion-series/security-onion-intro
nav_order: 10
has_children: true
---

# Security Onion Virtual Lab Tutorial: Introduction

This series of how-to articles walks you through how to set up your own virtual lab for information security research using virtual machines (VMs). I am using [VMware Fusion Pro](https://store-us.vmware.com/fusionpro_buy_new){:target="_blank"}, which is a Type 2 hypervisor used for desktop virtualization on host operating systems running macOS.

The centerpiece of the lab is a virtual machine (VM) running [Security Onion](https://securityonionsolutions.com/){:target="_blank"}, which is a leading open-source network intrusion detection system (NIDS) and network security monitor (NSM). Security Onion uses containers to give users a wide variety of tools that allow for network monitoring and alerting, threat hunting, and more. It utilizes well-known, widely used open-source applications, including:

* [Zeek](https://docs.zeek.org/en/master/about.html){:target="_blank"} (formerly known as Bro) analyzes traffic on the network, collects metadata about that traffic and logs all of it, making it a powerful tool for network detection and forensics.
* [Suricata](https://suricata.readthedocs.io/en/suricata-6.0.5/what-is-suricata.html){:target="_blank"} is a signature-based network intrusion detection system originally developed by the Open Information Security Foundation to replace an older IDS named Snort.
* The [ELK](https://www.elastic.co/what-is/elk-stack){:target="_blank"} stack, for Elasticsearch, Logstash, and Kibana. The ELK stack receives events in Security Onion logs from Logstash (as well as Filebeat). Elasticsearch is the search and analytics engine. Kibana is a user-interface and visualization tool.

Security Onion is set up on a private network with a network interface card (NIC) that works in promiscuous mode to "sniff" all of the traffic traversing the network. In practice this can be done by connecting Security Onion to a SPAN or TAP port. Since I am creating my environment virtually on my MacBook Pro, I will need to create some network infrastructure that will allow me to sniff traffic with Security Onion.

The basic components of my virtual lab will be:

* A virtual machine running [OPNsense](https://docs.opnsense.org/intro.html){:target="_blank"}, which is an open-source firewall and networking platform. I will use the OPNsense VM as a virtual router to create a local area network (LAN) that the other lab virtual machine will connect to. OPNsense provides the LAN so that these virtual machines can talk to each other, and it also connects them to the wide area network (WAN), or public internet, for things like updates. Using OPNsense also gives me the ability to connect Security Onion to the LAN and sniff traffic.
* A virtual machine running Security Onion. This tutorial will go over how to set up a Security Onion deployment that monitors the virtual lab and some basics on what Security Onion does and how to use it. Then we will create some malicious traffic on the network and see if Security Onion detects it.
* A [Kali Linux](https://www.kali.org/){:target="_blank"} virtual machine. I'm going to use Kali as an endpoint on the network that I can use to monitor the network and interact with it. But the primary use of Kali Linux is for penetration testing and other security research, so I will also be using Kali to reconnoiter and attack other virtual machines on the network, generating traffic that Security Onion should identify as malicious.
* Target virtual machines. I will start with [Metasploitable 3](https://github.com/rapid7/metasploitable3){:target="_blank"} VMs running both Ubuntu and Windows Server 2008. I am may also use [Metasploitable 2](https://sourceforge.net/projects/metasploitable/){:target="_blank"}. These are virtual machines that intentionally include many security vulnerabilities that can be exploited with tools in Kali such as Metasploit.

## Overview

The first set of how-to articles on this site will make up a tutorial on everything I needed to do to create my Security Onion-monitored virtual lab. Just that part itself is a considerable amount of work... and it doesn't always work for me. I think the articles provide good lessons on a variety of skills need to administer virtual machines, manage a network, and more. Here's what the first articles will cover:

1. [Prepare Your Installation Media]({% link security-onion-series/so-01-prepare-media.md %}): Some instructions on downloading and validating OPNsense and Security Onion and preparing them for installation in VMware Fusion Pro.

   * **Note:** Installation instructions for other VMs, like Kali or Metasploitable, are out of scope for this tutorial, but I hope to come back and cover them later.

2. [Create VMware Private Virtual Networks for Your Lab]({% link security-onion-series/so-02-vmw-network-setup.md %}): Create a private virtual network within VMware Fusion Pro.
3. [Create the OPNsense Virtual Machine]({% link security-onion-series/so-03-opn-sense-vm-creation.md %}): Create a virtual machine where you will install and configure OPNsense.
4. [Configure the OPNsense Virtual Machine]({% link security-onion-series/so-04-opn-sense-config.md %}): Set up OPNsense and use it to create the routing capabilities you need for your private virtual network.
5. [Create the Security Onion Virtual Machine]({% link security-onion-series/so-05-onion-vm-creation.md %}): Create a virtual machine where you will install and configure Security Onion.
6. [Configure the Security Onion Virtual Machine]({% link security-onion-series/so-06-onion-config.md %}): Walk through Security Onion's installation wizard.
7. [Start Using Security Onion and the Security Onion Console]({% link security-onion-series/so-07-onion-intro.md %}): Get to know Security Onion and some of its features through its web management interface and by using the command line.

## Prerequisites

This tutorial requires you to have some familiarity with and knowledge of desktop virtualization and the Linux command line. I created the virtual lab for this tutorial using:

* A 2016 MacBook Pro running macOS 12.4. This is a very powerful laptop, but it's probably not enough to do this right. Security Onion has a *minimum* RAM requirement of 12GB; my whole laptop only has 16GB, so a virtual lab running Security Onion and the other VMs (OPNsense, Kali, Metasploitable) will be slow if your host machine running the VMs does not have the processor power and RAM.
* [VMware Fusion Pro](https://store-us.vmware.com/fusionpro_buy_new). I've played around with [VirtualBox](https://www.virtualbox.org/){:target="_blank"}, which is free, and [Parallels](https://www.parallels.com/){:target="_blank"}, which I have paid for. I've had lots of problems with both. That could be my fault. But the $199 I paid for VMware Fusion Pro was definitely worth it. VMs I create in Fusion Pro work so much faster and more reliably for me.
* I use [ITerm2](https://iterm2.com/){:target="_blank"} with Zsh for the terminal on my MacBook Pro host machine.
* You will also need a web browser, both on the host operating system and in at least one of the VMs connected to the lab.
