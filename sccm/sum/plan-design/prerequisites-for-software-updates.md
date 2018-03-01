---
title: Prerequisites for software updates
titleSuffix: "Configuration Manager"
description: "Learn about prerequisites for software updates in System Center Configuration Manager."
keywords:
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 02/02/2018
ms.topic: article
ms.prod: configuration-manager
ms.service:
ms.technology:
 - configmgr-sum
ms.assetid: fdf05118-162a-411e-b72e-386b9dc9a5e1

---

# Prerequisites for software updates in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

This article lists the prerequisites for software updates in System Center Configuration Manager. For each of these, the external dependencies and internal dependencies are listed in separate tables.  

## Software update dependencies that are external to Configuration Manager  
 The following sections list the external dependencies for software updates.  

### Internet Information Services (IIS)  
 Internet Information Services (IIS) must be installed on site system servers to run the software update point, the management point, and the distribution point. For more information, see [Prerequisites for site system roles](../../core/plan-design/configs/site-and-site-system-prerequisites.md).  

### Windows Server Update Services (WSUS)  
 WSUS is necessary for software updates synchronization and for the software updates applicability scan on clients. The WSUS server must be installed before you create the software update point role. The following versions of WSUS are supported for a software update point:  

-   WSUS 10.0 (role in Windows Server 2016)
-   WSUS 6.2 and 6.3 (role in Windows Server 2012 and Windows Server 2012 R2)  
-   WSUS 3.2 (role in Windows Server 2008 R2)  

 When you have multiple software update points at a site, ensure that they're all running the same version of WSUS.  

> [!WARNING]  
>  The **Upgrades** software updates classification is only supported beginning in WSUS 4.0. Before you synchronize this new classification and have the ability to evaluate Windows 10 computers in a Windows 10 servicing plan, it is critical that you install [hotfix 3095113](https://support.microsoft.com/kb/3095113) for WSUS on your software update points and site servers. This hotfix enables WSUS on a Windows Server 2012-based server or a Windows Server 2012 R2-based server to sync and distribute feature upgrades for Windows 10. For more information, see [Manage Windows as a service](../../osd/deploy-use/manage-windows-as-a-service.md).  
>   
>  If you synchronize software updates with the **Upgrades** classification before you install [hotfix 3095113](https://support.microsoft.com/kb/3095113), see [Recover from synchronizing the Upgrades category before you install KB 3095113](#BKMK_RecoverUpgrades).  

### WSUS Administration Console  
  WSUS Administration Console is required on the Configuration Manager site server when the software update point is on a remote site system server and WSUS isn't already installed on the site server.  

> [!IMPORTANT]  
>  The WSUS version on the site server must be the same as the WSUS version that's running on the software update points.  

> [!IMPORTANT]  
>  Don't use WSUS Administration Console to configure WSUS settings. Configuration Manager connects to the instance of WSUS that is running on the software update point and configures the appropriate settings.  

### Windows Update Agent (WUA)  
 The WUA client is required on clients so that they can connect to the WSUS server. WUA retrieves the list of software updates that must be scanned for compliance.  

 When you install Configuration Manager, the latest version of WUA is downloaded. Then, when you install the Configuration Manager client, WUA is upgraded if necessary. However, if the installation fails, you must use a different method to upgrade WUA.  

## Software update dependencies that are internal to Configuration Manager  
 The following sections list the internal dependencies for software updates in Configuration Manager.  

### Management points  
 Management points transfer information between client computers and the Configuration Manager site. The managment points are required for software updates.  

### Software update points  
 You must install a software update point on the WSUS server to be able to deploy software updates in Configuration Manager. For more information, see [Install and configure a software update point](../get-started/install-a-software-update-point.md).

### Distribution points  
 Distribution points are required to store the content for software updates. For more information about how to install distribution points and manage content, see [Manage content and content infrastructure](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

### Client settings for software updates  
 By default, software updates are enabled for clients. However, there are other available settings that control how and when clients assess compliance for the software updates and control how the software updates are installed.  

 For more information, see the following articles:  

-   [Client settings for software updates](../get-started/manage-settings-for-software-updates.md#BKMK_ClientSettings).   

-   [Software updates client settings](../../core/clients/deploy/about-client-settings.md#software-updates).  

### Reporting services points  
 The reporting services point site system role can display reports for software updates. This role is optional, but recommended. For more information about how to create a reporting services point, see [Configuring reporting.  

##  <a name="BKMK_RecoverUpgrades"></a> Recover from synchronizing the Upgrades category before you install KB 3095113  
 You must install [hotfix 3095113](https://support.microsoft.com/kb/3095113) for WSUS  on your software update points and site servers before you synchronize the **Upgrades** classification. If the hotfix is not installed when the **Upgrades** classification is enabled, WSUS sees the Windows 10 build 1511 feature upgrade even if it can’t properly download and deploy the associated packages. 
 
 If you synchronize any upgrades without having first installed [hotfix 3095113](https://support.microsoft.com/kb/3095113), you populate the WSUS database (SUSDB) with unusable data. That data must be cleared before upgrades can be properly deployed. Use the following procedure to recover from this issue.  

#### To recover from synchronizing the Upgrades classification before you install KB 3095113  

1.  Delete software updates with the Upgrades classification. You can use a PowerShell script that's similar to the following sample script:  

    ```  
    $Server = Get-WSUSServer  
    $Config = $Server.GetConfiguration()  
    $Update10563 = “df4e45a3-946d-4467-b3fd-8621174bb666”  
    $UpdateGUID = New-Object Guid($Update10563)  
    $Server.DeleteUpdate($UpdateGUID)  
    ```  

    > [!IMPORTANT]  
    >  You must run the script on all software update points in your Configuration Manager hierarchy before you go to the next step.  

     To bulk delete software updates with the Upgrades classification, you can modify the PowerShell script to read multiple GUIDs from a text file.  

2.  Uncheck the **Upgrades** classification in the Software Update Point component properties. (For more information, see [Configure classifications and products](../get-started/configure-classifications-and-products.md).) Then start software updates synchronization. (For more information, see [Synchronize software updates](../get-started/synchronize-software-updates.md).)  

3.  Install [hotfix 3095113](https://support.microsoft.com/kb/3095113) for WSUS  on your software update points and site servers.  

4.  Select the **Upgrades** classification in the Software Update Point component properties. (For more information, see [Configure classifications and products](../get-started/configure-classifications-and-products.md).) Then start the software updates synchronization. (For more information, see [Synchronize software updates](../get-started/synchronize-software-updates.md).)  

## Next steps
[Prepare for software updates management](../get-started/prepare-for-software-updates-management.md)
