---
title: Set up a telecom expense management service in Microsoft Intune - Azure | Microsoft Docs
titleSuffix: 
description: Integrate Microsoft Intune with the Saaswedo telecom expense management service to monitor data usage and set thresholds or limits on Android device administrator, iOS, and iPadOS devices.
keywords: Saaswedo
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 06/08/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology:
ms.assetid: b7bf5802-4b65-4aeb-ac99-8e639dd89c2a


# optional metadata

#ROBOTS:
#audience:

ms.reviewer: davidra
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Microsoft Tunnel for Microsoft Intune
ms-tunnel-overview.md

Microsoft Tunnel is a VPN gateway solution for Microsoft Intune. The tunnel allows access to on-premises resources from iOS/iPadOS and Android Enterprise devices using modern authentication and Conditional Access. This article explains how the tunnel works, including prerequisites to use it, and its architecture. 

*Microsoft Tunnel is in public preview*.

When you have your prerequisite configurations in place and are ready to install the tunnel, see [Configure the Microsoft Tunnel](../protect/tunnel-configure.md). 


## Overview of Microsoft Tunnel
The Microsoft Tunnel VPN gateway solution installs to a Docker container that runs on a Linux server. The Linux server can be a physical box in your on-premises environment, or a virtual machine that runs on-premises or in the cloud. After the tunnel installs, you use Intune VPN profiles for iOS or Android to direct your devices to use the tunnel for connections to your corporate network and resources. When the tunnel is hosted in the cloud, you’ll need to use a solution like Azure ExpressRoute to extend your on-premises network to the cloud. The tunnel doesn’t support co-managed or tenant attached devices.

Through the Microsoft Endpoint Manager admin center, you’ll:
•	Download the Tunnel installation script that you’ll run on the Linux servers.
•	Configure aspects of the Microsoft Tunnel like IP addresses, DNS servers, and ports.
•	Deploy VPN profiles to devices to direct them to use the tunnel.
 
Through the VPN client, devices: 
•	Use Azure Active Directory (Azure AD) to authenticate to the tunnel.
•	Are evaluated against your Conditional Access policies. If the device isn’t compliant, then it won’t have access to your VPN server.   

To connect to the tunnel, devices use the Microsoft Tunnel app, which is available from the iOS/iPadOS or Android app stores.

You can install multiple Linux servers to support Microsoft Tunnel, and combine servers into logical groups called *Sites*. Each server can join a single Site. When you configure a Site, you’re defining a connection point for devices to use when they access the tunnel. Sites require a *Server configuration* that you’ll define and assign to the Site. The Server configuration is applied to each server you add to that Site, simplifying the configuration of additional servers.  

To direct devices to use the tunnel, you create and deploy a VPN policy for Microsoft Tunnel. This policy is a device configuration VPN profile that uses the Microsoft Tunnel for its connection type. 
Features of the VPN profiles for the tunnel include: 
•	A friendly name for the VPN connection that your end users will see.
•	The Site that the VPN client connects to. 
•	Per-app VPN configurations that define which apps the VPN profile is used for, and if its always-on or not. When always-on, the VPN will automatically connect and is used only for the apps you define. 
•	Manual connections to the tunnel when a user launches the VPN and selects *Connect*. 
•	Proxy support (iOS/iPadOS, Android 10+) 


Server configurations include: 
•	IP address range – These are the IP addresses that are assigned to devices that connect to your tunnel gateway server.
•	DNS servers – The DNS server devices should use when they connect to the server.
•	DNS suffix search. 
•	Split tunneling rules – Up to 500 rules shared across include and exclude routes. For example, if you create 300 include rules, you can then have up to 200 exclude rules. 
•	Port – The port that the tunnel gateway server listens on. 

Site configuration includes:
•	A public IP address or FQDN, which is the connection point for devices that use the tunnel. This can be an individual server or the IP or FQDN of a load-balancing server.
•	The Server configuration that is applied to each server in the Site. 


You assign a server to a Site at the time you install the tunnel software on the Linux server. The installation uses a script that you can download from within the admin center. After starting the script, you’ll be prompted to configure its operation for your environment, which includes specifying the Site the server will join. 

To use the Microsoft Tunnel, devices will need to install the Microsoft Tunnel app. You get the app from the iOS/iPadOS or Android app stores and deploy it to users. 

## Configure prerequisites for Microsoft Tunnel
The following sections detail prerequisites for the Linux server that hosts the tunnel software, and for your network.  

Note:
Microsoft Tunnel isn’t supported with Azure Government cloud environments.

### Linux server
Set up a Linux based virtual machine or a physical box on which the Microsoft Tunnel Gateway will install. 

•	**Linux distribution**: The following are supported:
•	CentOS 7.4+(CentOS 8+ isn’t supported)
•	Red Hat (RHEL) 7.4+ (RHEL 8+ is not supported)
•	Ubuntu 18.04 
•	Ubuntu 20.04  

•	**Size the Linux server**: Use the following guidance to meet your expected use:
# Devices 	# CPUs  	Memory GB  	# Servers  	# Sites  	Disk Space GB  
1000  	4 	4 	1  	1  	30  
2000  	4 	4 	1  	1  	30  
5000  	8  	8  	2  	1  	30  
10000  	8  	8  	3  	1  	30  
20000  	8  	8  	4  	1  	30  
40000  	8  	8  	8  	1  	30  

Support scales linearly. While each tunnel server supports up to 64,000 concurrent connections, individual devices can open multiple connections. 

•	**CPU**: 64-bit AMD/Intel processor.  

•	**Install Docker**:  Install Docker version 19.03 CE or later.

Microsoft Tunnel requires Docker on the Linux server to provide support for containers. Containers provide a consistent execution environment, health monitoring and proactive remediation, as well as a clean upgrade experience.  

For information about installing and configuring Docker, see: 
•	Install Docker Engine on CentOS 
•	Using Docker on Red Hat Enterprise Linux 7
•	Install Docker Engine on Ubuntu 

•	**Transport Layer Security (TLS) certificate**: The Linux server requires a trusted TLS certificate to secure the connection between devices and the Tunnel Gateway server. You’ll add the TLS certificate, including the full trusted certificate chain, to the server during installation of the Tunnel Gateway. 

o	The TLS certificate used to secure the Tunnel Gateway endpoint must have the IP address or FQDN of the Tunnel Gateway server in the SAN.  
o	TLS certificate cannot have an expiration date longer than 2 years or it will not be accepted on iOS devices.
o	Use of wildcards has limited support. For example, **\*.contoso.com** is supported. **cont*.com** isn’t supported. 
o	During installation of the Tunnel Gateway server, you must copy the entire trusted certificate chain to your Linux server. The installation script provides the location where you copy the certificate files and prompts you to do so.
o	If you use a TLS certificate that isn't publicly trusted, you must push the entire trust chain to devices using an Intune *trusted certificate* profile.  
o	The TLS certificate can be in **PEM** or **pfx** format.  
 

### Network 
We recommend using two Network Interface controllers (NICs) per Linux server to improve performance, though use of two is optional. 
 
o	**NIC 1** - This NIC handles traffic from your managed devices and should be on a public network with public IP address.  This is the address that you configure in the *Site configuration*. This address can represent a single server or a load balancer. 
o	**NIC 2** - This NIC handles traffic to your on-premises resources and should be on your private internal network without network segmentation.

If you run Linux as a VM in a cloud, you’ll need to ensure the server can access to your on-premises network. For example, if your VM runs in Azure, you can use Azure ExpressRoute or something similar to provide access. If you run the server in a VM on-premises, ExpressRoute is not necessary. 

If you choose to add a load balancer, consult your vendors documentation for configuration details, and take into consideration network traffic and firewall ports specific to Intune and the Microsoft Tunnel.

### Firewall
By default, the Microsoft Tunnel and server use the following ports: 

**Inbound ports**:
•	TCP 443 – Required by Microsoft Tunnel.
•	UDP 443 – Required by Microsoft Tunnel.
•	TCP 22 – Optional. Used for SSH/SCP. 

**Outbound ports**:
•	TCP 443 – Required to access Intune services. Required by Docker to pull images. 
•	TCP – 80 – Required to access Intune services.

When you create a Server configuration for the tunnel, you can specify a different port than the default of 443. If you specify a different port, be sure to configure firewalls to support your configuration. 

**Additional configurations**:
•	The Tunnel shares the same requirements as Network endpoints for Microsoft Intune, with the addition of port TCP 22, as noted above.  
•	Configure firewall rules to support the configurations detailed in  Microsoft Container Registry (MCR) Client Firewall Rules Configuration. 

### Proxy
You can use a proxy server with Microsoft Tunnel. The following can help you configure the Linux server and your environment for success: 

•	If you use an internal proxy, you might need to configure the Linux host to use your proxy server by using environment variables. This can be done by editing the **/etc/environment** file on the Linux server, and adding the following lines:
•	http_proxy=[address]  
https_proxy=[address] 

•	Authenticated proxies are not supported. 

•	The proxy can’t perform break and inspect. This is because the Linux server uses TLS mutual authentication when connecting to Intune.

•	Configure Docker to use the proxy to pull images. To do so, edit the **/etc/systemd/system/docker.service.d/http-proxy.conf** file on the Linux server and add the following lines:
•	[Service]
Environment="HTTP_PROXY=http://your.proxy:8080/"
Environment="HTTPS_PROXY=http://your.proxy:8080/"
Environment="NO_PROXY=127.0.0.1,localhost

Note:
Microsoft Tunnel doesn’t support Azure AD App Proxy, or similar proxy solutions.

### Platforms
The following device platforms are supported with Microsoft Tunnel, for devices enrolled with Intune:
•	Android Enterprise (Fully managed, Corporate-Owned Work Profile, Work profile) 
•	iOS/iPadOS 
 
The following functionality is supported by all platforms:
•	Azure Active Directory (Azure AD) authentication to the Tunnel using either username and password, or certificates. 
•	Per-App support. 
•	Manual full-device tunnel through a Tunnel app, where the user launches VPN and clicks *Connect*. 
•	Split tunneling. However, on iOS split tunneling rules are ignored when your VPN profile uses *per app VPN*. 

Support for a Proxy is limited to the following platforms:
•	Android 10 and later
•	iOS/iPadOS


## Run the readiness tool
Before you start a server install, we recommend you download and run the **mst-readiness** tool. The tool is a script that runs on your Linux server and does the following:
•	Confirms that your network configuration allows Microsoft Tunnel to access the required Microsoft endpoints.  
•	Validates that the Azure Active Directory (Azure AD) account you’ll use to install the tunnel server has the required roles to complete enrollment. 

The mst-readiness tool has a dependency on **jq**, a command-lie JSON processor. 
•	Before you run the readiness tool, ensure **jq** is installed. 
•	For information about how to get and install **jq**, see the documentation for the version of Linux that you use.

To use the readiness tool:
1.	Get the readiness tool through one of the following methods:
•	Download the tool directly by using a web browser.  Go to https://aka.ms/microsofttunnelready.  This downloads a file named **mst-readiness**.
•	Sign in to [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Tenant administration** > **Microsoft Tunnel Gateway**, select the **Servers** tab, select **Create** to open the *Create a server* pane, and then select **Download readiness tool**.  
•	Use a Linux command to get the readiness tool directly. For example, you can use **wget** or **curl** to open the link https://aka.ms/microsofttunnelready.

The script can be run from any Linux server that is on the same network as the server you plan to install, allowing network admins to run it and troubleshoot network issues independently.

2.	To validate your network configuration, run the script as **root** and use the following command line: `./mst-readiness network`

The script runs the following actions and reports on success or error for both:
•	Tries to connect to each Microsoft endpoint the tunnel will use. 
•	Checks that the required ports are open in your firewall.

3.	To validate that the account you’ll use to install Microsoft Tunnel has the required roles and permissions to complete enrollment, run the script with the following command line: `./mst-readiness account` 

You’ll be prompted to use a different machine with a web browser, which will then be used to authenticate to Azure AD and to Intune. The tool will report success or an error. 

For more information about this tool, see [Reference for mst-cli](../protect/microsoft-tunnel-reference.md#mst-cli-command-line-tool-for-microsoft-tunnel) in the Reference for Microsoft Tunnel article. 

## Use Conditional Access with the Microsoft Tunnel

When you use Conditional Access with Intune, you can create policies to gate device access to the Microsoft Tunnel. 

### Provision your tenant
Before you can configure Conditional Access policies for the tunnel, you must enable your tenant to support Microsoft Tunnel for Conditional Access. To enable your tenant, you run a PowerShell script that modifies your tenant to add **Microsoft Tunnel Gateway** as a cloud app that you can then select as part of a Conditional Access policy.  This process requires the use of the Azure Active Directory PowerShell module.
1.	[Download and install](https://docs.microsoft.com/powershell/azure/active-directory/install-adv2?view=azureadps-2.0) the **AzureAD PowerShell module**.  
2.	Download the PowerShell script named **mst-CA-provisioning.ps1** from **aka.ms/mst-ca-provisioning**.
3.	Using credentials that have the Azure Role permissions equivalent to Application Administrator, run the script from any location in your environment, to provision your tenant.  
The script modifies your tenant by creating a service principle with the following details:
•	App ID: 3678c9e9-9681-447a-974d-d19f668fcd88
•	Name: Microsoft Tunnel Gateway

The addition of this service principle is required so you can select the tunnel cloud app while configuring Conditional Access policies. It is also possible to use Graph to add the service principle information to your tenant.  
4.	After the script completes, you can use your normal process to create Conditional Access policies. 

For more information, see Create a device-based Conditional Access policy. 

### Create Conditional Access policy to limit access to Microsoft Tunnel

If you choose to configure Conditional Access policy to limit user access, we recommend configuring this policy after you provision your tenant to support the tunnel, but before you install the Tunnel Gateway. 

1.	Sign in to [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Endpoint Security** > **Conditional access** > **New policy**.
2.	Specify a name for this policy.
3.	To configure user and group access, below *Assignments*, select **Users and groups**.
a.	Select **Include** > **All users**.  
b.	Next, select **Exclude** and configure the groups you want to *grant access to*, and then save the user and Group configuration.
4.	Below *Access controls*, select **Grant**.
a.	Select **Block access**, and then save the Grant configuration.  
5.	Set **Enable policy** to **On**.
6.	Select **Create**.


## Architecture
The Microsoft Tunnel Gateway runs in Docker containers that run on Linux servers.  


  
Components:
A – Microsoft Intune.
B- Azure Active Directory (AD).
C – Linux server with Docker.  
  	Ci - Microsoft Tunnel Gateway.
	Cii – Management Agent.
Ciii – Authentication plugin – Authorization plugin, which authenticates with Azure AD.
D – Public facing IP or FQDN of the Microsoft Tunnel. This can represent a load balancer.
E – Mobile Device Management (MDM) enrolled device.
F – Firewall
G – Internal Proxy Server (optional).
H – Corporate Network.
I – Public internet.

Actions:	
1.	Intune administrator configures *Sites* and defines *Server configurations*. 
2.	Authentication plugin authenticates Microsoft Tunnel Gateway with Azure AD.
3.	Management Agent communicates to Intune to retrieve your server configuration policies, and to send telemetry logs to Intune. 
4.	Intune administrator creates and deploys VPN profiles and the Tunnel app to devices.    
5.	Device authenticates to Azure AD. Conditional Access policies are evaluated. 
6.	With split tunnel:
a.	Some traffic goes directly to the public internet.
b.	Some traffic goes to your public facing IP address for the Tunnel.
7.	The Tunnel routes traffic to your internal proxy and your corporate network.

Additional details:
•	Conditional Access is done in the VPN client and based on the cloud app *Microsoft Tunnel Gateway*. Non-compliant devices won’t receive an access token from Azure AD and won’t be able to access the VPN server. For more information about using Conditional Access with Microsoft Tunnel, see [Use Conditional Access with the Microsoft Tunnel.
•	The Management Agent is authorized against Azure AD using Azure app ID/secret keys.   
•	The VPN server uses NAT to provide addresses to VPN clients that are connecting to the corporate network. 
  
## Next steps
[Install and configure Microsoft Tunnel](ms-tunnel-overview.md)

 

# Configure Microsoft Tunnel for Intune
ms-tunnel-configure.md
This article can help you install the Microsoft Tunnel VPN gateway for Microsoft Intune. You install the tunnel software on a Linux server, and then use Microsoft Endpoint Manager admin center to configure the tunnel for use with your infrastructure. You also configure Intune VPN profiles to deploy the tunnel configuration to supported devices, and must provision devices with the Microsoft Tunnel app.   

*Microsoft Tunnel is in public preview*.

To use Microsoft Tunnel, you’ll need at least one Linux server with Docker installed, which runs either on-premises or in the cloud. Depending on your environment and infrastructure, additional configurations and software like Azure ExpressRoute might be needed.

Before you start installation be sure to complete the following tasks: 
•	Review and [Configure prerequisites for Microsoft Tunnel](../protect/ms-tunnel-configure.md). 
•	Run the Microsoft Tunnel [readiness tool](../protect/ms-tunnel-configure.md#run-the-readiness-tool) to confirm your environment is ready to support use of the tunnel. 

When your prerequisites are ready, return to this article to begin installation and configuration of the tunnel. 

When you install a tunnel server, it pulls down information about the tunnel Sites you’ve defined for you tenant, and the Server configurations for those Sites. Therefore, you must configure at least one Site and one Server configuration before you install the tunnel gateway server on a Linux server. 
 
## Create a Server configuration
Use of a *Server configuration* lets you set up a configuration one time and have that configuration used by multiple servers. The configuration includes IP address ranges, DNS servers, and split-tunneling rules. Later, you’ll assign a Server configuration to a Site, which automatically applies that configuration to each server that joins that Site.  

### To create a Server configuration:

1.	Sign in to [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Tenant administration** > **Microsoft Tunnel Gateway** > *select the* **Server configurations** *tab* > **Create new**.

2.	On the **Basics** tab, enter a *Name* and *Description* *(optional)* and select **Next**. 

3.	On the **Settings** tab, configure the following:
•	**IP address range**: IP addresses within this range are leased to devices when they connect to Tunnel Gateway.
•	**DNS servers**: These servers are used when a DNS request comes from a device that's connected to Tunnel Gateway.
•	**DNS suffix search** *(optional)*: This domain is provided to clients as the default domain when they connect to Tunnel Gateway.
•	**Split tunneling** *(optional)*: Include or exclude addresses. Included addresses are routed to Tunnel Gateway. Excluded addresses aren’t routed to Tunnel Gateway. 

Split tunneling supports a total of 500 rules between both include and exclude rules. For example, if you configure 300 include rules, you can only have 200 exclude rules. 

•	**Server port**: Enter the port that the server listens to for connections.

4.	On the **Review + create** tab, review the details for the configuration and select **Create** to save it. 

## Create a Site
Sites are logical groups of servers that host Microsoft Tunnel. You’ll assign a Server configuration to each Site you create. That configuration is applied to each server that joins the Site. 

### To create a Site configuration

1.	Sign in to [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Tenant administration** > **Microsoft Tunnel Gateway** > *select the* **Sites** *tab* > **Create**.

2.	On the **Create a site** pane, specify the following properties:
- **Name**: Enter a name for this Site. 
- **Description** *(optional)*
- **Public IP address or FQDN**:  Specify a public IP address or FQDN which is the connection point for devices that use the tunnel. This can be an individual server or the IP or FQDN of a load-balancing server.  The IP address must be publicly routable and the FQDN must be resolvable in public DNS.
- **Server configuration**: Use the drop-down to select a server configuration to associate with this Site.   
4. Select **Create** to save the Site. 

 
## Install Microsoft Tunnel
Before installing the Microsoft Tunnel on a Linux server, configure your tenant with at least one [Server configuration](#create-a-server-configuration), and then create a [Site](create-a-tunnel-site). Later, you’ll specify the Site that a server joins when you install the tunnel on that server. 
### Install Microsoft Tunnel: 

1.	Download the Microsoft Tunnel installation script through one of the following methods:
•	Open a web browser to https://aka.ms/microsofttunneldownload.

![Screen capture for download of installation script](/media/download-installation-script.png) 

•	Sign in to  [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Tenant administration** > **Microsoft Tunnel Gateway**, select the **Servers** tab,  select **Create** to open the *Create a server* pane, and then select **Download script**.  

The script downloads to your machine and has the name **mstunnel-setup**.

•	Use a Linux command to get the readiness tool directly. For example, on the server where you’ll install the tunnel, you can use **wget** or **curl** to open the link https://aka.ms/microsofttunnelready.  
 
2.	To start the server installation, run the script as **root** with the following command line: `./mstunnel-setup` 
TIP
If you stop the installation and script, you can restart it by running the command line again. Installation continues from where you left off. 
When you start the script, it downloads container images from Docker, and creates necessary folders and files on the server. 

	During setup, the script will prompt you to complete several admin tasks. 

3.	When prompted, accept the license agreement (EULA).

4.	Review and configure variables in the following files to support your environment.

•	Environment file: **/etc/mstunnel/env.sh**. For more information on these variables, see [Environment variables](../protect/ms-tunnel-refernce.md#environment variables) in the reference for Microsoft Tunnel article. 

5.	When prompted, copy the full chain of your TLS certificate file to the Linux server. The script displays the correct location to use on the Linux server. 

The TLS certificate secures the connection between the devices that use the tunnel and the Tunnel Gateway endpoint. The certificate must have the IP address or FQDN of the Tunnel Gateway server in its SAN.    
a.	Install the TLS certificate and private key. Use the following guidance that matches your file format: 

o	**PFX**:  
o	Copy the certificate file to **/etc/mstunnel/private/site.pfx**. 
o	**PEM**:
o	 Copy the full chain certificate into **/etc/mstunnel/certs/site.crt**.  For example:  `cp [full path to cert] /etc/mstunnel/certs/site.crt`
 
Alternatively, create a link to the full chain cert in **/etc/mstunnel/certs/site.crt**.  For example: `ln -s [full path to cert] /etc/mstunnel/certs/site.crt` 

o	Copy the private key file into **/etc/mstunnel/private/site.key**. For example: `cp [full path to key] /etc/mstunnel/private/site.key`
Alternatively, create a link to the private key file in **/etc/mstunnel/private/site.key**. For example: `ln -s [full path to key file] /etc/mstunnel/private/site.key`  This key should not be encrypted with a password.  


6.	After setup installs the certificate and creates the Tunnel Gateway services, you’re prompted to sign-in and authenticate with Intune. Use your Intune admin or Global Admin credentials. The account you use to complete the authentication must have an Intune license, or you must turn off the requirement for admin accounts to need licenses.  

Tip:
To turn off the requirement for admin licenses, in the Microsoft Endpoint Manager admin center navigate to **Tenant Administration** > **Roles** > **Administrator Licensing** and disable administrator licensing.

This authentication registers a connector to join the Tunnel Gateway with Microsoft Endpoint Manager and your Intune tenant.

a.	Use a separate device with a web browser. Navigate to **https://Microsoft.com/devicelogin** and enter the device code that’s provided by the installation script with the prompt to register, and then sign-in to with your Intune admin credentials. 

b.	After the connector registers, the script gets information about your Sites and Server configurations from Intune, and then prompts you to enter the GUID of the tunnel Site you want this server to join. The script presents you with a list of your available sites.

c.	After you select a Site, setup pulls down the Server configuration for that Site and applies it to your new tunnel server to complete the server installation. 

7.	After the installation script finishes, you can navigate in Microsoft Endpoint Manager admin center to the **Microsoft Tunnel Gateway** tab to view high level status for the tunnel. You can also open the **Health status** tab to confirm that the server is online. 

## Deploy the Microsoft Tunnel App
To use the Microsoft Tunnel, devices need access to the Microsoft Tunnel app. You can deploy the app to devices by assigning it to users. The following apps are available:

•	For Android, download the **Microsoft Tunnel** app from the **Google Play** store. See Add  Android store apps to Microsoft Intune.
•	For iOS/iPadOS, download the **Microsoft Tunnel** app from the Apple **App Store**. See Add iOS store apps to Microsoft Intune. 

For more information on deploying apps with Intune, see  Add apps to Microsoft Intune. 

## Create a VPN profile
After the Microsoft Tunnel is installed on a server, and devices have installed the Microsoft Tunnel app, you can deploy VPN profiles to direct devices to use the tunnel. To do so, you’ll create VPN profiles with a connection type of Microsoft Tunnel.
 
### Android
1.	Sign in to [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices** > **Configuration profiles** > **Create profile**.

2.	For *Platform*, select **Android Enterprise**, and then for *Profile* select **VPN** from for either *Device Owner Only* or *Work Profile Only*, and then select **Create**.

3.	On the **Basics** tab, enter a *Name* and *Description* *(optional)* and select **Next**.

4.	For *Connection type* select **Microsoft Tunnel**, and then Configure the following:
•	Base VPN:
•	For *Connection name*, specify a name that will display to users. 
•	For *Microsoft Tunnel Site*, select the tunnel Site that this VPN profile will use. 
•	Per-app VPN: 
Apps that are assigned in the per-app VPN profile send app traffic to the tunnel. 
•	To enable a per-app VPN, select **Add** and then browse to apps you’ve imported to Intune. These can be custom or public apps. 
•	Always-on VPN:
For *Always-on VPN*, select *Enable* to set the VPN client to automatically connect and reconnect to the VPN. Always-on VPN connections stay connected.  
•	Proxy: 
Configure proxy server details for your environment.  
 
For more information about VPN settings, see [Android Enterprise device settings to configure VPN](../configuration/vpn-settings-android-enterprise.md)

5.	On the **Assignments** tab, configure groups that will receive this profile. 

6.	On the **Review + create** tab, review the details for this profile and select **Create** to save it.  
  
### iOS

1.	Sign in to [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices** > **Device Configuration** > **Create profile**.
2.	For *Platform*, select **iOS/iPadOS**, and then for *Profile* select **VPN**, and then **Create**. 
3.	On the **Basics** tab, enter a *Name* and *Description* *(optional)* and select **Next**.

4.	For *Connection type* select **Microsoft Tunnel**, and then Configure the following:
•	Base VPN:
•	For *Connection name*, specify a name that will display to users. 
•	For *Microsoft Tunnel Site*, select the tunnel Site that this VPN profile will use. 
•	Per-app VPN: 
•	To enable a per-app VPN, select **Enable**. Additional configuration steps are required for iOS per-app VPNs. For more information see [Per-App VPN for iOS/iPadOS](../configuration/vpn-setting-configure-per-app.md).
•	Proxy: 
Configure proxy server details for your environment.  

## Upgrade Microsoft Tunnel
When there are updates for Microsoft Tunnel, the upgrade of your existing tunnel servers is managed automatically by Intune in a rolling upgrade: 
•	Intune upgrades the tunnel servers in a Site one server at a time.
•	After a successful upgrade of a server, Intune waits a short period of time before starting the upgrade of the next server. 
•	This process continues until all servers in a Site have updated to the new version.  

## Uninstall the Microsoft Tunnel
To uninstall the product, run **./mst-cli uninstall** from the Linux server as root.

## Next steps
[Monitor Microsoft Tunnel](ms-tunnel-monitor.md)


# Monitor Microsoft Tunnel
ms-tunnel-montior.md
After installation of Tunnel Gateway, you can view the server configuration and server health in the Microsoft Endpoint Manager admin center (endpoint.microsoft.com).  In the admin center, go to *Tenant administration* > *Microsoft Tunnel Gateway*, and select the **Health status** tab.  
 
*Microsoft Tunnel is in public preview*.

While in preview, Health status only shows whether the server has connected in the last 5 minutes or not.  Future enhancements will add additional details.

## Use mst-cli command line tool
In addition to the Microsoft Endpoint Manager admin center UI, you can use the **mst-cli** command line tool to get information about the Microsoft Tunnel server.  This file is added to the Linux server when the Microsoft Tunnel installs and is found at: **/usr/sbin/mst-cli**.
For more information and command line examples, see [mst-cli command line tool for Microsoft Tunnel)(../protect/ms-tunnel-reference.md#mst-cli-command-line-tool-for-microsoft-tunnel)

## Next steps
[Reference for Microsoft Tunnel](../protect/ms-tunnel-reference.md)


# Reference for Microsoft Tunnel
ms-tunnel-refernce.md
The information in this reference for Microsoft Tunnel is provided to support installation and maintenance of the tunnel installation in your environment. 
## mst-cli command line tool for Microsoft Tunnel

**Mst-cli** is a command line tool for use with Microsoft Tunnel. This tool is available on the Linux server after the tunnel completes installation and is found at **/usr/sbin/mst-cli**.   Some tasks you can use this tool to complete include: 
-	Get information about the tunnel server. 
-	Set or update the configuration of the tunnel server.
-	Restart the tunnel server.
-	Uninstall the tunnel server.
The following are common command line uses of the tool.
**Command Line Interface**:
•	`mst-cli –help` - Usage: **mst-cli [command]**

Commands:
•	`agent` - Operate on the agent component.
•	`server` - Operate on the server component.
•	`uninstall` - Uninstall the Microsoft Tunnel.
•	` eula` - Show the EULA.
•	`import_cert` - Import the TLS certificate.
 
•	`mst-cli agent –help` - Usage: **mst-cli agent [command]**

Commands: 
•	`logs` - Show the agent logs (-h for more information).
•	`status` - Show the agent status.
•	` start` - Start the agent service.
•	`stop` - Stop the agent service.
•	`restart` - Restart the agent service.

•	`mst-cli agent logs   help` - Usage: **mst-cli agent logs [flags]**

Flags:
•	`-f, --follow` - Follow log output. The default is false.
•	`--since string` - Show logs since TIMESTAMP.
•	`--tail uint` - Output the specified number of LINES at the end of the logs.  Defaults to zero (0), which prints all lines.
 `-t, --timestamps` - Output the timestamps in the log.

•	`mst-cli agent status` - The following is an example of the results you might see: 
State: running
Health: healthy
•	`mst-cli agent start` - Starts the agent if it is stopped.
•	`mst-cli agent stop` - Stops the agent.  Must be started manually after stopped.
•	`mst-cli agent restart` - Restarts the agent.
•	`mst-cli server --help` - Usage: **mst-cli server [command]**

Commands:
•	`logs` - Show the server logs. Use **-h** for more information.
•	`status` - Show the server status.
•	 `start` - Start the server service.
•	 `stop` - Stop the server service.
•	`restart` - Restart the server service.
•	`show` - Show various server stats. Use **-h** for mor information.
•	`mst-cli server logs –help` - Usage: **mst-cli server logs [flags]**

Flags:
•	`-f, --follow` - Follow log output. The default is false.
•	`--since string` - Show logs since TIMESTAMP
•	`--tail uint` - Output the specified number of LINES at the end of the logs.  Defaults to zero (0), which prints all lines.
•	`-t, --timestamps` - Output the timestamps in the log.
•	`mst-cli server status`
State: running
Health: healthy
•	`mst-cli server start` - Starts the server if it is stopped.
•	`mst-cli server stop` - Stops the server.  Must be started manually after stopped.
•	`mst-cli server restart` - Restarts the server.
•	`mst-cli server show`
•	`show status` - Prints the status and statistics of the server.
•	`show users` - Prints the connected users.
•	`show ip bans` - Prints the banned IP addresses.
•	`show ip ban points` - Prints all the known IP addresses which have points.
•	`show iroutes` - Prints the routes provided by users of the server.
•	`show sessions all` - Prints all the session IDs.
•	`show sessions valid` - Prints all the valid for reconnection sessions.
•	`show session [SID]` - Prints information on the specified session.
•	`show user [NAME]` - Prints information on the specified user.
•	`show id [ID]` - Prints information on the specified ID.
•	`show events` - Provides information about connecting users.
•	`show cookies all` - Alias for show sessions all.
•	`show cookies valid` - Alias for show sessions valid.

 ## Environment variables 
Following are environment variables you might want to configure when you install the Microsoft Tunnel software on the Linux server. These variables are found in the environment file **/etc/mstunnel/env.sh**: 

•	**http_proxy**=[address] - The HTTP address for your proxy server. 
•	**https_proxy**=[address] - The HTTPs address for your proxy server. 

## Data Paths  
The following file directories are created on the Linux server during the install of Microsoft Tunnel. 
Path/File 	Description 	Permissions 
/…/mstunnel 	The root directory for all configuration. 	Owner root, Group mstunnel 
/…/mstunnel/admin-settings.json 	Contains the settings for the server install.  *This file is managed by Intune and should not be edited manually*. 	  
/…/mstunnel/certs 	The directory where the TLS certificate is stored.  	Owner root, Group mstunnel. 
   
 
/…/mstunnel/private 	The directory where the Intune Agent certificate and the TLS private key are stored.  
 	Owner root, Group mstunnel  
 
 
## Files created by install /etc/mstunnel
•	**admin-settings.json**:
•	Contains the serialized *Server configuration* from Intune.
•	Created after the server has enrolled.

•	**agent-info.json**:
•	Created when the enrollment is complete.
•	"AgentId, IntuneTenantId, AADTenantId and the agent certificate RenewalDate".
•	Updated on agent certificate renewal.

•	**private/agent.p12**:
•	PFX certificate used for agent authentication to Intune.
•	Automatically renewed.

•	**version-info.json**:
•	Contains version information for the various components.
•	"ConfigVersion, DockerVersion, AgentImageHash, AgentCreateDate, ServerImageHash, ServerCreateDate"

•	**ocserv.conf**:
•	Server configuration
•	**Images_configured**:

## The Docker images used to create the containers
- agentImageDigest
- serverImageDigest

### Example of admin-settings.json  
{ 
"PolicyName": "Auto Generated Policy for rh7vm", 
   "DisplayName": "rh7vm Policy", 
   "Description": "This policy was auto generated for rh7vm",  
   "Network": "169.100.0.0/16",   
   "DNSServers": ["168.63.129.16"],  
   "DefaultDomainSuffix": "nmqjwlanybmubp4imht0k2b4qd.xx.internal.cloudapp.net",  
   "RoutesInclude": ["default"],   
   "RoutesExclude": [],   
   "ListenPort": 443  
} 
 
 
Admin Setting 	Description 
PolicyName 	The name of the settings policy. You can choose the name. 
DisplayName 	The short display name. You can choose the name. 
Description 	The description of the policy. You can choose the description. 
Network 	The network with mask that will be used to assign clients virtual addresses. This does not need to change unless you have a conflict. This setting will support 64K clients. 
DNSServers 	The list of DNS servers that the client should use.  These are able to resolve the addresses of internal resources. 
DefaultDomainSuffix 	The Domain suffix that a client appends to the host name when trying to resolve resources. 
RoutesInclude 	The list of routes that will be routed via the VPN.  The default is all routes. 
RoutesExclude 	The list of routes that should bypass the VPN. 
ListenPort 	The port that the VPN server will receive traffic on. 
 



## Docker commands
The following are common commands for Docker which can be of use if you must investigate problems on a tunnel server. 
**Command Line Interface**:
•	**Docker ps –a – see all containers**
•	**mstunnel-server** – This container runs the ocserv server components.
•	Inbound Port 443 or configure port
•	**mstunnel-agent** - This container runs the Intune connector
•	Outbound Port 443
•	If you need to restart docker:
•	**systemctl restart docker**
•	To run something in a container:
•	**docker exec –it mstunnel-server bash**
•	**docker exec –it mstunnel-agent bash**
## Linux commands
The following are common Linux commands you might use with a tunnel server.
•	`sudo su` – Makes you root on the box.  Use this before running these commands and installing mstunnel-setup.  Usually you want to do this only when running certain commands (like sudo mkdir myfolder to make a folder called myfolder).
•	`ls` – list contents of the directory.
•	`ls – l` – List contents of directory including timestamps.
•	`cd` – change to another directory (cd /etc/test/stuff changes you from the root directory to the etc subfolder to the test subfolder to the stuff folder.
•	`cp <source> <destination>` - Useful for copying the certs to the right location.
•	`ln –s <source> <target>` - Create a softlink.
•	`curl <URL>` – Checks access to a website such as curl https://microsoft.com.
•	`./<filename`>` -  Run a script.



