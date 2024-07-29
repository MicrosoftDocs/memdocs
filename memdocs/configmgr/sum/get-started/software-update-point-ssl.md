---
title: Configure a software update point to use TLS/SSL with a PKI certificate tutorial
titleSuffix: Configuration Manager
description: Tutorial - Configure Windows Server Update Services (WSUS) servers and the software update points to use TLS/SSL with a PKI certificate.
author: BalaDelli
ms.author: baladell
manager: apoorvseth
ms.date: 01/14/2022
ms.topic: tutorial
ms.service: configuration-manager
ms.subservice: software-updates
# Customer intent: As a Configuration Manager admin, I want to enable my WSUS servers and software update points to use TLS/SSL to reduce the ability of a potential attacker to remotely compromise a client and elevate privileges.
ms.localizationpriority: medium
ms.reviewer: mstewart,aaroncz 
ms.collection: tier3
---

# Tutorial: Configure a software update point to use TLS/SSL with a PKI certificate

*Applies to: Configuration Manager (current branch)*

Configuring Windows Server Update Services (WSUS) servers and their corresponding software update points (SUP) to use TLS/SSL may reduce the ability of a potential attacker to remotely compromise a client and elevate privileges. To ensure that the best security protocols are in place, we highly recommend that you use the TLS/SSL protocol to help secure your software update infrastructure. This article walks you through the steps required to configure each of your WSUS servers and the software update point to use HTTPS. For more information about securing WSUS, see the [Secure WSUS with the Secure Sockets Layer Protocol](/windows-server/administration/windows-server-update-services/deploy/2-configure-wsus#25-secure-wsus-with-the-secure-sockets-layer-protocol) article in the WSUS documentation.

In this tutorial, you will:
> [!div class="checklist"]
> * Obtain a PKI certificate, if needed
> * Bind the certificate to the WSUS Administration website
> * Configure the WSUS web services to require SSL
> * Configure the WSUS application to use SSL
> * Verify the WSUS console connection can use SSL
> * Configure the software update point to require SSL communication to the WSUS server
> * Verify functionality with Configuration Manager

## Considerations and limitations

WSUS uses TLS/SSL to authenticate client computers and downstream WSUS servers to the upstream WSUS server. WSUS also uses TLS/SSL to encrypt update metadata. WSUS doesn't use TLS/SSL for an update's content files. The content files are signed and the hash of the file is included in the update's metadata. Before the files are downloaded and installed by the client, both the digital signature and hash are checked. If either check fails, the update won't be installed.

Consider the following limitations when you use TLS/SSL to secure a WSUS deployment:

- Using TLS/SSL increases the server workload. You should expect a small performance loss from encrypting all the metadata that is sent over the network.
- If you use WSUS with a remote SQL Server database, the connection between the WSUS server and the database server isn't secured by TLS/SSL. If the database connection must be secured, consider the following recommendations:
   - Move the WSUS database to the WSUS server.
   - Move the remote database server and the WSUS server to a private network.
   - Deploy Internet Protocol security (IPsec) to help secure network traffic.

When configuring WSUS servers and their software update points to use TLS/SSL, you may want to phase in the changes for large Configuration Manager hierarchies. If you choose to phase in these changes, start at the bottom of the hierarchy and move upwards ending with the central administration site.

## Prerequisites

This tutorial covers the most common method to obtain a certificate for use with Internet Information Services (IIS). Whichever method your organization uses, ensure that the certificate meets the [PKI certificate requirements](../../core/plan-design/network/pki-certificate-requirements.md) for a Configuration Manager software update point. As with any certificate, the certificate authority must be trusted by devices communicating with the WSUS server.

- A WSUS server with the software update point role installed
- Verify you've followed [best practices](/troubleshoot/mem/configmgr/windows-server-update-services-best-practices#disable-recycling-and-configure-memory-limits) on disabling recycling and configuring memory limits for WSUS before enabling TLS/SSL.
- One of the two following options:
   - An appropriate PKI certificate already in the WSUS server's **Personal** certificate store.
   - The ability to request and obtain an appropriate PKI certificate for the WSUS server from your Enterprise root certificate authority (CA).
      - By default, most certificate templates including the WebServer certificate template will only issue to Domain Admins. If the logged in user isn't a domain admin, their user account will need to be granted the **Enroll** permission on the certificate template.

## <a name="bkmk_pki"></a> Obtain the certificate from the CA if needed

If you already have an appropriate certificate in the WSUS server's **Personal** certificate store, skip this section and start with the [Bind the certificate](#bkmk_bind) section. To send a certificate request to your internal CA to install a new certificate, follow the instructions in this section.
 
1. From the WSUS server, open an administrative command prompt and run `certlm.msc`. Your user account needs to be a local administrator to manage certificates for the local computer.

   The Certificate Manager tool for the local device appears.

1. Expand **Personal**, then right-click on **Certificates**.
1. Select **All Tasks** then **Request New Certificate**.
1. Choose **Next** to begin certificate enrollment.
1. Choose the type of certificate to enroll. The certificate purpose is **Server Authentication** and the Microsoft certificate template to use is **Web Server** or a custom template that has **Server Authentication** specified as **Enhanced Key Usage**. You may be prompted for additional information to enroll the certificate. Typically, you'll specify the following information at minimum:

   - **Common name:** Found on the **Subject** tab, set the value to the WSUS server's FQDN.
   - **Friendly name:** Found on the **General** tab, set the value to a descriptive name to help you identify the certificate later.
   
   :::image type="content" source="media/certificate-properties.png" alt-text="Certificate properties window to specify more information for enrollment":::

1. Select **Enroll** then **Finish** to complete the enrollment.
1. Open the certificate if you want to see details about it such as the certificate's thumbprint.

> [!TIP]
> If your WSUS server is internet facing, you'll need the external FQDN in the Subject or Subject Alternative Name (SAN) in your certificate.

## <a name="bkmk_bind"></a> Bind the certificate to the WSUS Administration site

Once you have the certificate in the WSUS server's personal certificate store, bind it to the WSUS Administration site in IIS.

1. On the WSUS server, open Internet Information Services (IIS) Manager.
1. Go to **Sites** > **WSUS Administration**.
1. Select **Bindings** from either the action menu or by right-clicking on the site.
1. In the **Site Bindings** window, select the line for **https**, then select **Edit...**.

   - Don't remove the HTTP site binding. WSUS uses HTTP for the update content files.
   
1. Under the **SSL certificate** option, choose the certificate to bind to the WSUS Administration site. The certificate's friendly name is shown in the drop-down menu. If a friendly name wasn't specified, then the certificate's `IssuedTo` field is shown. If you're not sure which certificate to use, select **View** and verify the thumbprint matches the one you obtained.

   :::image type="content" source="media/edit-site-binding.png" alt-text="Edit Site Binding window with SSL certificate selection":::

1. Select **OK** when you're done, then **Close** to exit the site bindings. Keep Internet Information Services (IIS) Manager open for the next steps.



## <a name="bkmk_webserv"></a> Configure the WSUS web services to require SSL

1. In IIS Manager on the WSUS server, go to **Sites** > **WSUS Administration**.
1. Expand the WSUS Administration site so you see the list of web services and virtual directories for WSUS.
1. For each of the below WSUS web services:
   - ApiRemoting30
   - ClientWebService
   - DSSAuthWebService
   - ServerSyncWebService
   - SimpleAuthWebService

   Make the following changes:
   
   1. Select **SSL Settings**.
   1. Enable the **Require SSL** option.
   1. Verify the **Client certificates** option is set to **Ignore**.
   1. Select **Apply**.

Don't set the SSL settings at the top-level WSUS Administration site since certain functions, such as content, need to use HTTP.

## <a name="bkmk_wsusutil"></a> Configure the WSUS application to use SSL

Once the web services are set to require SSL, the WSUS application needs to be notified so it can do some additional configuration to support the change.

1. Open an admin command prompt on the WSUS server. The user account running this command must be a member of either the WSUS Administrators group or the local Administrators group.
1. Change directory to the tools folder for WSUS:

   `cd "c:\Program Files\Update Services\Tools"`
   
1. Configure WSUS to use SSL with the following command:

    `WsusUtil.exe configuressl server.contoso.com`
   
   Where *server.contoso.com* is the FQDN of the WSUS server.
   
1. WsusUtil returns the URL of the WSUS server with the port number specified at the end. The port will be either 8531 (default) or 443. Verify the URL returned is what you expected. If something was mistyped, you can run the command again.

   :::image type="content" source="media/wsusutil.png" alt-text="The wsusutil configuressl command returning the HTTPS URL for WSUS":::

> [!TIP] 
> If your WSUS server is internet facing, specify the external FQDN when running `WsusUtil.exe configuressl`.

## <a name="bkmk_wsus_console"></a> Verify the WSUS console can connect using SSL

The WSUS console uses the ApiRemoting30 web service for connection. The Configuration Manager software update point (SUP) also uses this same web service to direct WSUS to take certain actions such as:

- Initiating a software update synchronization
- Setting the proper upstream server for WSUS, which is dependent on where the SUP's site resides in your Configuration Manager hierarchy
- Adding or removing products and classifications for synchronization from the hierarchy's top-level WSUS server.
- Removing expired updates

Open the WSUS console to verify you can use an SSL connection to the WSUS server's ApiRemoting30 web service. We'll test some of the other web services later.

1. Open the WSUS console and select **Action** > **Connect to Server**.
1. Enter the FQDN of the WSUS server for the **Server name** option.
1. Choose the **Port number** returned in the URL from WSUSutil.

1. The **Use Secure Sockets Layer (SSL) to connect to this server** option automatically enables when either 8531 (default) or 443 are chosen.

   :::image type="content" source="media/connect-wsus-console.png" alt-text="Connect to the WSUS console over the HTTPS port":::
       
1. If your Configuration Manager site server is remote from the software update point, launch the WSUS console from the site server and verify the WSUS console can connect over SSL.
   - If the remote WSUS console can't connect, it likely indicates a problem with either trusting the certificate, name resolution, or the port being blocked.

## <a name="bkmk_cm_sup"></a> Configure the software update point to require SSL communication to the WSUS server

Once WSUS is set up to use TLS/SSL, you'll need to update the corresponding Configuration Manager software update point to require SSL too. When you make this change, Configuration Manager will:

- Verify it can configure the WSUS server for the software update point
- Direct clients to use the SSL port when they're told to scan against this WSUS server.

To configure the software update point to require SSL communication to the WSUS server, do the following steps: 

1. Open the Configuration Manager console and connect to either your central administration site or the primary site server for the software update point you need to edit.
1. Go to **Administration** > **Overview** > **Site Configuration** > **Servers and Site System Roles**.
1. Select the site system server where WSUS is installed, then select the software update point site system role.
1. From the ribbon, choose **Properties**.
1. Enable the **Require SSL communication to the WSUS server** option.

   :::image type="content" source="media/sup-properties.png" alt-text="SUP properties showing the option for Require SSL communication to the WSUS server":::
   
1. In the [**WCM.log**](../../core/plan-design/hierarchy/log-files.md#BKMK_SUPLog) for the site, you'll see the following entries when you apply the change:

   ```
   SCF change notification triggered.
   Populating config from SCF
   Setting new configuration state to 1 (WSUS_CONFIG_PENDING)
   ...
   Attempting connection to local WSUS server
   Successfully connected to local WSUS server
   ...
   Setting new configuration state to 2 (WSUS_CONFIG_SUCCESS)
   ```

Log file examples have been edited to remove unneeded information for this scenario.  

## <a name="bkmk_cm_verify"></a> Verify functionality with Configuration Manager

### Verify the site server can sync updates

1. Connect the Configuration Manager console to the top-level site.
1. Go to **Software Library** > **Overview** > **Software Updates** > **All Software Updates**.
1. From the ribbon, select **Synchronize Software Updates**.
1. Select **Yes** to the notification asking if you want to initiate a site-wide synchronization for software updates.

   - Since the WSUS configuration changed, a full software updates synchronization will occur rather than a delta synchronization.
   
1. Open the **wsyncmgr.log** for the site. If you're monitoring a child site, you'll need to wait for the parent site to finish synchronization first. Verify that the server syncs successfully by reviewing the log for entries similar to the following:

   ```
   Starting Sync
   ...
   Full sync required due to changes in main WSUS server location.
   ...
   Found active SUP SERVER.CONTOSO.COM from SCF File.
   ...
   https://SERVER.CONTOSO.COM:8531
   ...
   Done synchronizing WSUS Server SERVER.CONTOSO.COM
   ...
   sync: Starting SMS database synchronization
   ...
   Done synchronizing SMS with WSUS Server SERVER.CONTOSO.COM
   ```

### <a name="bkmk_cm_verify-client"></a> Verify a client can scan for updates

When you change the software update point to require SSL, Configuration Manager clients receive the updated WSUS URL when it makes a location request for a software update point. By testing a client, we can:
-  Determine if the client trusts the WSUS server's certificate. 
- If the SimpleAuthWebService and the ClientWebService for WSUS are functional.
-  That the WSUS content virtual directory is functional, if the client happened to get a EULA during the scan

1. Identify a client that scans against the software update point recently changed to use TLS/SSL. Use [Run scripts](../..//apps/deploy-use/create-deploy-scripts.md) with the below PowerShell script if you need help with identifying a client:

   ```powershell
   $Last = (Get-CIMInstance -Namespace "root\CCM\Scanagent" -Class "CCM_SUPLocationList").LastSuccessScanPath
   $Current= Write-Output (Get-CIMInstance -Namespace "root\CCM\Scanagent" -Class "CCM_SUPLocationList").CurrentScanPath
   Write-Host "LastGoodSUP- $last"
   Write-Host "CurrentSUP- $current"
   ```
   > [!TIP]
   > Open this script in community hub. For more information, see [Direct links to community hub items](../../core/servers/manage/community-hub.md).
1. Run a software update scan cycle on your test client. You can force a scan with the following PowerShell script:

   ```powershell
   Invoke-WMIMethod -Namespace root\ccm -Class SMS_CLIENT -Name TriggerSchedule "{00000000-0000-0000-0000-000000000113}"
   ```
   > [!TIP]
   > Open this script in community hub. For more information, see [Direct links to community hub items](../../core/servers/manage/community-hub.md).

1. Review the client's **ScanAgent.log** to verify the message to scan against the software update point was received.

   ```
   Message received: '<?xml version='1.0' ?>
   <UpdateSourceMessage MessageType='ScanByUpdateSource'>
	  <ForceScan>TRUE</ForceScan>
	  <UpdateSourceIDs>
			<ID>{A1B2C3D4-1234-1234-A1B2-A1B2C3D41234}</ID>
	  </UpdateSourceIDs>
	</UpdateSourceMessage>'
   ```

1. Review the **LocationServices.log** to verify that the client sees the correct WSUS URL.
**LocationServices.log**

   ```
   WSUSLocationReply : <WSUSLocationReply SchemaVersion="1
   ...
   <LocationRecord WSUSURL="https://SERVER.CONTOSO.COM:8531" ServerName="SERVER.CONTOSO.COM"
   ...
   </WSUSLocationReply>
   ```

1. Review the **WUAHandler.log** to verify that the client can successfully scan.

   ```
   Enabling WUA Managed server policy to use server: https://SERVER.CONTOSO.COM:8531
   ...
   Successfully completed scan.
   ```

## <a name="bkmk_cert_pinning"></a> TLS certificate pinning for devices scanning HTTPS-configured WSUS servers
<!--8913032-->
*(Introduced in 2103)*

Starting in Configuration Manager 2103, you can further increase the security of HTTPS scans against WSUS by enforcing certificate pinning. To fully enable this behavior, add certificates for your WSUS servers to the new `WindowsServerUpdateServices` certificate store on your clients and ensure certificate pinning is enabled through **Client Settings**. For more information about the changes to the Windows Update Agent, see [Scan changes and certificates add security for Windows devices using WSUS for updates - Microsoft Tech Community](https://techcommunity.microsoft.com/t5/windows-it-pro-blog/scan-changes-and-certificates-add-security-for-windows-devices/ba-p/2053668).

### Prerequisites for enforcing TLS certificate pinning for Windows Update client

- Configuration Manager version 2103
- Ensure your WSUS servers and software update points are configured to use TLS/SSL
- Add the certificates for your WSUS servers to the new `WindowsServerUpdateServices` certificate store on your clients
   - When using certificate pinning with a cloud management gateway (CMG), the `WindowsServerUpdateServices` store needs the CMG certificate. If clients switch from internet to VPN both the CMG and WSUS server certificates are needed in the `WindowsServerUpdateServices` store. <!--12590425-->

> [!Note]
> Software update scans for devices will continue to run successfully using the default value of **Yes** for the **Enforce TLS certificate pinning for Windows Update client for detecting updates** client setting. This includes scans over both HTTP and HTTPS. The certificate pinning doesn't take effect until a certificate is in the client's `WindowsServerUpdateServices` store and the WSUS server is configured to use TLS/SSL.



### Enable or disable TLS certificate pinning for devices scanning HTTPS-configured WSUS servers

1. From the Configuration Manager console, go to **Administration** > **Client Settings**.
1. Choose the **Default Client Settings** or a custom set of client settings, then select **Properties** from the ribbon.
1. Select the **Software Updates** tab in the **Client settings**
1. Choose one of the following options for the **Enforce TLS certificate pinning for Windows Update client for detecting updates** setting:
   - **No**: Don't enable enforcement of TLS certificate pinning for WSUS scanning
   - **Yes**: Enables enforcement of TLS certificate pinning for devices during WSUS scanning (default)
1. [Verify clients](#bkmk_cm_verify-client) can scan for updates.

## Next steps

[Deploy software updates](../deploy-use/deploy-software-updates.md)
