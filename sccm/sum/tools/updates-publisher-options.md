---
title: "Configure options"
titleSuffix: "Configuration Manager"
description: "Configure options for using System Center Updates Publisher"
ms.custom: na
ms.date: 4/29/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4e620080-5400-45bb-87c2-fbdbc8aeacac
caps.latest.revision: 1
author: mestew
ms.author: mstewart
manager: angrobe
robots: NOINDEX, NOFOLLOW
---
# Configure options for Updates Publisher

*Applies to: System Center Updates Publisher*

Review and configure the options and related settings that affect the operation of Updates Publisher.

To access the Updates Publisher options, in upper left corner of the console, click on the **Updates Publisher** **Properties** tab, and then choose **Options**.

![Options](media/properties1.png)   


Options are divided into the following:

-   Update Server
-   ConfigMgr Server
-   Proxy Settings
-   Trusted Publishers
-   Advanced
-   Updates
-   Logging

## Update Server
You must configure Updates Publisher to work with update server like Windows Server Update Services (WSUS) before you can [publish updates](/sccm/sum/tools/manage-updates-with-updates-publisher#publish-updates-and-bundles). This includes specifying the server, methods to connect to that server when it is remote from the console, and a certificate to use to digitally sign updates you publish.

-   **Configure an update server**. When you configure an update server, select the top-level WSUS server (update server) in your Configuration Manager hierarchy so that all child sites have access to the updates that you publish.

  If your update server is remote from your Updates Publisher server, specify the fully qualified domain name (FQDN) of the server, and if you will connect by SSL. When you connect by SSL, the default port changes from 8530 to 8531. Ensure the port you set matches what is in use by your update server.

    > [!TIP]  
    > If you do not configure an update server, you can still use Updates Publisher to author software updates.

-   **Configure the signing certificate**. You must configure and successfully connect to an update server before you can configure the signing certificate.

    Updates Publisher uses the signing certificate to sign the software updates that are published to the update server. Publishing fails if the digital certificate is not available in the certificate store of the update server or the computer that runs Updates Publisher.

    For more information about adding the certificate to the certificate store, see [Certificates and security for Updates Publisher](/sccm/sum/tools/updates-publisher-security).

    If a digital certificate is not automatically detected for the update server, choose one of the following:

    -   **Browse**: Browse is only available when the update server is installed on the server where you run the console. After you select a certificate you must choose **Create** to add that certificate to the WSUS certificate store on the update server. You must enter the **.pfx** file password for certificates that you select by this method.

    -   **Create:** Use this option to create a new certificate. This also adds the certificate to the WSUS certificate store on the update server.

    **If you create your own signing certificate**, configure the following:

    -   Enable the **Allow private key to be exported** option.

    -   Set **Key Usage** to digital signature.

    -   Set **Minimum key size** to a value equal to or greater than 2048 bit.

    Use the **Remove** option to remove a certificate from the WSUS certificate store. This option is available when the update server is local to the Updates Publisher console you use, or when you used **SSL** to connect to a remote update server.

## ConfigMgr Server
Use these options when you use Configuration Manager with Updates Publisher.

-   **Specify the Configuration Manager server:** After you enable support for Configuration Manager, specify the location of the top-tier site server from your Configuration Manager hierarchy. If that server is remote from the Updates Publisher install, specify the FQDN of the site server. Choose **Test Connection** to ensure you can connect to the site server.

-   **Configure thresholds:** Thresholds are used when you publish updates with a publication type of Automatic. The threshold values help determine when the full content for an update is published instead of only the metadata. To learn more publication types, see [Assign updates to a publication](/sccm/sum/tools/manage-updates-with-updates-publisher#assign-updates-and-bundles-to-a-publication)

    You can one or both of the following thresholds:

    -   **Requested client count threshold:** This defines how many clients must request an update before Updates Publisher can automatically publish the full set of content for that update. Until the specified number of clients request the update, only the updates metadata is published.

    -   **Package source size threshold (MB):** This prevents automatic publishing of updates that exceed the size you specify. If the updates size exceeds this value, only the metadata is published. Updates that are smaller than the specified size can have their full content published.

## Proxy Settings
Updates Publisher uses the proxy settings when you import software catalogs from the Internet or publish updates to the Internet.

-   Specify the FQDN or IP address of a proxy server. IPv4 and IPv6 are supported.

-   If the proxy server authenticates users for Internet access, you must specify the Windows name. A universal principle name (UPN) is not supported.

## Trusted Publishers
When you import an update catalog, the source of that catalog (based on its certificate), is added as a trusted publisher. Similarly, when you publish an update, the source of the updates certificate is added as a trusted publisher.

You can view certificate details for each publisher and remove a publisher from the list of trusted publishers.

Content from publishers that are not trusted can potentially harm client computers when the client scans for updates. You should accept content only from publishers that you trust.

## Advanced
Advanced options include the following:

-   **Repository location:** View and modify the location of the Database file, **scupdb.sdf**. This file is the repository for Updates Publisher.

-   **Timestamp:** When enabled, a timestamp is added to updates you sign that identifies when it was signed. An update that was signed while a certificate was valid can be used after that signing certificate expires. By default, software updates cannot be deployed after their signing certificate expires.

-   **Check for updates to subscribed catalogs:** Each time Updates Publisher starts, it can automatically check for updates to catalogs that you have subscribed to. When a catalog update is found, details are provided as **Recent Alerts** in the **Overview** window of the **Updates Workspace**.

-   **Certificate revocation:** Choose this option to enable certificate revocation checks.

-   **Local source publishing:** Updates Publisher can use a local copy of an update you are publishing before downloading that update from the Internet. The location must be a folder on the computer that runs Updates Publisher. By default, this location is **My Documents\LocalSourcePublishing.** Use this when you have previously downloaded one or more updates, or have made modifications to an update you want to deploy.

-   **Software Updates Cleanup Wizard:** Start the updates cleanup wizard. The wizard expires updates that are on the update server but not in the Updates Publisher repository. See [Expire unreferenced updates](#expire-unreferenced-software-updates) for more details.

## Updates
 Updates Publisher can automatically check for new updates each time it opens. You can also opt into receiving preview builds of Updates Publisher.

To manually check for updates, in the Updates Publisher console click on
![Properties](media/properties2.png)  
to open the **Updates Publisher Properties**, and then choose **Check for update**.

After Updates Publisher finds a new update, it displays the **Update Available** window and you can then choose to install it. If you choose to not install the update, it is offered the next time you open the console.

## Logging
Updates Publisher logs basic information about Updates Publisher to **&lt;*path*&gt;\Windows\Temp\UpdatesPublisher.log**.

Use notepad or **CMTrace** to view the log. CMTrace is the Configuration Manager log file tool and can be found in the **\SMSSetup\Tools** folder of the Configuration Manager source media.

You can change the size of the log and its level of detail.

When you enable database logging, information about the queries that are run against the Updates Publisher database are included. Use of database logging can lead to reduced performance of the Updates Publisher computer.

To view the log file, in the console click on ![Properties](media/properties2.png)
to open the **Updates Publisher Properties**, and then choose **View log file**.

## Expire unreferenced software updates
You can run the **Software Update Cleanup Wizard** to expire updates that are on your update server but not in the Updates Publisher repository. This notifies Configuration Manager which then removes those updates from any future deployments.

The act of expiring an update cannot be reversed. Only perform this task when you are sure that the software updates you select are no longer required by your organization.

### To remove expired software updates
1.  In the Updates Publisher console, click on ![Properties](media/properties2.png) to open the **Updates Publisher Properties**, and then choose **Options**.

2.  Choose **Advanced**, and then under **Software Update Clean Wizard,** choose **Start**.

3.  Select the software updates you want to expire, and then choose **Next**.

4.  After reviewing your selections, chose **Next** to accept the selections and expire those updates.

5.  After the wizard finishes, choose **Close** to complete the wizard.
