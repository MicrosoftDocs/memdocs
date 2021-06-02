---
title: Install and configure the Microsoft Tunnel VPN solution for Microsoft Intune - Azure | Microsoft Docs
description: Install and configure the Microsoft Tunnel Gateway, a VPN server that runs on Linux. With Microsoft Tunnel, cloud-based devices you manage with Intune can reach your on-premises infrastructure.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 6/14/2021
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

   - **Automatically upgrade servers at this site**: If *Yes*, servers upgrade automatically when an upgrade is available. If *No*, upgrade is manual and an administrator must approve an upgrade before it can start.

     For more information, see [Upgrade Microsoft Tunnel](../protect/microsoft-tunnel-upgrade.md).

   - **Limit server upgrades to maintenance window**: If *Yes*, server upgrades for this site can only start between the start time and end time specified. There must be at least an hour between the start time and end time. When set to *No*, there is no maintenance window and upgrades start as soon as possible depending on how *Automatically upgrade servers at this site* is configured.

     When set to *Yes*, configure the following options:

     - **Time zone** – The time zone you select determines when the maintenance window starts and ends on all servers in the site, regardless of the time zone of individual servers.
     - **Start time** – Specify the earliest time that the upgrade cycle can start, based on the time zone you selected.
     - **End time** - Specify the latest time that upgrade cycle can start, based on the time zone you selected. Upgrade cycles that start before this time will continue to run and can complete after this time.

     For more information, see [Upgrade Microsoft Tunnel](../protect/microsoft-tunnel-upgrade.md).

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

2. To start the server installation, run the script as **root**.  For example, you might use the following command line: `sudo chmod +x ./mstunnel-setup`. The script always installs the [most recent version](../protect/microsoft-tunnel-upgrade.md#microsoft-tunnel-update-history) of Microsoft Tunnel.

   > [!IMPORTANT]
   > **For the U.S. government cloud**, the command line must reference the government cloud environment. To do so, run the following comands to add *intune_env=FXP* to the command line:
   >
   > 1. Run `sudo chmod +x ./mstunnel-setup`
   > 2. Run `sudo intune_env=FXP ./mstunnel-setup`

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

6. After setup installs the certificate and creates the Tunnel Gateway services, you’re prompted to sign in and authenticate with Intune. The user account must have either the Intune Administrator or Global Administrator roles assigned. The account you use to complete the authentication must have an Intune license. The credentials of this account aren't saved and are only used for initial sign-in to Azure Active Directory. After successful authentication, Azure app IDs/secret keys are used for authentication between the Tunnel Gateway and Azure Active Directory.

   This authentication registers Tunnel Gateway with Microsoft Endpoint Manager and your Intune tenant.

   1. Open a web browser to https://Microsoft.com/devicelogin and enter the device code that’s provided by the installation script, and then sign in with your Intune admin credentials.

   2. After Microsoft Tunnel Gateway registers with Intune, the script gets information about your Sites and Server configurations from Intune. The script then prompts you to enter the GUID of the tunnel Site you want this server to join. The script presents you with a list of your available sites.

   3. After you select a Site, setup pulls the Server configuration for that Site from Intune and applies it to your new server to complete the Microsoft Tunnel installation.

7. After the installation script finishes, you can navigate in Microsoft Endpoint Manager admin center to the **Microsoft Tunnel Gateway** tab to view high-level status for the tunnel. You can also open the **Health status** tab to confirm that the server is online.

## Deploy the Microsoft Tunnel client app

To use the Microsoft Tunnel, devices need access to a Microsoft Tunnel client app. You can deploy the tunnel client app to devices by assigning it to users. The following apps are available:

**Android**:

- **Microsoft Defender for Endpoint** - Download Microsoft Defender for Endpoint for use as the Microsoft Tunnel client app from the **Google Play** store. See [Add Android store apps to Microsoft Intune](../apps/apps-add.md).

  When you use Microsoft Defender for Endpoint as your tunnel client application and as a mobile threat defense (MTD) application, see [Use Microsoft Defender for Endpoint for MTD and as the Microsoft Tunnel client app](#use-custom-settings-for-microsoft-defender-for-endpoint) for important configuration guidance.

**iOS/iPadOS**:

- For iOS/iPadOS, download the **Microsoft Tunnel** client app from the Apple **App Store**. See Add iOS store apps to Microsoft Intune.

For more information on deploying apps with Intune, see [Add apps to Microsoft Intune](../apps/apps-add.md).

## Create a VPN profile

After the Microsoft Tunnel installs and devices install the Microsoft Tunnel client app, you can deploy VPN profiles to direct devices to use the tunnel. To do so, you’ll create VPN profiles with one of the following connection types:

- Android: **Microsoft Tunnel**

  The Android platform supports routing of traffic through a per-app VPN and split tunneling rules independently, or at the same time.

  > [!Note]
  > Prior to support for using Microsoft Defender for Endpoint as the tunnel client app, a standalone tunnel client app was available in preview and used a connection type of **Microsoft Tunnel (standalone client)**. As of June 14 2021, both the standalone tunnel app and standalone client connection type are deprecated and drop from support 60 days later on August 14 2021.

- iOS/iPadOS: **Microsoft Tunnel (standalone client)**

  The iOS platform supports routing traffic by either a per-app VPN or by split tunneling rules, but not both simultaneously. If you enable a per-app VPN for iOS, your split tunneling rules are ignored.

### Android

1. Sign in to [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices** > **Configuration profiles** > **Create profile**.

2. For *Platform*, select **Android Enterprise**. For *Profile* select **VPN** for either **Corporate-Owned Work Profile** or **Personally-Owned Work Profile**, and then select **Create**.

   > [!NOTE]
   > *Android Enterprise dedicated* devices aren't supported by the Microsoft Tunnel.

3. On the **Basics** tab, enter a *Name* and *Description* *(optional)* and select **Next**.

4. For *Connection type* select **Microsoft Tunnel**, and then configure the following details:

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

   > [!IMPORTANT]  
   > For *Android Enterprise Personally-Owned Work Profile* devices that use Microsoft Defender for Endpoint as a Microsoft Tunnel client application and as a MTD app, you must use [**custom settings**](#use-custom-settings-for-microsoft-defender-for-endpoint) to configure Microsoft Defender for Endpoint instead of using a separate app configuration profile. Use of custom settings is optional for all other platforms.

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

## Use custom settings for Microsoft Defender for Endpoint

Intune Microsoft Defender for Endpoint as both a MTD app and as the Microsoft Tunnel client application on Android Enterprise devices. If you use Defender for Endpoint for both the Microsoft Tunnel client application and as a MTD app, you can use *custom settings* in your VPN profile for Microsoft Tunnel to simplify your configurations. Use of custom settings in the VPN profile replaces the need to use a separate app configuration profile.

For devices [enrolled](../enrollment/android-enroll.md) as *Android Enterprise personally-owned work profile* that use Defender for Endpoint for both purposes, you must use custom settings instead of an app configuration profile. On these devices, the app configuration profile for Defender for Endpoint conflicts with Microsoft Tunnel and can prevent the device from connecting to Microsoft Tunnel.

If you use Microsoft Defender for Endpoint for MTD but not for Microsoft Tunnel, then you continue to use the app configuration profile to configure Microsoft Defender for Endpoint.

### Add app configuration support for Microsoft Defender for Endpoint to a VPN profile for Microsoft Tunnel

Use the following information to configure the custom settings in a VPN profile to configure Microsoft Defender for Endpoint [in place of a separate app configuration profile](../protect/advanced-threat-protection-manage-android.md):

| Configuration key | Value type | Configuration value            | Information about the setting                |
|-----------------------|------------------|------------|--------------|
| vpn               | Integer | Options: <br> 1 - Enable (default) <br> 0 - Disable | Set a to enable to allow the Microsoft Defender for Endpoint anti-phishing capability to use a local VPN.   |
| antiphishing      | Integer | Options: <br> 1 - Enable (default) <br> 0 - Disable | Set to enable to turn on Microsoft Defender for Endpoint anti-phishing. When disabled, the anti-phishing capability is turned off.   |
| defendertoggle    | Integer | Options: <br> 1 - Enable (default) <br> 0 - Disable | Set to enable to use Microsoft Defender for Endpoint. When disabled, no Microsoft Defender for Endpoint functionality is available.   |

:::image type="content" source="./media/microsoft-tunnel-configure/custom-settings.png" alt-text="Configure custom settings in the VPN profile for Microsoft Defender for Endpoint":::

## Upgrade Microsoft Tunnel

Intune periodically releases updates to the Microsoft Tunnel server. To stay in support, tunnel servers must run the most recent release, or at most be one version behind.

By default, after a new upgrade is available Intune automatically starts the upgrade of tunnel servers as soon as possible, at each of your tunnel sites. To help you manage upgrades, you can configure options that manage the upgrade process:

- You can allow automatic upgrade of servers at a site, or require admin approval before upgrades being.
- You can configure a maintenance window which limits when upgrades at a site can start. 

For more information about upgrades for Microsoft Tunnel, including how to view tunnel status and configure upgrade opotons, see [Upgrade Microsoft Tunnel](../protect/microsoft-tunnel-upgrade.md).

## Update the TLS certificate on the Linux server

You can use the **./mst-cli** command-line tool to update the TLS certificate on the server:  

1. Copy the new certificate to **/etc/mstunnel/certs/site.crt**
2. Copy the private key to **/etc/mstunnel/private/site.key**
3. Run: `mst-cli import_cert`

For more information about *mst-cli*, see [Reference for Microsoft Tunnel](../protect/microsoft-tunnel-reference.md).

## Uninstall the Microsoft Tunnel

To uninstall the product, run **./mst-cli uninstall** from the Linux server as root.

## Next steps

[Use Conditional Access with the Microsoft Tunnel](microsoft-tunnel-conditional-access.md)  
[Monitor Microsoft Tunnel](microsoft-tunnel-monitor.md)
