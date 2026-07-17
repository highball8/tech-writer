---
layout: page
title: "Prepare OPNsense and Security Onion Installation Media"
nav_order: 11
parent: "Security Onion: Creating a Virtual Lab Environment—Windows 11, 2026"
---

# Prepare OPNsense and Security Onion Installation Media
{: .no_toc }

1. TOC
{:toc}

In this tutorial you will create two virtual machines (VMs): one OPNsense VM to provide routing for virtualized lab networks, and one VM to run Security Onion. On this page you are going to download the installation media needed to create those VMs and verify that the installation media is valid.

## Download, Validate, and Prepare the OPNsense Installation Media

1. Open a browser and go to [OPNsense's download page](https://opnsense.org/download/){:target="_blank"}.
   ![](/assets/images/security-onion-images-win11-2026/01-iso-prep-win11-2026/01-iso-prep-win11-2026-001.png)
2. Use the drop-down menus to select your processor's **System architecture** and the **image type**. Select **amd64** as the architecture and **dvd** as the media image type.
   ![](/assets/images/security-onion-images-win11-2026/01-iso-prep-win11-2026/01-iso-prep-win11-2026-002.png)
3. Scroll down the page and select the OPNsense **Mirror Location** where you want to download your media from. 
   ![](/assets/images/security-onion-images-win11-2026/01-iso-prep-win11-2026/01-iso-prep-win11-2026-003.png)

   * You can also scroll down the page to see the full list of mirror sites:
   ![](/assets/images/security-onion-images-win11-2026/01-iso-prep-win11-2026/01-iso-prep-win11-2026-004.png)

   * If you click the link for one of the mirror sites, you will see all of the files available for download, including the different architectures, image types, and signature files to verify the media.
   ![](/assets/images/security-onion-images-win11-2026/01-iso-prep-win11-2026/01-iso-prep-win11-2026-005.png)

4. After selecting each option, click the **Download OPNsense** button.
   ![](/assets/images/security-onion-images-win11-2026/01-iso-prep-win11-2026/01-iso-prep-win11-2026-006.png)
5. Move these files from your local machine's download folder into their own folder. In this series I am going to put my installation media in a folder called **onion-isos**.
   ![](/assets/images/security-onion-images-win11-2026/01-iso-prep-win11-2026/01-iso-prep-win11-2026-007.png)
6. Next I will check that the has on the file matches what is on the OPNsense downloads page. Open a command line application. In this case I am using PowerShell, which I can open by typing **powershell** in the search bar in the taskbar and then clicking **Windows PowerShell** in the results.
   ![](/assets/images/security-onion-images-win11-2026/01-iso-prep-win11-2026/01-iso-prep-win11-2026-008.png)
7. On the command line, navigate to the folder where you put the OPNsense files.\\
`> cd D:\onion-isos\`
8. Now use `certutil` to check the SHA256 has of the file you downloaded from OPNsense.org:\\ `> certutil.exe -hashfile .\OPNsense-26.1.6-dvd-amd64.iso.bz2 SHA256`.

9. The output of the command shows the hash:

   ```bash
   SHA256 hash of .\OPNsense-26.1.6-dvd-amd64.iso.bz2:
   6ba3633d9c0f96d82c792015a45f4b8aac45ea8fa2bdba3c5e534d0c90a4f08c
   CertUtil: -hashfile command completed successfully.
   PS D:\onion-isos>
   ```

10. Make sure the SHA256 value that the `certutil` command generates matches what is on [OPNsense's download page](https://opnsense.org/download/){:target="_blank"}.
   ![](/assets/images/security-onion-images-win11-2026/01-iso-prep-win11-2026/01-iso-prep-win11-2026-009.png)

11. In the Windows File Explorer, right-click the **.iso.bz2** file in your **onion-isos** folder and select **Extract All...** from the context menu.
   ![](/assets/images/security-onion-images-win11-2026/01-iso-prep-win11-2026/01-iso-prep-win11-2026-010.png)
12. The extraction process creates a new folder in the current folder, ending in **.iso**.
   ![](/assets/images/security-onion-images-win11-2026/01-iso-prep-win11-2026/01-iso-prep-win11-2026-011.png)
13. The ISO file is within the extracted folder, `<OPNsense-filename>.iso`.
   ![](/assets/images/security-onion-images-win11-2026/01-iso-prep-win11-2026/01-iso-prep-win11-2026-012.png)

Your OPNsense ISO is ready for installation.

### Download, Validate, and Prepare the Security Onion Installation Media

1. You can download the [current Security Onion ISO from their GitHub repo](https://github.com/Security-Onion-Solutions/securityonion/blob/3/main/DOWNLOAD_AND_VERIFY_ISO.md){:target="_blank"}. The download link for the latest ISO is under **Download and Verify**.
   ![](/assets/images/security-onion-images-win11-2026/01-iso-prep-win11-2026/01-iso-prep-win11-2026-013.png)

2. Right-clik the link and select **Save Link As...** from the context menu.
   ![](/assets/images/security-onion-images-win11-2026/01-iso-prep-win11-2026/01-iso-prep-win11-2026-014.png)

3. Save the file to the same location that you saved your OPNsense download.
   ![](/assets/images/security-onion-images-win11-2026/01-iso-prep-win11-2026/01-iso-prep-win11-2026-015.png)

4. When the file download is complete, use the PowerShell `certutil` command again to generate the SHA256 hash for the ISO file you downloaded.

   ```bash
   > certutil.exe -hashfile .\securityonion-3.1.0-20260528.iso SHA256
   SHA256 hash of .\securityonion-3.1.0-20260528.iso:
   62fab57e247c843d6a04f0796d8162c732b65d82fc3e4a59d087135b9fd32912
   CertUtil: -hashfile command completed successfully.
   ```

5. Verify the hash value against the one on [Security Onion's GitHub](https://github.com/Security-Onion-Solutions/securityonion/blob/3/main/DOWNLOAD_AND_VERIFY_ISO.md){:target="_blank"}:
   ![](/assets/images/security-onion-images-win11-2026/01-iso-prep-win11-2026/01-iso-prep-win11-2026-016.png)

Your Security Onion ISO is ready for installation.