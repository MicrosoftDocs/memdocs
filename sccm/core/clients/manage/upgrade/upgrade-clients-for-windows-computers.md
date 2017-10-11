---
title: "Upgrade clients"
titleSuffix: "Configuration Manager"
description: "Upgrade clients on Windows computers in System Center Configuration Manager."
ms.custom: na
ms.date: 05/04/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6143fd47-48ec-4bca-b53b-5b9b9f067bc3
caps.latest.revision: 11
caps.handback.revision: 0
author: arob98
ms.author: angrobe
manager: angrobe

---
# How to upgrade clients for Windows computers in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

You can upgrade the client on Windows computers using client installation methods or the automatic client upgrade features in Configuration Manager. The following client installation methods are valid ways to upgrade client software on Windows computers:  

-   Group policy installation  

-   Logon script installation  

-   Manual installation  

-   Upgrade installation  

 If you are interested in upgrading the client using a client installation methods, learn more about using those methods in [How to deploy clients to Windows computers in System Center Configuration Manager](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md).

 Beginning in version 1610, you can exclude clients from being upgraded by specifying an exclusion group. For more information, see [How to exclude upgrading clients for Windows computers](exclude-clients-windows.md).  


> [!TIP]  
>  If you are upgrading your server infrastructure from a previous version of Configuration Manager \(such as Configuration Manager 2007 or System Center 2012 Configuration Manager\), we recommend that you complete the server upgrades including installing all current branch updates, before upgrading the Configuration Manager clients.   The latest current branch update contains the latest version of the client, so it's best to do client upgrades after you have installed all of the Configuration Manager updates you want to use.

> [!NOTE]
> If you plan to reassign the site for the clients during upgrade, you can specify the new site using the SMSSITECODE client.msi property. If you use AUTO for the SMSSITECODE, you must also specify SITEREASSIGN=TRUE to allow automatic site reassignment to occur during upgrade. For more information, see [SMSSITECODE](../../deploy/about-client-installation-properties.md#smssitecode).

## Use automatic client upgrade  
 You can also configure Configuration Manager to automatically upgrade the client software to the latest Configuration Manager client version when Configuration Manager identifies that a client that is assigned to the Configuration Manager hierarchy is lower than the version used in the hierarchy. This scenario includes upgrading the client to the latest version when it attempts to assign to a Configuration Manager site.  

 A client can be automatically upgraded in the following scenarios:  

-   The client version is lower that the version being used in the hierarchy.  

-   The client on the central administration site has a language pack installed and the existing client does not.  

-   A client prerequisite in the hierarchy is a different version than the one installed on the client.  

-   One or more of the client installation files are a different version.  

> [!NOTE]  
>  You can run the report **Count of Configuration Manager clients by client versions** in the report folder **Site - Client Information** to identify the different versions of the Configuration Manager client in your hierarchy.  

 Configuration Manager creates an upgrade package by default that is automatically sent to all distribution points in the hierarchy. If you make changes to the client package on the central administration site, for example, add a client language pack, Configuration Manager automatically updates the package, and distributes it to all distribution points in the hierarchy. If automatic client upgrade is enabled, every client will install the new client language package automatically.  

> [!NOTE]  
>  Configuration Manager does not automatically send the client upgrade package to Configuration Manager cloud-based distribution points.  

 We recommend that you enable automatic client upgrades across your hierarchy. This will keep your clients updated with minimal administrative overhead.  

 Use the following procedure to configure automatic client upgrade. Automatic client upgrade must be configured at a central administration site and this configuration applies to all clients in your hierarchy.  

### To configure automatic client upgrades  

1.  In the Configuration Manager console, click **Administration**.  

2.  In the **Administration** workspace, expand **Site Configuration**, and then click **Sites**.  

3.  On the **Home** tab, in the **Sites** group, click **Hierarchy Settings**.  

4.  In the **Client Upgrade** tab of the **Hierarchy Settings Properties** dialog box, review the version and date of the production client, and make sure it's the version you want to use for upgrading Windows computers.  If it's not the client version you were expecting to see, you may need to promote the pre-production client to production. For more information, see [How to test client upgrades in a pre-production collection in System Center Configuration Manager](../../../../core/clients/manage/upgrade/test-client-upgrades.md).  

5.  Click **Upgrade all clients in the hierarchy using the production client** and click **OK** in the confirmation dialog box.  

6.  If you don't want client upgrades to apply to servers, click **Do not upgrade servers**.  

7.  Specify the number of days in which computers must upgrade the client after they receive client policy. The client will be upgraded at a random interval within this number of days. This prevents scenarios where a large number of client computers are upgraded simultaneously.

    > [!NOTE]
    > A computer must be running to upgrade the client. If a computer isn't running when it's scheduled to receive the upgrade, the upgrade does not occur. Instead, when the computer is restarted, another upgrade is scheduled for a random time within the number of days allowed. If this occurs after the number of days to upgrade has expired, the upgrade will be scheduled to occur at a random time within 24 hours after the computer has been restarted.
    >     
    > Because of this behavior, computers that are routinely shut down at the end of the workday may take a longer to upgrade than expected if the randomly scheduled upgrade time isn't within the normal working hours.

7. Beginning in version 1610, if you want to exclude clients from being upgraded, click **Exclude specified clients from upgrade** and specify the collection to exclude.

8.  If you want the client installation package to be copied to distribution points that have been enabled for prestaged content, click **Automatically distribute client installation package to distribution points that are enabled for prestaged content**.  

9. Click **OK** to save the settings and close the **Hierarchy Settings Properties** dialog box. Clients receive these settings when they next download policy.

>[!NOTE]
>Client upgrades honor any Configuration Manager maintenance windows you have configured.
