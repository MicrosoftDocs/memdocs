---
title: Prerequisites for software updates
titleSuffix: "Configuration Manager"
description: "Learn about prerequisites for software updates in System Center Configuration Manager."
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 08/20/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: fdf05118-162a-411e-b72e-386b9dc9a5e1
ms.collection: M365-identity-device-management
---

# Prerequisites for software updates in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

This article lists the prerequisites for software updates in System Center Configuration Manager. For each of these, the external dependencies and internal dependencies are listed in separate tables.  

## Software update dependencies that are external to Configuration Manager  
 The following sections list the external dependencies for software updates.  

### Internet Information Services  
 Internet Information Services (IIS) must be installed on site system servers to run the software update point, the management point, and the distribution point. For more information, see [Prerequisites for site system roles](../../core/plan-design/configs/site-and-site-system-prerequisites.md).  

### Windows Server Update Services  
 Windows Server Update Services (WSUS) is necessary for software updates synchronization and for the software updates applicability scan on clients. The WSUS server must be installed before you create the software update point role. The following versions of WSUS are supported for a software update point:  

-   WSUS 10.0.14393 (role in Windows Server 2016)
-   WSUS 10.0.17763 (role in Windows Server 2019) (Requires Configuration Manager 1810 or later)
-   WSUS 6.2 and 6.3 (role in Windows Server 2012 and Windows Server 2012 R2)

> [!NOTE]
> - Beginning with version 1702, Windows Server 2008 R2 isn't supported for the software update point role. For more information, see [Supported operating systems for site system servers](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers#bkmk_2008r2sp1).
> - When you have multiple software update points at a site, ensure that they're all running the same version of WSUS.

### WSUS Administration Console  
 The WSUS Administration Console is required on the Configuration Manager site server when the software update point is on a remote site system server and WSUS isn't already installed on the site server.  

> [!IMPORTANT]  
> - The WSUS version on the site server must be the same as the WSUS version that's running on the software update points.
> - Don't use WSUS Administration Console to configure WSUS settings. Configuration Manager connects to the instance of WSUS that is running on the software update point and configures the appropriate settings.  


### Windows Update Agent  
 The Windows Update Agent (WUA) client is required on clients so that they can connect to the WSUS server. WUA retrieves the list of software updates that must be scanned for compliance.  

 When you install Configuration Manager, the latest version of WUA is downloaded. Then, when you install the Configuration Manager client, WUA is upgraded if necessary. However, if the installation fails, you must use a different method to upgrade WUA.  

## Software update dependencies that are internal to Configuration Manager  
 The following sections list the internal dependencies for software updates in Configuration Manager.  

### Management points  
 Management points transfer information between client computers and the Configuration Manager site. The management points are required for software updates.  

### Software update points  
 You must install a software update point on the WSUS server to be able to deploy software updates in Configuration Manager. For more information, see [Install and configure a software update point](../get-started/install-a-software-update-point.md).

### Distribution points  
 Distribution points are required to store the content for software updates. For more information about how to install distribution points and manage content, see [Manage content and content infrastructure](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

### Client settings for software updates  
 By default, software updates are enabled for clients. However, there are other available settings that control how and when clients assess compliance for the software updates and control how the software updates are installed.  

 For more information, see the following articles:  

- [Client settings for software updates](../get-started/manage-settings-for-software-updates.md#BKMK_ClientSettings)   

- [Software updates client settings](../../core/clients/deploy/about-client-settings.md#software-updates)  

### Reporting services points  
 The reporting services point site system role can display reports for software updates. This role is optional but recommended. For more information about how to create a reporting services point, see [Configuring reporting](../../core/servers/manage/configuring-reporting.md).  

## <a name="BKMK_RecoverUpgrades"></a> Download of Windows 10 upgrades fails with "Error: Invalid certificate signature" or 0xc1800118

These issues described in this section only apply to WSUS running on Windows Server 2012 or Windows Server 2012 R2 machines (WSUS 6.2 and 6.3). Typically, you'll only see the issues described in this section if you installed WSUS before July 2017 and you recently enabled the **Upgrades** classification. However, it's possible to see these issues in other situations too.

### Which updates are required on WSUS 6.2 and 6.3?

 - You must install [KB 3095113](https://support.microsoft.com/kb/3095113), released in October 2015, on your software update points and site servers before you synchronize the **Upgrades** classification. 
 - To service Windows 10 version 1607 and later, you must install and configure [KB 3159706](https://support.microsoft.com/en-us/help/3159706), which was released in May 2016.

>[!IMPORTANT]
> Both KB 3095113 and KB 3159706 are included in the **Security Monthly Quality Rollup** starting in July 2017. This means you may not see KB 3095113 and KB 3159706 as installed updates since they may hve been installed with a rollup. However, if you need either of these updates, we recommend installing a **Security Monthly Quality Rollup** released after October 2017 since they contain an additional WSUS update to decrease memory utilization on WSUS's clientwebservice.

### Historical information about KB 3095113

 [KB 3095113](https://support.microsoft.com/kb/3095113) was [released as a hotfix](https://blogs.technet.microsoft.com/wsus/2015/12/03/important-update-for-wsus-4-0-kb-3095113/) in October 2015 to add support for Windows 10 upgrades to WSUS. The update enables WSUS to synchronize and distribute updates in the **Upgrades** classification for Windows 10.

If you synchronize any upgrades without having first installed [hotfix 3095113](https://support.microsoft.com/kb/3095113), you populate the WSUS database (SUSDB) with unusable data. That data must be cleared before the upgrades can be properly deployed. Windows 10 upgrades in this state can't be downloaded by using the Download Software Updates Wizard.

Errors that resemble the following appear on the Completion page of the Download Software Updates Wizard:

```
Error: Upgrade to Windows 10 Pro, version 1511, 10586
Failed to download content id {content_id}. Error: Invalid certificate signature
```

Additionally, errors resembling the following are logged in the PatchDownloader.log file:

```
Download http://wsus.ds.b1.download.windowsupdate.com/d/upgr/2015/12/10586.0.151029-1700.th2_release_...esd...
Authentication of file C:\Users\{username}\AppData\Local\Temp\2\{temporary_filename}.tmp failed, error 0x800b0004
ERROR: DownloadContentFiles() failed with hr=0x80073633
# This log is truncated for readability.
```

Historically, when these errors occurred, they would be resolved by performing a modified version of the [resolution used in "WSUS only" environments](https://blogs.technet.microsoft.com/wsus/2016/01/29/how-to-delete-upgrades-in-wsus/). The basic steps, which are informational only, are listed below: 
 
1. Disable the **Upgrades** classification from synchronizing in both WSUS and Configuration Manager.
1. Delete the **Upgrades** from the WSUS databases using a script.
1. Perform a software update point synchronization from your top-level site in Configuration Manager. This will be a full synchronization because we made a change to the classifications Configuration Manager synchronizes.
1. Install KB 3095113 if it isn't already installed. 
   - Remember KB 3095113 and KB 3159706 are included in the **Security Monthly Quality Rollup** starting in July 2017.
   - In earlier versions of Configuration Manager, you would also have to install [KB 3127032](https://support.microsoft.com/en-us/help/3127032/windows-10-upgrades-are-not-downloaded-in-system-center-configuration).
1. Select the **Upgrades** classification in the Software Update Point component properties and perform another software update point synchronization from your top-level site.

Because these steps are very similar to the resolution for issues caused by not performing the manual steps required after the installation of KB 3159706, we've combined both sets of steps into a single resolution in the section below: [To recover from synchronizing the upgrades before you install KB 3095113 or KB 3159706  ](#bkmk_fix-upgrades).

### Historical information about KB 3159706

KB 3148812 was initially released in April 2016 to enable WSUS to natively decrypt the .esd files used for upgrading Windows 10 packages. [KB 3148812 caused problems for some customers](https://blogs.technet.microsoft.com/wsus/2016/05/05/the-long-term-fix-for-kb3148812-issues/) and was replaced with [KB 3159706](https://support.microsoft.com/en-us/help/3159706). KB 3159706 needs to be installed on all your software update points and site servers before you can service Windows 10 Version 1607 and later devices. However, problems can arise if you don't realize that you need to perform the following manual steps, once per WSUS database, after installing KB3159706:

1. From an elevated command prompt run `"C:\Program Files\Update Services\Tools\wsusutil.exe" postinstall /servicing`.
1. Restart the WSUS service on all of the WSUS servers. 

If you don't realize that KB 3159706 had manual steps after installation, or you synchronized in the upgrade for Windows 10 1607 before installing KB 3159706, you would run into issues connecting to the WSUS console and deploying the upgrade respectively. When a client downloaded the upgrade file, it would get a [**0xC1800118** error code](https://support.microsoft.com/help/3194588/0xc1800118-error-when-you-push-windows-10-version-1607-by-using-wsus).

Because these steps are very similar to the resolution for issues caused by not performing the manual steps required after the installation of KB 3095113, we've combined both sets of steps into a single resolution in the section below: [To recover from synchronizing the upgrades before you install KB 3095113 or KB 3159706  ](#bkmk_fix-upgrades).
 

### <a name="bkmk_fix-upgrades"></a> To recover from synchronizing the upgrades before you install KB 3095113 or KB 3159706  

1. Disable the **Upgrades** classification in both WSUS and Configuration Manager.
   - Uncheck the **Upgrades** classification in the Software Update Point component properties on the top-level site. 
     - For more information, see [Configure classifications and products](../get-started/configure-classifications-and-products.md).
   - Uncheck the **Upgrades** classification from WSUS under **Products and Classifications** on the **Options** page.
     - If you share the WSUS database between multiple WSUS servers, you only need to do this once for each database.  
     - For more information, see [Setting up Update Synchronizations](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/manage/setting-up-update-synchronizations#setting-up-update-synchronizations-1)
1. On each WSUS server, from an elevated command prompt run: `"C:\Program Files\Update Services\Tools\wsusutil.exe" postinstall /servicing`.
   -  WSUS places the database into [single user mode](https://docs.microsoft.com/sql/relational-databases/databases/set-a-database-to-single-user-mode) before it checks to see if servicing is needed. The servicing either runs or doesn't run based on the results of the check. Then, the database is put back into multi-user mode.
   - If you share the WSUS database between multiple WSUS servers, you only need to do this once for each database.
1. 


<!--

1.  Delete software updates with the **Upgrades** classification. You can use a PowerShell script that's similar to the following sample script:  

    ```  
    $Server = Get-WSUSServer  
    $Config = $Server.GetConfiguration()  
    $Update10563 = “df4e45a3-946d-4467-b3fd-8621174bb666”  
    $UpdateGUID = New-Object Guid($Update10563)  
    $Server.DeleteUpdate($UpdateGUID)  
    ```  

    > [!IMPORTANT]  
    >  You must run the script on all software update points in your Configuration Manager hierarchy before you go to the next step.  

     To bulk delete software updates with the **Upgrades** classification, you can modify the PowerShell script to read multiple GUIDs from a text file.  

2.  Uncheck the **Upgrades** classification in the Software Update Point component properties. (For more information, see [Configure classifications and products](../get-started/configure-classifications-and-products.md).) Then start software updates synchronization. (For more information, see [Synchronize software updates](../get-started/synchronize-software-updates.md).)  

3.  Install [hotfix 3095113](https://support.microsoft.com/kb/3095113) for WSUS  on your software update points and site servers.  

4.  Select the **Upgrades** classification in the Software Update Point component properties. (For more information, see [Configure classifications and products](../get-started/configure-classifications-and-products.md).) Then start the software updates synchronization. (For more information, see [Synchronize software updates](../get-started/synchronize-software-updates.md).)  

-->

## Next steps
[Prepare for software updates management](../get-started/prepare-for-software-updates-management.md)
