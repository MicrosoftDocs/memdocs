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

# Enable third-party updates 

*Applies to: System Center Configuration Manager version 1806*

Beginning with version 1806, the **Third-Party Software Update Catalogs** node in the Configuration Manager console allows you to subscribe to third-party catalogs, publish their updates to your software update point (SUP), and then deploy them to clients.  <!--1357605, 1352101, 1358714-->


## Prerequisites 
- Sufficient disk space on the top-level software update point's WSUSContent folder to store the source binary content for third-party software updates.
     - The amount of required storage varies based on the vendor, types of updates, and specific updates that you publish for deployment.
    - If you need to move the WSUSContent folder to another drive with more free space, see the [How to change the location where WSUS stores updates locally](https://blogs.technet.microsoft.com/sus/2008/05/19/wsus-how-to-change-the-location-where-wsus-stores-updates-locally/) blog post.
- The third-party software update synchronization service requires internet access.
    - For the partner catalogs list, download.microsoft.com over HTTPS port 443 is needed. 
    -  Internet access to any third-party catalogs and update content files. Additional ports other than 443 may be needed.
    - Third-party updates use the same proxy settings as the SUP.

## Additional requirements when the SUP is remote from the top-level site server 

1. SSL must be enabled on the SUP when it's remote. 
    - [Configure SSL on WSUS](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/deploy/2-configure-wsus#bkmk_2.5.ConfigSSL)
    - [Configure SSL on the SUP](../get-started/install-a-software-update-point.md#configure-ssl-communications-to-wsus)

2. To allow the creation of the self-signed WSUS certificate: 
   - Remote registry should be enabled on the SUP server.
   -  The **WSUS server connection account** should have remote registry permissions on the SUP/WSUS server. 

    If the remote registry items aren't possible, do the following step:    
   - In the registry key `HKLM\Software\Microsoft\Update Services\Server\Setup`, create a new DWORD named **EnableSelfSignedCertificates** with a value of `1`. 

3. To enable installing the certificate to the Trusted Publishers and Trusted Root stores on the remote SUP server:
   - The **WSUS server connection account** should have remote administration permissions on the SUP server.

    If this item isn't possible, export the certificate from the local computer's WSUS store into the Trusted Publisher and Trusted Root stores. 

> [!NOTE] 
>The **WSUS server connection account** can be identified by viewing the **Proxy and Account Settings** tab on the Site System role properties of the SUP. If an account is not specified, the site server's computer account is used.

## Enable third-party updates on the SUP
If you enable this option, you can subscribe to third-party update catalogs in the Configuration Manager console. You can then publish those updates to WSUS and deploy them to clients. The following steps should be run once per hierarchy to enable and set up the feature for use. The steps may need to be rerun if you ever replace the top-level SUP's WSUS server. 

1. In the Configuration Manager console, go to the **Administration** workspace. Expand **Site Configuration**, and select the **Sites** node.
2. Select the top-level site in the hierarchy. In the ribbon, click **Configure Site Components**, and select **Software Update Point**.
3. Switch to the **Third-Party Updates** tab. Select the option **Enable third-party software updates**.


## Configure the WSUS signing certificate
You'll need to decide if you want Configuration Manager to automatically manage the third-party WSUS signing certificate, or if you need to manually configure the certificate. 

### Automatically manage the WSUS signing certificate
If you don't have a requirement to use PKI certificates, you can choose to automatically manage the signing certificates for third-party updates.

1. In the Configuration Manager console, go to the **Administration** workspace. Expand **Site Configuration**, and select the **Sites** node.
2. Select the top-level site in the hierarchy. In the ribbon, click **Configure Site Components**, and select **Software Update Point**.
3. Switch to the **Third-Party Updates** tab. Select the option **Configuration Manager manages the certificate**. 
4. A new certificate of type **Third-party WSUS Signing** is created in the **Certificates** node under **Security** in the **Administration** workspace.  

### Manually manage the WSUS signing certificate
If you need to manually configure the certificate, such as needing to use a PKI certificate, you'll need to use [System Center Updates Publisher](../tools/updates-publisher-options.md#update-server) to do so.  

1. Configure the signing certificate using [System Center Updates Publisher](../tools/updates-publisher-options.md#update-server).
2. In the Configuration Manager console, go to the **Administration** workspace. Expand **Site Configuration**, and select the **Sites** node.
3. Select the top-level site in the hierarchy. In the ribbon, click **Configure Site Components**, and select **Software Update Point**.
4. Switch to the **Third-Party Updates** tab. Select the option **Manually manage the certificate**.


## Enable third-party updates on the clients
Enable third-party updates on the clients in the client settings. The setting sets the Windows Update agent policy for [Allow signed updates for an intranet Microsoft update service location](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/deploy/4-configure-group-policy-settings-for-automatic-updates#BKMK_comp3). This client setting also installs the WSUS signing certificate to the Trusted Publisher store on the client. Run these steps for each custom client setting you want to use for third-party updates. For more information, see the [About client settings](/sccm/core/clients/deploy/about-client-settings#Enable-third-party-software-updates) article.

1. In the Configuration Manager console, go to the **Administration** workspace and select the **Client Settings** node.
2. Select an existing custom client setting or create a new one. 
3. Select the **Software Updates** tab on the left-hand side. If you don't have this tab, ensure that the **Software Updates** box is enabled.
4. Set **Enable third-party software updates** to **Yes**. 


## Add a custom catalog

1. Go to the **Software Updates Library** workspace, expand **Software updates**, and select the **Third-Party Software Update Catalogs** node. 
2. Click **Add Custom Catalog** in the ribbon. 
3. Select the catalog to subscribe to and click **Add Custom Catalog** in the ribbon.  
4. On the **General** page, specify the following: 
    - **Download URL**: A valid HTTPS address of the custom catalog.
    - **Publisher**: The name of the organization that publishes the catalog. 
    - **Name**: The name of the catalog to display in the Configuration Manager Console. 
    - **Description**: A description of the catalog. 
    - **Support URL** (optional): A valid HTTPS address of a website to get help with the catalog. 
    - **Support Contact** (optional): Contact information to get help with the catalog. 

<!--this feels incomplete, check with Aaron for screenshots-->

## Subscribe to a third-party catalog and sync updates

Perform the following steps for each third-party catalog to which you want to subscribe:  

1. In the Configuration Manager console, go to the **Software Library** workspace. Expand **Software Updates** and select the **Third-Party Software Update Catalogs** node.  
2. Select the catalog to subscribe and click **Subscribe to Catalog** in the ribbon. 
3. Review and approve the catalog certificate.
    >[!NOTE]
    >When you subscribe to a third-party software update catalog, the certificate that you review and approve in the wizard is added to the site. This certificate is of type **Third-party Software Updates Catalog**. You can manage it from the **Certificates** node under **Security** in the **Administration** workspace.  
4. Complete the wizard. 
    - After initial subscription, the catalog should start to download in a few minutes. 
     - The catalog synchronizes automatically every 7 days.
     - Click **Sync now** in the ribbon to sync it outside of the schedule.
5. After the catalog is downloaded, the product metadata needs to be synchronized to the software update point. [Manually start the software updates synchronization](../get-started/synchronize-software-updates.md#manually-start-software-updates-synchronization) to synchronize the product information.
6. Once the product information is synchronized, you can configure the new product to synchronize its updates into Configuration manager. 




