---
title: Install and configure the Microsoft Tunnel VPN solution for Microsoft Intune - Azure | Microsoft Docs
description: Install and configure the Microsoft Tunnel Gateway, a VPN server that runs on Linux. With Microsoft Tunnel, cloud-based devices you manage with Intune can reach your on-premises infrastructure.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/29/2021
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology:

# optional metadata

#ROBOTS:
#audience:
 
ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Configure Microsoft Tunnel for Intune

Configuration of the Microsoft Tunnel VPN gateway for Microsoft Intune is a multi-step process. The process includes use of the Microsoft Endpoint Manager admin center, and running a script to install the tunnel software on a Linux server, which must run Docker. While this article walks you through the steps to configure the Microsoft Tunnel for use, configuration of Linux and Docker is beyond the scope of this content.

*Microsoft Tunnel is in public preview*.

When installing the Microsoft Tunnel, you’ll start in the Microsoft Endpoint Manager admin center to define both Servers and Sites. Then, you run the tunnel installation script on a Linux server that has Docker installed. The script installs containers to support the tunnel server, pulls information from Intune about the tunnel Sites you’ve defined for your tenant, and then installs the Tunnel server. The Linux server can run on-premises or in the cloud. Depending on your environment and infrastructure, extra configurations and software, like Azure ExpressRoute, might be needed.

Before you continue, be sure to complete the following tasks:

- Review and [Configure prerequisites for Microsoft Tunnel](microsoft-tunnel-prerequisites.md).
- Run the Microsoft Tunnel [readiness tool](../protect/microsoft-tunnel-prerequisites.md#run-the-readiness-tool) to confirm your environment is ready to support use of the tunnel.

After your prerequisites are ready, return to this article to begin installation and configuration of the tunnel.

## Create a Server configuration

Use of a *Server configuration* lets you create a configuration a single time and have that configuration used by multiple servers. The configuration includes IP address ranges, DNS servers, and split-tunneling rules. Later, you’ll assign a Server configuration to a Site, which automatically applies that configuration to each server that joins that Site.

### To create a Server configuration

1. Sign in to [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Tenant administration** > **Microsoft Tunnel Gateway** > *select the* **Server configurations** *tab* > **Create new**.

2. On the **Basics** tab, enter a *Name* and *Description* *(optional)* and select **Next**.

3. On the **Settings** tab, configure the following items:
   - **IP address range**: IP addresses within this range are leased to devices when they connect to Tunnel Gateway. For example, *169.254.0.0/16*.
   - **DNS servers**: These servers are used when a DNS request comes from a device that's connected to Tunnel Gateway.
   - **DNS suffix search** *(optional)*: This domain is provided to clients as the default domain when they connect to Tunnel Gateway.
   - **Split tunneling** *(optional)*: Include or exclude addresses. Included addresses are routed to Tunnel Gateway. Excluded addresses aren’t routed to Tunnel Gateway. For example, you might configure an include rule for *255.255.0.0* or *192.168.0.0/16*.

     Split tunneling supports a total of 500 rules between both include and exclude rules. For example, if you configure 300 include rules, you can only have 200 exclude rules.

   - **Server port**: Enter the port that the server listens to for connections.

4. On the **Review + create** tab, review the configuration, and then select **Create** to save it.

## Create a Site

Sites are logical groups of servers that host Microsoft Tunnel. You’ll assign a Server configuration to each Site you create. That configuration is applied to each server that joins the Site.

### To create a Site configuration

1. Sign in to [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Tenant administration** > **Microsoft Tunnel Gateway** > *select the* **Sites** *tab* > **Create**.

2. On the **Create a site** pane, specify the following properties:

   - **Name**: Enter a name for this Site.
   - **Description** *(optional)*
   - **Public IP address or FQDN**:  Specify a public IP address or FQDN, which is the connection point for devices that use the tunnel. This IP address can be an individual server or the IP or FQDN of a load-balancing server. The IP address must be publicly routable and the FQDN must be resolvable in public DNS.
   - **Server configuration**: Use the drop-down to select a server configuration to associate with this Site.

3. Select **Create** to save the Site.

## Install Microsoft Tunnel Gateway

Before installing Microsoft Tunnel Gateway on a Linux server, configure your tenant with at least one [Server configuration](#create-a-server-configuration), and then create a [Site](#create-a-site). Later, you’ll specify the Site that a server joins when you install the tunnel on that server.

### Use the script to install Microsoft Tunnel

1. Download the Microsoft Tunnel installation script by using one of the following methods:

   - Download the tool directly by using a web browser. Go to https://aka.ms/microsofttunneldownload to download the file **mstunnel-setup**.

   - Sign in to [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Tenant administration** > **Microsoft Tunnel Gateway**, select the **Servers** tab,  select **Create** to open the *Create a server* pane, and then select **Download script**.

     ![Screen capture for download of installation script](./media/microsoft-tunnel-configure/download-installation-script.png)

   - Use a Linux command to get the readiness tool directly. For example, on the server where you’ll install the tunnel, you can use **wget** or **curl** to open the link https://aka.ms/microsofttunneldownload.

      For example, to use **wget** and log details to *mstunnel-setup* during the download, run `wget --output-document=mstunnel-setup https://aka.ms/microsofttunneldownload`

2. To start the server installation, run the script as **root**.  For example, you might use the following command line: `sudo chmod +x ./mstunnel-setup`. The script always installs the [most recent version](#microsoft-tunnel-updates) of Microsoft Tunnel.

   > [!IMPORTANT]
   > **For the U.S. government cloud**, the command line must reference the government cloud environment. To do so add *intune_env=FXP* to the command line. For example: `sudo chmod +x intune_env=FXP ./mstunnel-setup`

   > [!TIP]  
   > If you stop the installation and script, you can restart it by running the command line again. Installation continues from where you left off.

   When you start the script, it downloads container images from Docker, and creates necessary folders and files on the server.

   During setup, the script will prompt you to complete several admin tasks.

3. When prompted by the script, accept the license agreement (EULA).

4. Review and configure variables in the following files to support your environment.

   - Environment file: **/etc/mstunnel/env.sh**. For more information on these variables, see [Environment variables](../protect/microsoft-tunnel-reference.md#environment-variables) in the reference for Microsoft Tunnel article.

5. When prompted, copy the full chain of your Transport Layer Security (TLS) certificate file to the Linux server. The script displays the correct location to use on the Linux server.

   The TLS certificate secures the connection between the devices that use the tunnel and the Tunnel Gateway endpoint. The certificate must have the IP address or FQDN of the Tunnel Gateway server in its SAN.

   The private key will remain available on the machine where you create the certificate signing request for the TLS certificate. This file must be exported with a name of **site.key**.

   Install the TLS certificate and private key. Use the following guidance that matches your file format:

   - **PFX**:
     - The certificate file name must be **site.pfx**. Copy the certificate file to **/etc/mstunnel/private/site.pfx**.

   - **PEM**:
     - The full chain (root, intermediate, end-entity) must be in a single file named **site.crt**. If your using a certificate issued by a public provider like Digicert, you have the option of downloading the complete chain as a single .pem file.

     - The certificate file name must be **site.crt*. Copy the full chain certificate into **/etc/mstunnel/certs/site.crt**. For example: `cp [full path to cert] /etc/mstunnel/certs/site.crt`

       Alternatively, create a link to the full chain cert in **/etc/mstunnel/certs/site.crt**. For example: `ln -s [full path to cert] /etc/mstunnel/certs/site.crt`

     - Copy the private key file into **/etc/mstunnel/private/site.key**. For example: `cp [full path to key] /etc/mstunnel/private/site.key`

       Alternatively, create a link to the private key file in **/etc/mstunnel/private/site.key**. For example: `ln -s [full path to key file] /etc/mstunnel/private/site.key` This key shouldn't be encrypted with a password. The private key file name must be **site.key**.

6. After setup installs the certificate and creates the Tunnel Gateway services, you’re prompted to sign in and authenticate with Intune. The user account must have either the Intune Administrator or Global Administrator roles assigned. The account you use to complete the authentication must have an Intune license, or you must turn off the requirement for admin accounts to need licenses. The credentials of this account aren't saved and are only used for initial sign-in to Azure Active Directory. After successful authentication, Azure app IDs/secret keys are used for authentication between the Tunnel Gateway and Azure Active Directory.

   > [!TIP]  
   > To turn off the requirement for admin licenses, in the Microsoft Endpoint Manager admin center navigate to **Tenant Administration** > **Roles** > **Administrator Licensing** and disable administrator licensing.

   This authentication registers Tunnel Gateway with Microsoft Endpoint Manager and your Intune tenant.

   1. Open a web browser to https://Microsoft.com/devicelogin and enter the device code that’s provided by the installation script, and then sign in with your Intune admin credentials.

   2. After Microsoft Tunnel Gateway registers with Intune, the script gets information about your Sites and Server configurations from Intune. The script then prompts you to enter the GUID of the tunnel Site you want this server to join. The script presents you with a list of your available sites.

   3. After you select a Site, setup pulls the Server configuration for that Site from Intune and applies it to your new server to complete the Microsoft Tunnel installation.

7. After the installation script finishes, you can navigate in Microsoft Endpoint Manager admin center to the **Microsoft Tunnel Gateway** tab to view high-level status for the tunnel. You can also open the **Health status** tab to confirm that the server is online.

## Deploy the Microsoft Tunnel App

To use the Microsoft Tunnel, devices need access to the Microsoft Tunnel app. You can deploy the app to devices by assigning it to users. The following apps are available:

- For Android, download the **Microsoft Tunnel** app from the **Google Play** store. See Add  Android store apps to Microsoft Intune.
- For iOS/iPadOS, download the **Microsoft Tunnel** app from the Apple **App Store**. See Add iOS store apps to Microsoft Intune.

For more information on deploying apps with Intune, see  Add apps to Microsoft Intune.

## Create a VPN profile  

> [!Important]
> In preparation for the [public preview of Tunnel client functionality in the Microsoft Defender for Endpoint app](https://aka.ms/defendertunnel), the VPN profile connection type for the Microsoft Tunnel client app has been renamed to **Microsoft Tunnel (standalone client)**. At this time, you should use the **Microsoft Tunnel (standalone client)** connection type, not the **Microsoft Tunnel** connection type.   

After the Microsoft Tunnel installs and devices install the Microsoft Tunnel app, you can deploy VPN profiles to direct devices to use the tunnel. To do so, you’ll create VPN profiles with the **Microsoft Tunnel (standalone client)** connection type.  


- The Android platform supports routing of traffic through a per-app VPN and split tunneling rules independently, or at the same time.
- The iOS platform supports routing traffic by either a per-app VPN or by split tunneling rules, but not both simultaneously. If you enable a per-app VPN for iOS, your split tunneling rules are ignored.

### Android

1. Sign in to [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices** > **Configuration profiles** > **Create profile**.

2. For *Platform*, select **Android Enterprise**. For *Profile* select **VPN** for either **Corporate-Owned Work Profile** or **Personally-Owned Work Profile**, and then select **Create**.

   > [!NOTE]
   > *Android Enterprise dedicated* devices aren't supported by the Microsoft Tunnel.

3. On the **Basics** tab, enter a *Name* and *Description* *(optional)* and select **Next**.

4. For *Connection type* select **Microsoft Tunnel (standalone client)**, and then configure the following details:

   - **Base VPN**:  
     - For *Connection name*, specify a name that will display to users.
     - For *Microsoft Tunnel Site*, select the tunnel Site that this VPN profile will use.

   - **Per-app VPN**:  
     - Apps that are assigned in the per-app VPN profile send app traffic to the tunnel.
     - On Android, launching an app won't launch the per-app VPN. However, when the VPN has *Always-on VPN* set to *Enable*, the VPN will already be connected and app traffic will use the active VPN. If the VPN isn't set to be *Always-on*, the user must manually start the VPN before it can be used.
     - To enable a per-app VPN, select **Add** and then browse to custom or public apps you’ve imported to Intune.

   - **Always-on VPN**:  
     - For *Always-on VPN*, select *Enable* to set the VPN client to automatically connect and reconnect to the VPN. Always-on VPN connections stay connected. If *Per-app VPN* is set to *Enable*, only the traffic from apps you select go through the tunnel.

   - **Proxy**:  
     - Configure proxy server details for your environment.  

   For more information about VPN settings, see [Android Enterprise device settings to configure VPN](../configuration/vpn-settings-android-enterprise.md)

5. On the **Assignments** tab, configure groups that will receive this profile.

6. On the **Review + create** tab, review the configuration, and then select **Create** to save it.

### iOS

1. Sign in to [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices** > **Device Configuration** > **Create profile**.

2. For *Platform*, select **iOS/iPadOS**, and then for *Profile* select **VPN**, and then **Create**.

3. On the **Basics** tab, enter a *Name* and *Description* *(optional)* and select **Next**.

4. For *Connection type* select **Microsoft Tunnel (standalone client)**, and then configure the following items:
   - **Base VPN**:  
     - For *Connection name*, specify a name that will display to users.
     - For *Microsoft Tunnel Site*, select the tunnel Site that this VPN profile will use.  
   - **Per-app VPN**:  
     - To enable a per-app VPN, select **Enable**. Additional configuration steps are required for iOS per-app VPNs. When the per-app VPN is configured, your split tunneling rules are ignored by iOS.

        For more information, see [Per-App VPN for iOS/iPadOS](../configuration/vpn-setting-configure-per-app.md).

   - **On-Demand VPN Rules**:  
     Define on-demand rules that allow use of the VPN when conditions are met for specific FQDNs or IP addresses.

     For more information, see [Automatic VPN settings](../configuration/vpn-settings-ios.md#automatic-vpn)

   - **Proxy**:  
     - Configure proxy server details for your environment.  

## Upgrade Microsoft Tunnel

When there are [updates for Microsoft Tunnel](#microsoft-tunnel-updates), upgrade of your installed Microsoft Tunnel is managed automatically by Intune in a rolling upgrade:

- Intune upgrades the Microsoft Tunnel servers in a Site one server at a time. During upgrade, the Microsoft Tunnel on the server isn't available for use.

- Intune begins to update the first server in a Site as soon as 10 minutes after the release becomes available. If the server was off, it begins after the server turns on.

- After a successful upgrade of a server, Intune waits a short period of time before starting the upgrade of the next server.

- This process continues until all servers in a Site have updated to the new version.

The tunnel update is automatic, but updates only a single server per Site at a time. To avoid down-time while a server updates, consider assigning two or more servers to each Microsoft Tunnel Site.

## Update the TLS certificate on the Linux server

You can use the **./mst-cli** command-line tool to update the TLS certificate on the server:  

1. Copy the new certificate to **/etc/mstunnel/certs/site.crt**
2. Copy the private key to **/etc/mstunnel/private/site.key**
3. Run: `mst-cli import_cert`

For more information about *mst-cli*, see [Reference for Microsoft Tunnel](../protect/microsoft-tunnel-reference.md).
## Uninstall the Microsoft Tunnel

To uninstall the product, run **./mst-cli uninstall** from the Linux server as root.

## Microsoft Tunnel updates

Updates for the Microsoft Tunnel release periodically. When a new version is available, read about the changes here. Because Microsoft Tunnel [automatically updates](#upgrade-microsoft-tunnel) when a new version releases, you'll automatically benefit from each new version.

After an update releases, it rolls out to tenants over the following days. This means your tunnel servers might not start the process to update for a few days.

The Microsoft Tunnel version for a server isn’t available in the Intune UI at this time. Instead, run the following command on the Linux server that hosts the tunnel to identify the hash values of  *agentImageDigest* and *serverImageDiegest*: `cat /etc/mstunnel/images_configured`

### March 29, 2021

Image hash values:

- **agentImageDigest**: sha256:7ff81ebec9d129558cf07ba1d044d4051dbfaf9eb75cc91500a11f4ef0cb447e

- **serverImageDigest**: sha256:56dc303c67735bad243b2dc8644cc3d1e5318aa963be05a9a685ec6bcbb41c4e

Changes in this release:

- Minor bug fixes and enhancements

- ### January 19, 2021

Image hash values:

- **agentImageDigest**: sha256:227557e71b197c5c26baeed7633e5f89b476bbb8eb23fc82dec260890d5145f1

- **serverImageDigest**: sha256:70026dc3585db871f419d25066e655902af732286b0537512d53e1f0897cc423

Changes in this release:

- Support for Red Hat Enterprise Linux 8.
- Extraneous logging suppressed.

### October 29, 2020

Image hash values:

- **agentImageDigest**: sha256:ba48de2c746a68286d15985f807702c60004131368a4a6a50ceab0f04653031a

- **serverImageDigest**: sha256:a60d778664f7f3ba28d363ec783014d9fc2eda6cc5f6057a1eab8635928e7b07

Changes in this release:

- Fixes for logging. [View the Microsoft Tunnel system logs](../protect/microsoft-tunnel-monitor.md#view-microsoft-tunnel-logs).
- Additional bug fixes.

### October 12, 2020

Image hash values:

- **agentImageDigest**: sha256:d168e416591d94d6a02b64e5dde8709e2d5a44261d67036caafcb55b12912ca5

- **serverImageDigest**: sha256:8b50257a94b9825915cb6a77ed49cfb3e5c6f68da9ae0272cdf8e49cff3d342e

Changes in this release:

- Microsoft Tunnel now [logs](../protect/microsoft-tunnel-monitor.md#view-microsoft-tunnel-logs) operational and monitoring details to Linux server logs in the *syslog* format.
- Various bug fixes.

### September 23, 2020

The initial public preview release of Microsoft Tunnel.

<!-- Archive of past releases
-->
## Next steps

[Use Conditional Access with the Microsoft Tunnel](microsoft-tunnel-conditional-access.md)  
[Monitor Microsoft Tunnel](microsoft-tunnel-monitor.md)
