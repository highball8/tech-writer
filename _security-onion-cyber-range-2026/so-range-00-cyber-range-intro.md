---
layout: page
title: "Operating a Cyber Range with Security Onion—Windows 11, 2026"
nav_order: 20
has_children: true
---

# Operating a Cyber Range with Security Onion—--Windows 11, 2026

In both the [Security Onion: Creating a Virtual Lab Environment---Windows 11, 2026]({% link _security-onion-series-win11-2026/so-00-tutorial-intro-win11-2026.md %}) and [Security Onion: Creating a Virtual Lab Environment---macOS, 2022]({% link _security-onion-series-macos-2022/so-00-tutorial-intro-macos-2022.md %}) series, I explained how you can create a virtualized lab environment, or cyber range, monitored by Security Onion using VMware desktop virtualization software. 

While those tutorials mayu have taught you a lot about how to create and manage virtual machines and virtual networks, there's not a lot in there about the whole purpose of the lab: the "cyber range" part. This tutorial will introduce you to how to start using Security Onion, and then I will demonstrate a couple of exercises using the Kali virtual machine to reconnoiter and attack the Metasploitable virtual machines, introducing you to tools like [Nmap](https://nmap.org/){:target="_blank"}, [Metasploit](https://www.metasploit.com/){:target="_blank"}, [BurpSuite](https://portswigger.net/burp){:target="_blank"}, and [Zap](https://www.zaproxy.org/){:target="_blank"}. Then you can go full circle by using Security Onion's capabilities to review alerts and log data of that activity to see it through a defender's eyes.

I'm going to start with an [Introduction to Security Onion (2026)]({% link _security-onion-cyber-range-2026/so-range-00-cyber-range-intro.md %}), showing you how to access Security Onion via SSH or through the web management interface and exploring its features.