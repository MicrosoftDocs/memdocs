---
title: Enable third party updates
titleSuffix: Configuration Manager
description: Enable third party updates in Configuration Manager
ms.date: 07/13/2018
ms.prod: configuration-manager
ms.technology: configmgr-sum 
ms.topic: conceptual
ms.assetid: 946b0f74-0794-4e8f-a6af-9737d877179b
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Enable third party updates 

*Applies to: System Center Configuration Manager (Current Branch)*

Beginning with version 1806, the **Third-Party Software Update Catalogs** node in the Configuration Manager console allows you to subscribe to third-party catalogs, publish their updates to your software update point (SUP), and then deploy them to clients.  <!--1357605, 1352101, 1358714-->


## Prerequisites 
- Sufficient disk space on the top level software update point's WSUSContent folder to store the source binary content for third-party software updates.
     - The amount of required storage varies based on the vendor, types of updates, and specific updates that you publish for deployment.
    - If you need to move the WSUSContent folder to another drive with more free space, see the [How to change the location where WSUS stores updates locally](https://blogs.technet.microsoft.com/sus/2008/05/19/wsus-how-to-change-the-location-where-wsus-stores-updates-locally/) blog post.
- The third-party software update synchronization service requires internet access.
    - For the partner catalogs list, download.microsoft.com over HTTPS port 443 is needed. 
    -  Internet access to any third-party catalogs and update content files. Additional ports other than 443 may be needed for this.
    - Third party updates use the same proxy settings as the SUP.

## Additional requirements when the SUP is remote from the top-level site server 

1. SSL must be enabled on the SUP when it is remote. 
    - [Configure SSL on WSUS](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/deploy/2-configure-wsus#bkmk_2.5.ConfigSSL)
    - [Configure SSL on the SUP](../get-started/install-a-software-update-point#configure-ssl-communications-to-wsus)

2. To allow the creation of the self-signed WSUS certificate: 
   - Remote registry should be enabled on the SUP server.
   -  The **WSUS server connection account** should have remote registry permissions on the SUP/WSUS server. 

    If the remote registry items are not possible, do the following:    
   - In the registry key `HKLM\Software\Microsoft\Update Services\Server\Setup`, create a new DWORD named **EnableSelfSignedCertificates** with a value of `1`. 

3. To enable installing the certificate to the Trusted Publishers and Trusted Root stores on the remote SUP server:
   - The **WSUS server connection account** should have remote administration permissions on the SUP server.

    If this item is not possible, export the certificate from the local computer's WSUS store into the Trusted Publisher and Trusted Root stores. 

> [!NOTE] 
>The **WSUS server connection account** can be identified by viewing the **Proxy and Account Settings** tab on the Site System role properties of the SUP. If an account is not specified, the site server's computer account is used.

## Enable the third party updates feature on the SUP
<!--You can enable the Configuration Manager site to automatically configure the certificate. The site communicates with WSUS to generate a certificate for this purpose. Configuration Manager then continues to deploy that certificate to clients. -->

### Enable third party updates on the SUP
The following steps should be run once per hierarchy to enable and set up the feature for use. The steps may need to be re-run if you ever replace the top-level SUP's WSUS server. 

1. In the Configuration Manager console, go to the **Administration** workspace. Expand **Site Configuration**, and select the **Sites** node.
2. Select the top-level site in the hierarchy. In the ribbon, click **Configure Site Components**, and select **Software Update Point**.
3. Switch to the **Third Party Updates** tab. Select the option to **Enable third-party software updates**.


## Configure the WSUS signing certificate
You will need to decide if you want Configuration Manager to automatically manage the third-party WSUS signing certificate, or if you need to manually configure the certificate. 

### Automatically managae the WSUS signing certificate
If you don't have a requirement to use PKI certificates and you have never used third party updates with SCCM, it is generally easier to allow SCCM to automatically manage the signing certificates.   

### Manually manage the WSUS signing certificate
If you need to manually configure the certificate, such as needing to use a PKI certificate, you will need to use [System Center Updates Publisher](../tools/updates-publisher-options#update-server) to do so.  


## Enable third party updates on the clients
Enable third party updates on the clients by enabling it in the client settings. These steps need to be run for each custom client setting you want to use for third party updates. For more information, see the [About client settings](/sccm/core/clients/deploy/about-client-settings#Enable-third-party-software-updates) article

1. In the Configuration Manager console, go to the **Administration** workspace and select the **Client Settings** node.
2. Select an existing custom client setting or create a new one. 
3. Select the **Software Updates** tab on the left hand side. If you do not have this tab, ensure that the **Software Updates** box is enabled.
4. Set **Enable third party software updates** to **Yes**. 


