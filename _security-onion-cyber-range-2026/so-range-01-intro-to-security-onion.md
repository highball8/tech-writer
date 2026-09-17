---
layout: page
title: "Introduction to Security Onion (2026)"
nav_order: 21
parent: "Operating a Cyber Range with Security Onion--—Windows 11, 2026"
---

# Using Security Onion and the Security Onion Console
{: .no_toc }

1. TOC
{:toc}

This section provides a basic overview of how to start using Security Onion. Security Onion does a lot, hopefully I can show you some of those things across these pieces. This section provides a quick introduction to the Security Onion Console ~~~and in particular its **Alerts** page and how to use it~~~.

## Interacting With Security Onion and the Security Onion Console

Now that you have installed Security Onion and connected it to the HOME_NET_LAN network to monitor traffic, it's time to boot it up, log in to the Security Onion Console from the management network, and start to learn how to use it.

You interact with Security Onion in two ways: through the command line of the Linux virtual machine (VM), and through your web browser using the Security Onion Console. In both cases, you are connecting to the VM's network adapter that you assigned for the "management network." In this case, I connected it to VMware Workstation Pro's NAT network.

### Accessing the Security Onion Virtual Machine's Command Line Interface

There are two ways to access the command line:

* Using the VMware Workstation Pro console window (which I have used throughout these tutorials).
* By connecting to the VM using SSH, the Secure Shell protocol. In my case, I do that on the Windows host machine using the IP address of the Security Onion VM network on the NAT network (the management network). To do so, you need the IP address of the VM on the management network and the credentials you created for the VM during initial installation.

#### Log in Using SSH

  1. `$ ssh <username>@<management-network-ip-address>`
  2. Enter your password.

{: .important }
* On Linux or macOS host machines, an SSH client is installed by default.
* On Windows, SSH may or may not be installed. Open PowerShell and run this command to check:\
`Get-WindowsCapability -Online | Where-Object Name -like 'OpenSSH.Client*'`
  * It will return `State: Installed` if SSH is installed. If not, use this PowerShell command to install it: `Add-WindowsCapability -Online -Name OpenSSH.Client~~~~0.0.1.0`.

##### SSH Key Authentication: Linux

If you prefer to use SSH keys for authentication, you can add your SSH key pair to the Security Onion VM so you can log in without using a password. On Linux, you add your SSH public key to the VM using these commands.

1. `$ ssh-copy-id -i ~/.ssh/<public-key-name>.pub <username>@<management-network-ip-address>`
2. Enter your password.

##### SSH Key Authentication: Windows 11

This is the equivalent version of ``ssh-copy-id` for Windows:  
1. type $env:USERPROFILE\.ssh\<public-key-name>.pub | ssh <username>@<management-network-ip-address> "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"

## Start Using Security Onion and the Security Onion Console

1. To start Security Onion for the first time, click the play icon in the VMware Workstation Pro menu bar. (You can also select the **VM** (Virtual Machine) menu and click **Power on this virtual machine**.)
   ![](/assets/images/security-onion-cyber-range-2026/so-range-01/so-range-01-001.png)

   * **Note:** You will also want at least the OPNsense VM running; at this time running the Kali or Metasploitable VMs is optional.

2. When you boot Security Onion after installation, you will see the login prompt with the hostname you gave to the system. Enter the Linux system credentials that you set for the VM during initial installation.
   ![](/assets/images/security-onion-cyber-range-2026/so-range-01/so-range-01-002.png)
3. When you successfully log in, a banner displays the URL to use for accessing the Security Onion Console on the management network. Type `sudo so-status` and enter your password to determine the status of Security Onion.
   ![](/assets/images/security-onion-cyber-range-2026/so-range-01/so-range-01-003.png)
4. When I first run this command, I get the output `System appears to be starting. No highstate has completed since the system was restarted.` This is the SaltStack application setting up the VM. Without getting into it too much, SaltStack is an application that can configure and orchestrate complicated application deployments. Security Onion uses it to manage its many container-based services. The `salt-master` communicates the target state of the environment to the different `salt-minions`. This could be spread across multiple hosts in a complex environment, but here I have a single, standalone Security Onion VM, so the salt-master and salt-minion are working on the same host.
   ![](/assets/images/security-onion-cyber-range-2026/so-range-01/so-range-01-004.png)

   * **Note:** When you first boot Security Onion, it can take a long time for SaltStack to complete its configuration and bring up all of the Security Onion services. When I reviewed the logs after it ran the first time, it took about 45 minutes. You can follow along from the command line with `journalctl -u salt-minion -f`.

5. Now run `so-status` again, either `sudo so-status` or switch to the root user with `sudo su -` and then run `so-status`. The output is a color-coded breakdown of all the Docker containers that make up Security Onion.
   ![](/assets/images/security-onion-cyber-range-2026/so-range-01/so-range-01-005.png)
4. Open your browser of choice and enter the URL from the login banner and enter it into the browser. Check the address bar to make sure that the URL starts with `https://`.
   ![](/assets/images/security-onion-cyber-range-2026/so-range-01/so-range-01-006.png)
5. Your browser will display a self-signed certificate warning (**NET::ERR_CERT_AUTHORITY_INVALID**). Click **Advanced**.
   ![](/assets/images/security-onion-cyber-range-2026/so-range-01/so-range-01-007.png)
6. Click **Proceed to \<Security-Onion-URL\>**.
   ![](/assets/images/security-onion-images-macos-2022/07-onion-intro-macos-2022/07-onion-intro-macos-2022-008.png)
7. Enter the email address and password that you entered during Security Installation configuration on the **Login to Security Onion** page and click **Login**.
   ![](/assets/images/security-onion-images-macos-2022/07-onion-intro-macos-2022/07-onion-intro-macos-2022-007.png)
8. The Security Onion **Overview** page loads with some introductory text about Security Onion and how to customize this page. In the left sidebar are links to:
   ![](/assets/images/security-onion-images-macos-2022/07-onion-intro-macos-2022/07-onion-intro-macos-2022-008.png)

   * The **Overview** page.
   * The **Alerts** page where you can review detections on your network.
   * A **Dashboards** page for visualizing Security Onion data.
   * The **Hunt** page, where you can compare different events as part of investigations and incident response.
   * The **Cases** page. "Cases" are events that you can create when browsing the **Alert**, **Dashboard**, or **Hunt** pages.
   * The **PCAP** page for capturing and replaying packet captures (PCAPs).
   * The **Grid** page lets you check the operational status of the Security Onion host (in a standalone deployment) or all of your Security Onion hosts (in a distributed deployment).
   * The **Downloads** page
   * The **Administration** page is where you can manage user accounts to access the Security Onion Console.
   * Additional **Tools** that extend what you can do with Security Onion:

      * A **Kibana** instance that provides security information and event management (SIEM) functionality.
      * **Grafana** provides visualizations of the state of your Security Onion system, with near-real-time reporting of both high-level and very granular system properties, as well as other statistics, such as network activity.
      * **CyberChef** is an open-source project from Britain's GCHQ, that describes itself as "The Cyber Swiss Army Knife -- a web app for encryption, encoding, compression and data analysis."
      * **Playbook** is a tool that allows you "to create a Detection Playbook, which itself consists of individual Plays. These Plays are fully self-contained and describe the different aspects around a particular detection strategy."
      * **FleetDM** is a tool that "asks questions about your servers, containers, and laptops running Linux, Windows, and macOS."
      * **Navigator** lets you walk through the steps of an attack using the MITRE ATT&CK Framework.

9. Click **Alerts**.
   ![](/assets/images/security-onion-images-macos-2022/07-onion-intro-macos-2022/07-onion-intro-macos-2022-009.png)
10. The **Alerts** page loads with a table of events that it has detected. Since this is a fresh install on a network with no traffic, all of these alerts are related to the Security Onion VM itself and are rated as having a low severity. 
   ![](/assets/images/security-onion-images-macos-2022/07-onion-intro-macos-2022/07-onion-intro-macos-2022-010.png)
11. Each individual alert type is grouped by its name, and also by the module, or the detection engine. In this case, the **event.module** for all alerts is **ossec**. These events are being detected by another piece of software that Security Onion leverages called Wazuh, a host-based intrusion detection system. (The name **ossec** refers to a Wazuh predecessor, OSSEC.) This means Wazuh is installed on our Security Onion VM and is monitoring for potentially malicious activity.
   ![](/assets/images/security-onion-images-macos-2022/07-onion-intro-macos-2022/07-onion-intro-macos-2022-011.png)
12. As suggested by the severity level, these are all routine events. Hover over **sshd authentication success** (with a count of two alerts) and click its row.
   ![](/assets/images/security-onion-images-macos-2022/07-onion-intro-macos-2022/07-onion-intro-macos-2022-012.png)
13. A menu appears. Click **Drilldown**.
   ![](/assets/images/security-onion-images-macos-2022/07-onion-intro-macos-2022/07-onion-intro-macos-2022-013.png)
14. This table displays the individual alerts with the name **sshd authentication success**. Click the arrowhead to twirl down an individual event.
   ![](/assets/images/security-onion-images-macos-2022/07-onion-intro-macos-2022/07-onion-intro-macos-2022-014.png)
15. Scroll down the page to see all of the metadata that Wazuh collected and reported about this event. If you look at the message, you can see that this event was generated when I SSH'd into Security Onion from my host Mac using my SSH key for authentication.
   ![](/assets/images/security-onion-images-macos-2022/07-onion-intro-macos-2022/07-onion-intro-macos-2022-015.png)
16. Scroll back up to the top of the table. Notice the bubble that says **rule.name:"sshd: authentication success."**. This indicates that all the alerts you see are filtered by this rule name. Click the **x** to remove this filter.
   ![](/assets/images/security-onion-images-macos-2022/07-onion-intro-macos-2022/07-onion-intro-macos-2022-016.png)
17. When you see the **Alerts** table reload, it looks different. You see all of the individual rules, and the word **Ungroup** in the text field above. This is the query field where you can enter Security Onion queries to search through your alerts.
   ![](/assets/images/security-onion-images-macos-2022/07-onion-intro-macos-2022/07-onion-intro-macos-2022-017.png)
18. If you click the down arrow next to the query field, you will see several predefined queries, including the default one that was selected when you first came to the **Alerts** page, **Group by Name, Module**. Select this query.
   ![](/assets/images/security-onion-images-macos-2022/07-onion-intro-macos-2022/07-onion-intro-macos-2022-018.png)
19. You are back where you started, with several uninteresting alerts. In the next article, we are going to try and generate our own, more interesting, alerts using the Kali VM to generate malicious traffic for Security Onion to detect.
   ![](/assets/images/security-onion-images-macos-2022/07-onion-intro-macos-2022/07-onion-intro-macos-2022-019.png)
