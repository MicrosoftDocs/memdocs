---
title: Install and configure the Microsoft Tunnel VPN solution for Microsoft Intune - Azure | Microsoft Docs
description: Install and configure the Microsoft Tunnel Gateway, a VPN server that runs on Linux. With Microsoft Tunnel, cloud-based devices you manage with Intune can reach your on-premises infrastructure.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 10/06/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology:

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: lacranda
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Configure Microsoft Tunnel for Intune

This article can help you install the Microsoft Tunnel VPN gateway for Microsoft Intune. You install the tunnel software on a Linux server, and then use Microsoft Endpoint Manager admin center to configure the tunnel for use with your infrastructure. You also configure Intune VPN profiles to deploy the tunnel configuration to supported devices, and must provision devices with the Microsoft Tunnel app.

*Microsoft Tunnel is in public preview*.

To Install Microsoft Tunnel Gateway, you’ll need at least one Linux server with Docker installed, which runs either on-premises or in the cloud. Depending on your environment and infrastructure, additional configurations and software like Azure ExpressRoute might be needed.

Before you start installation be sure to complete the following tasks:

- Review and [Configure prerequisites for Microsoft Tunnel](../protect/microsoft-tunnel-configure.md).
- Run the Microsoft Tunnel [readiness tool](../protect/microsoft-tunnel-overview.md#run-the-readiness-tool) to confirm your environment is ready to support use of the tunnel.

After your prerequisites are ready, return to this article to begin installation and configuration of the tunnel.

When you install Microsoft Tunnel, it pulls down information about the tunnel Sites you’ve defined for your tenant. This information includes the Server configurations for those Sites. Therefore, you must configure at least one Site and one Server configuration before you install Microsoft Tunnel on a Linux server.

## Create a Server configuration

Use of a *Server configuration* lets you set up a configuration one time and have that configuration used by multiple servers. The configuration includes IP address ranges, DNS servers, and split-tunneling rules. Later, you’ll assign a Server configuration to a Site, which automatically applies that configuration to each server that joins that Site.

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

   - Download the tool directly by using a web browser.  Go to https://aka.ms/microsofttunneldownload to download the file **mstunnel-setup**.

   - Sign in to [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Tenant administration** > **Microsoft Tunnel Gateway**, select the **Servers** tab,  select **Create** to open the *Create a server* pane, and then select **Download script**.

     ![Screen capture for download of installation script](./media/microsoft-tunnel-configure/download-installation-script.png)

   - Use a Linux command to get the readiness tool directly. For example, on the server where you’ll install the tunnel, you can use **wget** or **curl** to open the link https://aka.ms/microsofttunneldownload.

      For example, to use **wget** and log details to *mstunnel-setup* during the download, run `wget --output-document=mstunnel-setup https://aka.ms/microsofttunneldownload`

2. To start the server installation, run the script as **root**.  For example, you might use the following command line: `sudo chmod +x ./mstunnel-setup`

   > [!TIP]  
   > If you stop the installation and script, you can restart it by running the command line again. Installation continues from where you left off.

   When you start the script, it downloads container images from Docker, and creates necessary folders and files on the server.

   During setup, the script will prompt you to complete several admin tasks.

3. When prompted by the script, accept the license agreement (EULA).

4. Review and configure variables in the following files to support your environment.

   - Environment file: **/etc/mstunnel/env.sh**. For more information on these variables, see [Environment variables](../protect/microsoft-tunnel-reference.md#environment-variables) in the reference for Microsoft Tunnel article.

5. When prompted, copy the full chain of your TLS certificate file to the Linux server. The script displays the correct location to use on the Linux server.

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

6. After setup installs the certificate and creates the Tunnel Gateway services, you’re prompted to sign in and authenticate with Intune. The user account must have either the Intune Administrator or Global Administrator roles assigned. The account you use to complete the authentication must have an Intune license, or you must turn off the requirement for admin accounts to need licenses. The credentials of this account are not saved and are only used for initial sign-in to Azure Active Directory. After successful authentication, Azure app IDs/secret keys are used for authentication between the Tunnel Gateway and Azure Active Directory.

   > [!TIP]  
   > To turn off the requirement for admin licenses, in the Microsoft Endpoint Manager admin center navigate to **Tenant Administration** > **Roles** > **Administrator Licensing** and disable administrator licensing.

   This authentication registers Tunnel Gateway with Microsoft Endpoint Manager and your Intune tenant.

   1. From a web browser. navigate to https://Microsoft.com/devicelogin and enter the device code that’s provided by the installation script, and then sign in with your Intune admin credentials.

   2. After Microsoft Tunnel Gateway registers with Intune, the script gets information about your Sites and Server configurations from Intune. The script then prompts you to enter the GUID of the tunnel Site you want this server to join. The script presents you with a list of your available sites.

   3. After you select a Site, setup pulls down the Server configuration for that Site and applies it to your new server to complete the Microsoft Tunnel installation.

7. After the installation script finishes, you can navigate in Microsoft Endpoint Manager admin center to the **Microsoft Tunnel Gateway** tab to view high-level status for the tunnel. You can also open the **Health status** tab to confirm that the server is online.

## Deploy the Microsoft Tunnel App

To use the Microsoft Tunnel, devices need access to the Microsoft Tunnel app. You can deploy the app to devices by assigning it to users. The following apps are available:

- For Android, download the **Microsoft Tunnel** app from the **Google Play** store. See Add  Android store apps to Microsoft Intune.
- For iOS/iPadOS, download the **Microsoft Tunnel** app from the Apple **App Store**. See Add iOS store apps to Microsoft Intune.

For more information on deploying apps with Intune, see  Add apps to Microsoft Intune.

## Create a VPN profile

After the Microsoft Tunnel installs on a server, and devices have installed the Microsoft Tunnel app, you can deploy VPN profiles to direct devices to use the tunnel. To do so, you’ll create VPN profiles with a connection type of Microsoft Tunnel.

- The Android platform supports routing of traffic through a per-app VPN and split tunneling rules independently, or at the same time.
- The iOS platform supports routing traffic by either a per-app VPN or by split tunneling rules, but not both simultaneously. If you enable a per-app VPN for iOS, your split tunneling rules are ignored.

### Android

1. Sign in to [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices** > **Configuration profiles** > **Create profile**.

2. For *Platform*, select **Android Enterprise**, and then for *Profile* select **VPN** from for either *Device Owner Only* or *Work Profile Only*, and then select **Create**.

3. On the **Basics** tab, enter a *Name* and *Description* *(optional)* and select **Next**.

4. For *Connection type* select **Microsoft Tunnel**, and then configure the following details:
   - **Base VPN**:  
     - For *Connection name*, specify a name that will display to users.
     - For *Microsoft Tunnel Site*, select the tunnel Site that this VPN profile will use.
   - **Per-app VPN**:  
     - Apps that are assigned in the per-app VPN profile send app traffic to the tunnel.
     - To enable a per-app VPN, select **Add** and then browse to apps you’ve imported to Intune. These can be custom or public apps.

   - **Always-on VPN**:  
     - For *Always-on VPN*, select *Enable* to set the VPN client to automatically connect and reconnect to the VPN. Always-on VPN connections stay connected. If per-app VPN is enabled, only traffic from apps you select will go through the tunnel.
   - **Proxy**:  
     - Configure proxy server details for your environment.  

   For more information about VPN settings, see [Android Enterprise device settings to configure VPN](../configuration/vpn-settings-android-enterprise.md)

5. On the **Assignments** tab, configure groups that will receive this profile.

6. On the **Review + create** tab, review the configuration, and then select **Create** to save it.

### iOS

1. Sign in to [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices** > **Device Configuration** > **Create profile**.

2. For *Platform*, select **iOS/iPadOS**, and then for *Profile* select **VPN**, and then **Create**.

3. On the **Basics** tab, enter a *Name* and *Description* *(optional)* and select **Next**.

4. For *Connection type* select **Microsoft Tunnel**, and then Configure the following items:
   - **Base VPN**:  
     - For *Connection name*, specify a name that will display to users.
     - For *Microsoft Tunnel Site*, select the tunnel Site that this VPN profile will use.  
   - **Per-app VPN**:  
     - To enable a per-app VPN, select **Enable**. Additional configuration steps are required for iOS per-app VPNs. When the per-app VPN is configured, your split tunneling rules are ignored by iOS.

        For more information, see [Per-App VPN for iOS/iPadOS](../configuration/vpn-setting-configure-per-app.md).

    - **Proxy**:  
      - Configure proxy server details for your environment.  

## Upgrade Microsoft Tunnel

When there are updates for Microsoft Tunnel, upgrade of your installed Microsoft Tunnels is managed automatically by Intune in a rolling upgrade:

- Intune upgrades the Microsoft Tunnel servers in a Site one server at a time.

- After a successful upgrade of a server, Intune waits a short period of time before starting the upgrade of the next server.

- This process continues until all servers in a Site have updated to the new version.

## Uninstall the Microsoft Tunnel

To uninstall the product, run **./mst-cli uninstall** from the Linux server as root.

## Next steps

[Monitor Microsoft Tunnel](microsoft-tunnel-monitor.md)
