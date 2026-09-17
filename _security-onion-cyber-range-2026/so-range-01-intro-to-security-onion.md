---
layout: page
title: "Introduction to Security Onion (2026)"
nav_order: 21
parent: "Operating a Cyber Range with Security Onion—Windows 11, 2026"
---

# Using Security Onion and the Security Onion Console
{: .no_toc }

- TOC
{:toc}

This section provides a basic overview of how to start using Security Onion. Security Onion does a lot, hopefully I can show you some of those things across these pieces. This section provides a quick introduction to the virtual machine's command line and the Security Onion Console. There are also some steps on how to completing configuration by specifying your **HOME_NET** network, testing Security Onion's ability to detect traffic, and updating Security Onion.

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

If you prefer to use SSH keys for authentication, you can add your SSH key pair to the Security Onion VM so you can log in without using a password. On Linux, you add your SSH public key to the VM and then log in using these commands.

1. `$ ssh-copy-id -i ~/.ssh/<public-key-name>.pub <username>@<management-network-ip-address>`
2. Enter your password.
3. Once your SSH public key has been added to the VM, you can log in with ssh -i ~/.ssh/<public-key-name> <username>@<management-network-ip-address>`

##### SSH Key Authentication: Windows 11

To copy your SSH public key from a Windows computer to your Security Onion VM, use this equivalent version of `ssh-copy-id` for Windows:  
1. type $env:USERPROFILE\.ssh\<public-key-name>.pub | ssh <username>@<management-network-ip-address> "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"
2. Enter your password.
3. Once your SSH public key has been added to the VM, you can log in with `ssh -i $env:USERPROFILE\.ssh\<public-key-name> <username>@<management-network-ip-address>`.

## Security Onion Console: First Look

1. To start Security Onion for the first time, click the play icon in the VMware Workstation Pro menu bar. (You can also select the **VM** (Virtual Machine) menu and click **Power on this virtual machine**.)
   ![](/assets/images/security-onion-cyber-range-2026/so-range-01/so-range-01-001.png)

   * **Note:** You will also want at least the OPNsense VM running; at this time running the Kali or Metasploitable VMs is optional.

2. When you boot Security Onion after installation, you will see the login prompt with the hostname you gave to the system. Enter the Linux system credentials that you set for the VM during initial installation.
   ![](/assets/images/security-onion-cyber-range-2026/so-range-01/so-range-01-002.png)
3. When you successfully log in, a banner displays the URL to use for accessing the Security Onion Console on the management network. Type `sudo so-status` and enter your password to determine the status of Security Onion.
   ![](/assets/images/security-onion-cyber-range-2026/so-range-01/so-range-01-003.png)
4. When I first run this command, I get the output `System appears to be starting. No highstate has completed since the system was restarted.` This is the SaltStack application setting up the VM. Without getting into it too much, SaltStack is an application that can configure and orchestrate complicated application deployments. Security Onion uses it to manage its many container-based services. The `salt-master` communicates the target state of the environment to the different `salt-minions`. This could be spread across multiple hosts in a complex environment, but here I have a single, standalone Security Onion VM, so the salt-master and salt-minion are working on the same host.
   ![](/assets/images/security-onion-cyber-range-2026/so-range-01/so-range-01-004.png)

   {: .note }
   When you first boot Security Onion, it can take a long time for SaltStack to complete its configuration and bring up all of the Security Onion services. When I reviewed the logs after it ran the first time to create this content, it took about 45 minutes. You can follow along from the command line with `journalctl -u salt-minion -f`.

5. Run `so-status` again, either `sudo so-status` or switch to the root user with `sudo su -` and then run `so-status`. The output is a color-coded breakdown of all the Docker containers that make up Security Onion.
   ![](/assets/images/security-onion-cyber-range-2026/so-range-01/so-range-01-005.png)
4. Open your browser of choice and enter the URL from the login banner and enter it into the browser. Check the address bar to make sure that the URL starts with `https://`.
   ![](/assets/images/security-onion-cyber-range-2026/so-range-01/so-range-01-006.png)
5. Your browser will display a self-signed certificate warning (**NET::ERR_CERT_AUTHORITY_INVALID**). Click **Advanced**.
   ![](/assets/images/security-onion-cyber-range-2026/so-range-01/so-range-01-007.png)
6. Click **Proceed to \<Security-Onion-URL\> (Risky)**.
   ![](/assets/images/security-onion-cyber-range-2026/so-range-01/so-range-01-008.png)
7. Enter the email address and password that you entered during Security Installation configuration on the **Login to Security Onion** page and click **Login**.
   ![](/assets/images/security-onion-cyber-range-2026/so-range-01/so-range-01-009.png)
8. The Security Onion **Overview** page loads with some introductory text about using and customizing Security Onion. In the left sidebar are links to itself as well as:
   ![](/assets/images/security-onion-cyber-range-2026/so-range-01/so-range-01-010.png)

   * **Onion AI:** This is a premium feature sold by the creator of Security Onion, [Security Onion Solutions](https://securityonionsolutions.com){:target="_blank"}.
   ![](/assets/images/security-onion-cyber-range-2026/so-range-01/so-range-01-onion-ai.png)
   * The **Alerts** generated from Suricata rules.
   ![](/assets/images/security-onion-cyber-range-2026/so-range-01/so-range-01-alerts.png)   
   * A **Dashboards** page for creating your own visualizations of Security Onion data.
   ![](/assets/images/security-onion-cyber-range-2026/so-range-01/so-range-01-dashboards.png)
   * The **Hunt** page, where you can compare different events as part of investigations and incident response.
   ![](/assets/images/security-onion-cyber-range-2026/so-range-01/so-range-01-hunt.png)
   * The **Cases** page. "Cases" are events that you can create when browsing the **Alerts**, **Dashboard**, or **Hunt** pages.
   ![](/assets/images/security-onion-cyber-range-2026/so-range-01/so-range-01-cases.png)
   * The **Detections** page allows you to manage the detection engineering rules running in Security Onion. These include the network events in Suricata, Sigma rules used by ElastAlert, and file-scanning rules used by a tool called Strelka.
   ![](/assets/images/security-onion-cyber-range-2026/so-range-01/so-range-01-detections.png)
   * The **PCAP** page for capturing and replaying packet captures (PCAPs).
   ![](/assets/images/security-onion-cyber-range-2026/so-range-01/so-range-01-pcap.png)
   * The **Grid** page lets you check the operational status of the Security Onion and its components. In this series, I only have a single host, or a "standalone deployment." When there are Security Onion hosts, that's a distributed deployment.
   ![](/assets/images/security-onion-cyber-range-2026/so-range-01/so-range-01-grid.png)
   * The **Downloads** page contains links to download Elastic Agent installers which are ready to be installed on the hosts covered by your Security Onion deployment.
   ![](/assets/images/security-onion-cyber-range-2026/so-range-01/so-range-01-downloads.png)
   * The **Administration** page is where you can manage user accounts to access the Security Onion Console.
   ![](/assets/images/security-onion-cyber-range-2026/so-range-01/so-range-01-admin-users-1.png)
   * Additional **Tools** that extend what you can do with Security Onion:

      * A **Kibana** instance that provides security information and event management (SIEM) functionality.
      ![](/assets/images/security-onion-cyber-range-2026/so-range-01/so-range-01-kibana-so-home.png)
      * The **Elastic Fleet** link takes you to a Kibana page where you can manage the different components of your Elastic deployment, such as the agents installed on hosts that send log data to the Elastic server and the Elastic server itself.
      ![](/assets/images/security-onion-cyber-range-2026/so-range-01/so-range-01-kibana-fleet.png)
      * The **Osquery Manager** link takes you to another Kibana page where you can manage an integration with feature that integrates [osquery](https://osquery.readthedocs.io/en/stable/){:target="_blank"}, which "allows you to write SQL queries to explore operating system data." The individual Elastic Agents in your fleet can use osquery to check the states of the hosts they are installed on.
      ![](/assets/images/security-onion-cyber-range-2026/so-range-01/so-range-01-kibana-osqueries.png)
      * **InfluxDB** is an observability tool that provides visualizations of the state of your Security Onion system, with near-real-time reporting of both high-level and very granular system properties, as well as other statistics, such as network activity.
      ![](/assets/images/security-onion-cyber-range-2026/so-range-01/so-range-01-influxdb.png)
      * **CyberChef** is an open-source project from Britain's GCHQ, that describes itself as "The Cyber Swiss Army Knife -- a web app for encryption, encoding, compression and data analysis."
      ![](/assets/images/security-onion-cyber-range-2026/so-range-01/so-range-01-cyber-chef.png)
      * **Navigator** provides you with an interactive version of the MITRE ATT&CK Framework that you can use as an information resource when investigating incidents.
      ![](/assets/images/security-onion-cyber-range-2026/so-range-01/so-range-01-attck-navigator.png)

As you can see, Security Onion has a lot of features, and there are lots of different ways to use them.

First, you need to complete a few more configuration tasks. 

## Security Onion Configuration: Set Home Networks

As described in [Create VMware Private Virtual Networks for the Security Onion Environment](({% link _security-onion-cyber-range-2026/so-range-01-intro-to-security-onion.md %})), you designed this environment with a simulated local-area network (LAN) called HOME_NET_LAN, with an IP address space of 10.10.10.0/24. Now you need to specify this network as the HOME_NET that Suricata and Zeek are monitoring and defending. You used to declare this network as part of the initial configuration process for Security Onion, but now you can do it through the Security Onion Console.

1. In the Security Onion Console, click the **Administration** link in the left sidebar, then click **Configuration**. Under Analyst Quick Links > Suricata, click Suricata Home Networks.
   ![](/assets/images/security-onion-cyber-range-2026/so-range-01/so-range-01-011.png)
2. The HOME_NET variable setting is under **suricata > config > vars > address-groups > HOME_NET**. By default HOME_NET is set to the RFC 1918 Class A, B, and C private networks. 
   ![](/assets/images/security-onion-cyber-range-2026/so-range-01/so-range-01-012.png)
3. We only need Security Onion to monitor a relatively small part of the Class A network, and since we already declared our EXTERNAL_NET_LAN to be a part of that same CIDR block, it is best to specify that. In the **Current Grid Value** text field, enter **10.10.10.0/24**.
   ![](/assets/images/security-onion-cyber-range-2026/so-range-01/so-range-01-013.png)
4. You can click the ** ** drop-down menu, but you will see there is only one option, **onion2026 (standalone)** *and clicking on it won't do anything*.
   ![](/assets/images/security-onion-cyber-range-2026/so-range-01/so-range-01-014.png)
5. Hold the pointer over the green check mark and you will see **Save changes** tooltip text. Click the green check mark.
   ![](/assets/images/security-onion-cyber-range-2026/so-range-01/so-range-01-015.png)
6. A blue banner will display across the top of the **Configuration** pane stating that **New changes are ready to be applied to the suricata module...**. Click **Synchronize Suricata**.
   ![](/assets/images/security-onion-cyber-range-2026/so-range-01/so-range-01-016.png)
7. As the changes synchronize, a Security Onion icon progress indicator displays in the center of the screen. Click **Configuration**.
   ![](/assets/images/security-onion-cyber-range-2026/so-range-01/so-range-01-017.png)
8. Under **Analyst Quick Links**, click **Zeek Home Networks** under **Zeek**.
   ![](/assets/images/security-onion-cyber-range-2026/so-range-01/so-range-01-018.png)
9. The HOME_NET variable setting is under **zeek > config > networks > HOME_NET**. Just like Suricata, **HOME_NET** is set to the RFC 1918 networks. 
   ![](/assets/images/security-onion-cyber-range-2026/so-range-01/so-range-01-019.png)
10. In the **Current Grid Value** text field, enter the same value that you set for the Suricata HOME_NET, **10.10.10.0/24** and click the check mark icon to save changes.
   ![](/assets/images/security-onion-cyber-range-2026/so-range-01/so-range-01-020.png)
11. A blue banner will display across the top of the **Configuration** pane stating that **New changes are ready to be applied to the zeek module...**. Click **Synchronize Zeek**. 
   ![](/assets/images/security-onion-cyber-range-2026/so-range-01/so-range-01-021.png)

## Test Security Onion Detections

When you first start using your Security Onion deployment, there will be little or no event data. What exists might be for the VM's operating system. When I created this page, Security Onion's Alert page had no events.
![](/assets/images/security-onion-cyber-range-2026/so-range-01/so-range-01-022.png)

Security Onion provides a test function that you can run from the command line.. Run the command `so-test` from the command line of the Security Onion VM. This creates a `tcpreplay` container that simulates traffic in the environment. 

1. Run the command `so-test` from the command line of the Security Onion VM.

   ```bash
   [onion@onion2026 ~]$ sudo so-test
   Replay functionality not enabled; attempting to enable now (may require Internet access)...

   Pulling so-tcpreplay image
   =========================================================================
   Starting tcpreplay...

   This could take a while if another Salt job is running.
   Run this command with --force to stop all Salt jobs before proceeding.
   =========================================================================
   local:
   ----------
            ID: so-tcpreplay
      Function: docker_container.running
   ```

2. When the `so-test` process is complete, the output ends with:

   ```bash
   Statistics for network device: bond0
         Successful packets:        55748
         Failed packets:            0
         Truncated packets:         0
         Retried packets (ENOBUFS): 0
         Retried packets (EAGAIN):  0
   Replay completed. Warnings shown above are typically expected.
   [onion@onion2026 ~]$
   ```

3. Reload the **Alert** page in Security Onion. The simulated Alert events generated by `so-test` display. Select an event to look at and click its right-facing arrow (`>`) to twirl it down.
   ![](/assets/images/security-onion-cyber-range-2026/so-range-01/so-range-01-023.png)
4. When you open an alert, there are two tabs. The first is the **Alert Details**, which provides you with all of the metadata about the alert. This is basically presenting the JSON data you would see in a Kibana search in a format that is more readable to the casual user. There is also an **Overview** in the right sidebar that provides a **Summary** of the action detected.
   ![](/assets/images/security-onion-cyber-range-2026/so-range-01/so-range-01-024.png)
5. You can also click on the **Guided Analysis** tab to see some AI-generated summaries that answer some basic questions about potentially malicious activity.
   ![](/assets/images/security-onion-cyber-range-2026/so-range-01/so-range-01-025.png)
6. If you click Dashboards in the left sidebar, you will see that the default dashboard visualizations are now populated with event data from `so-test`.
   ![](/assets/images/security-onion-cyber-range-2026/so-range-01/so-range-01-026.png)
7. You can also see the same event data in Kibana. Click **Kibana** in the left sidebar.
   ![](/assets/images/security-onion-cyber-range-2026/so-range-01/so-range-01-027.png)
8. Your browser will open a new tab or window with an Elastic login screen. Enter the same credentials you used to log in to the Security Onion Console and click **Log in**.
   ![](/assets/images/security-onion-cyber-range-2026/so-range-01/so-range-01-028.png)
9. Click **Alert** under **Event Category** in the **Navigation** widget on the Kibana home page, which you will notice is now populated with some of the events generated by `so-test`.
   ![](/assets/images/security-onion-cyber-range-2026/so-range-01/so-range-01-029.png)
10. You can see the same events from the **Alerts** page on the **Security Onion - Alerts** page in Kibana.
   ![](/assets/images/security-onion-cyber-range-2026/so-range-01/so-range-01-030.png)

If all of this works, you have demonstrated that your Security Onion deployment can detect network activity, analyze it, identify potenitally malicious activity, and feed that data into the various analytical tools that make up Security Onion. You can now start creating events yourself with your other virtual machines.

## Updating Security Onion

Security Onion is actively developed and maintained and makes updates available to users frequently. The update process, called `soup` for Security Onion UPdater, is executed from the command line.

1. Access the command line through the VMware console or over SSH.
2. Type `sudo soup` and press `Enter`. You can also `sudo soup -y` for the update to proceed unattended, where it answers yes to any prompt.
3. You will see a lot of output as `soup` performs a series of pre-update checks, then downloads packages and container images and installs and starts them. An update can take 20 minutes or longer depending on which version you currently have and what Security Onion is updating.

## Clear Security Onion Event Data

Since you ran test data, you may want to reset or clear the event data in Security Onion for when you start simulating your own attacks on the netowrk. You can reset the logs and logging configurations of your Security Onion instance by running these two commands:

```
sudo so-nsm-clear -h
sudo so-elastic-clear -h
```

{: .note }
After completing your introduction to Security Onion, completing configuration, and running `soup`, consider taking a snapshot of your virtual machine.