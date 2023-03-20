---
title: Prerequisites for software updates
titleSuffix: Configuration Manager
description: Learn about prerequisites for software updates in Configuration Manager.
author: BalaDelli
ms.author: baladell
manager: apoorvseth
ms.date: 03/20/2023
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.localizationpriority: medium
ms.reviewer: mstewart,aaroncz 
ms.collection: tier3
---

# Prerequisites for software updates in Configuration Manager

*Applies to: Configuration Manager (current branch)*

This article lists the prerequisites for software updates in Configuration Manager. For each of the prerequisites, the external dependencies and internal dependencies are listed in separate tables.  

## Software update dependencies that are external to Configuration Manager  
 The following sections list the external dependencies for software updates.  

### Internet Information Services  
 Internet Information Services (IIS) must be installed on the site system servers to run the software update point, the management point, and the distribution point. For more information, see [Prerequisites for site system roles](../../core/plan-design/configs/site-and-site-system-prerequisites.md).  

### Windows Server Update Services  
 Windows Server Update Services (WSUS) is needed for software updates synchronization and for the software updates applicability scan on clients. The WSUS server must be installed before you create the software update point role. The following versions of WSUS are supported for a software update point:  

- WSUS 10.0.14393 (role in Windows Server 2016) (2023-02 Cumulative Update, or a later cumulative update)
- WSUS 10.0.17763 (role in Windows Server 2019) (Requires Configuration Manager 1810 or later) (2023-02 Cumulative Update, or a later cumulative update)
- WSUS 10.0.20348 (role in Windows Server 2022) (2023-02 Cumulative Update, or a later cumulative update)
- WSUS 6.2 and 6.3 (role in Windows Server 2012 and Windows Server 2012 R2) (2023-03 Cumulative Update, or a later cumulative update)
  - [KB 3095113 and KB 3159706 (or an equivalent update)](#BKMK_wsus2012) are needed for WSUS 6.2 and 6.3 if you deploy Windows upgrades.

> [!NOTE]
> - Starting March 28, 2023, on-premises Windows 11, version 22H2 devices will receive quality updates via the Unified Update Platform (UUP), 2023-02 cumulative update is a must If you're unable to install these updates, you can [manually add the required MIME types for UUP](windows-server/administration/windows-server-update-services/plan/plan-your-wsus-deployment#manually-add-the-required-mime-types-for-uup) to the WSUS server.
> - When you have multiple software update points at a site, ensure that they're all running the same version of WSUS.

### WSUS Administration Console  
The WSUS Administration Console is required on the Configuration Manager site server when the software update point is on a remote site system server and WSUS isn't already installed on the site server.  

> [!IMPORTANT]  
> - The WSUS version on the site server must be the same as the WSUS version that's running on the software update points.
> - Don't use WSUS Administration Console to configure WSUS settings. Configuration Manager connects to the instance of WSUS that is running on the software update point and configures the appropriate settings.  


### Windows Update Agent  
 The Windows Update Agent (WUA) client is required on clients so that they can connect to the WSUS server. WUA retrieves the list of software updates that must be scanned for compliance.  

 When you install Configuration Manager, the latest version of WUA is downloaded. Then, when you install the Configuration Manager client, WUA is upgraded if necessary. If the installation fails, you must use a different method to upgrade WUA.  

## Software update dependencies that are internal to Configuration Manager  
 The following sections list the internal dependencies for software updates in Configuration Manager.  

### Management points  
 Management points transfer information between client computers and the Configuration Manager site. The management points are required for software updates.  

### Software update points  
 You must install a software update point on the WSUS server to deploy software updates in Configuration Manager. For more information, see [Install and configure a software update point](../get-started/install-a-software-update-point.md).

### Distribution points  
 Distribution points are required to store the content for software updates. For more information about how to install distribution points and manage content, see [Manage content and content infrastructure](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

### Client settings for software updates  
Software updates are enabled for clients by default. There are other available settings that control how and when clients assess compliance for the software updates and control how the software updates are installed.  

 For more information, see the following articles:  

- [Client settings for software updates](../get-started/manage-settings-for-software-updates.md#BKMK_ClientSettings)   

- [Software updates client settings](../../core/clients/deploy/about-client-settings.md#software-updates)

> [!Important]
> Beginning with the September 2020 cumulative update, HTTP-based WSUS servers will be secure by default. A client scanning for updates against an HTTP-based WSUS will no longer be allowed to leverage a user proxy by default. If you still require a user proxy despite the security trade-offs, a new [software updates client setting](../../core/clients/deploy/about-client-settings.md#software-updates) is available to allow these connections. For more information about the changes for scanning WSUS, see [September 2020 changes to improve security for Windows devices scanning WSUS](https://go.microsoft.com/fwlink/?linkid=2144403). To ensure that the best security protocols are in place, we highly recommend that you use the TLS/SSL protocol to help [secure your software update infrastructure](../get-started/software-update-point-ssl.md).

### Reporting services points  
 The reporting services point site system role can display reports for software updates. This role is optional but recommended. For more information about how to create a reporting services point, see [Configuring reporting](../../core/servers/manage/configuring-reporting.md).  

## <a name="BKMK_wsus2012"></a> Which updates are required on WSUS 6.2 and 6.3?

Two updates are required for syncing **Upgrades** classification in WSUS 6.2 and 6.3. Occasionally, you might see an error downloading or deploying upgrades if they synchronized before KB3095113 and KB3159706 were installed. Information about possible issues is in the next section.  

- You must install [KB 3095113](https://support.microsoft.com/kb/3095113), released in October 2015, on your software update points and site servers before you synchronize the **Upgrades** classification.
  - This update enables the **Upgrades** classification.
- To service Windows 10 or later clients, you must install and configure [KB 3159706](https://support.microsoft.com/help/3159706). KB 3159706 was released in May 2016.
  - This update enables WSUS to natively decrypt the files used for upgrading Windows 10 version 1607 and later.

>[!IMPORTANT]
> Both KB 3095113 and KB 3159706 are included in the **Security Monthly Quality Rollup** starting in July 2017. This means you may not see KB 3095113 and KB 3159706 as installed updates since they may have been installed with a rollup. However, if you need either of these updates, we recommend installing a **Security Monthly Quality Rollup** released after October 2017 since they contain an additional WSUS update to decrease memory utilization on WSUS's clientwebservice.

## <a name="BKMK_RecoverUpgrades"></a> Download of Windows upgrades fails with "Error: Invalid certificate signature" or 0xc1800118

The updates and issue described in this section only apply to WSUS running on Windows Server 2012 or Windows Server 2012 R2 machines (WSUS 6.2 and 6.3). Typically, you'll only see the issues described in this section if you installed WSUS before July 2017 and you've recently enabled the **Upgrades** classification. However, it's possible to see these issues in other situations too.

### Historical information about KB 3095113

 [KB 3095113](https://support.microsoft.com/kb/3095113) was [released as a hotfix](/archive/blogs/wsus/important-update-for-wsus-4-0-kb-3095113) in October 2015 to add support for Windows 10 upgrades to WSUS. The update enables WSUS to synchronize and distribute updates in the **Upgrades** classification for Windows.

If you synchronize any upgrades without having first installed [KB 3095113](https://support.microsoft.com/kb/3095113), you populate the WSUS database (SUSDB) with unusable data. That data must be cleared before the upgrades can be properly deployed. Windows upgrades in this state can't be downloaded by using the Download Software Updates Wizard.

Errors that resemble the following appear on the Completion page of the Download Software Updates Wizard:

``` Output
Error: Upgrade to Windows 10 Pro, version 1511, 10586
Failed to download content id {content_id}. Error: Invalid certificate signature
```

Additionally, errors resembling the following are logged in the PatchDownloader.log file:

``` Log
Download http://wsus.ds.b1.download.windowsupdate.com/d/upgr/2015/12/10586.0.151029-1700.th2_release_...esd...
Authentication of file C:\Users\{username}\AppData\Local\Temp\2\{temporary_filename}.tmp failed, error 0x800b0004
ERROR: DownloadContentFiles() failed with hr=0x80073633
# This log is truncated for readability.
```

Historically, when these errors occurred, they would be resolved by doing a modified version of the [resolution steps for WSUS](/archive/blogs/wsus/how-to-delete-upgrades-in-wsus). Because these steps are similar to the resolution for not doing the manual steps required after KB 3159706 installation, we've combined both sets of steps into a single resolution in the section below:

- [To recover from synchronizing the upgrades before you install KB 3095113 or KB 3159706](#bkmk_fix-upgrades).

### Historical information about KB 3159706

KB 3148812 was initially released in April 2016 to enable WSUS to natively decrypt the .esd files used for upgrading Windows 10 packages. [KB 3148812 caused problems for some customers](/archive/blogs/wsus/the-long-term-fix-for-kb3148812-issues) and was replaced with [KB 3159706](https://support.microsoft.com/help/3159706). KB 3159706 needs to be installed on all your software update points and site servers before you can service Windows 10 Version 1607 and later devices. However, problems can arise if you don't realize the KB requires the following manual steps after installation:

1. From an elevated command prompt run `"C:\Program Files\Update Services\Tools\wsusutil.exe" postinstall /servicing`.
1. Restart the WSUS service on all of the WSUS servers.

If you don't realize that KB 3159706 had manual steps after installation, or you synchronized in the upgrades before installing KB 3159706, you would run into issues connecting to the WSUS console and deploying the upgrade respectively. When a client downloaded the upgrade file, it would get a **0xC1800118** error code.

Because the resolution steps are similar to the resolution for synchronizing upgrades before KB 3095113 installation, we've combined both sets of steps into a single resolution in the next section.
 

### <a name="bkmk_fix-upgrades"></a> To recover from synchronizing the upgrades before you install KB 3095113 or KB 3159706

Follow the steps below to resolve both the 0xc1800118 error and "Error: Invalid certificate signature":

1. Disable the **Upgrades** classification in both WSUS and Configuration Manager. You don't want a synchronization to occur until you're directed to by these instructions.  
   - Uncheck the **Upgrades** classification in the software update point component properties on the top-level site.
     - For more information, see [Configure classifications and products](../get-started/configure-classifications-and-products.md).
   - Uncheck the **Upgrades** classification from WSUS under **Products and Classifications** on the [**Options** page](/windows-server/administration/windows-server-update-services/manage/setting-up-update-synchronizations), or use the PowerShell ISE running as administrator.
      ```PowerShell
      Get-WsusClassification | Where-Object -FilterScript {$_.Classification.Title -Eq "Upgrades"} | Set-WsusClassification -Disable
      ```  
     - If you share the WSUS database between multiple WSUS servers, you only need to uncheck **Upgrades** once for each database.  
1. On each WSUS server, from an elevated command prompt run: `"C:\Program Files\Update Services\Tools\wsusutil.exe" postinstall /servicing`. Then, restart the WSUS service on all of the WSUS servers.
   -  WSUS places the database into [single user mode](/sql/relational-databases/databases/set-a-database-to-single-user-mode) before it checks to see if servicing is needed. The servicing either runs or doesn't run based on the results of the check. Then, the database is put back into multi-user mode. 
   - If you share the WSUS database between multiple WSUS servers, you only need to do this servicing once for each database.
1. Delete all of the Windows 10 upgrades from each WSUS database using the PowerShell ISE running as administrator.
   ```PowerShell
   [reflection.assembly]::LoadWithPartialName("Microsoft.UpdateServices.Administration")
   $wsus = [Microsoft.UpdateServices.Administration.AdminProxy]::GetUpdateServer();
   $wsus.GetUpdates() | Where {$_.UpdateClassificationTitle -eq 'Upgrades' -and $_.Title -match 'Windows 10'} `
   | ForEach-Object {$wsus.DeleteUpdate($_.Id.UpdateId.ToString()); Write-Host $_.Title removed}
   ```
1. Delete files from the tbFile table from each of the WSUS databases used by your software update points. On the WSUS database, run the following commands from SQL Server Management Studio:
   ```SQL
   declare @NotNeededFiles table (FileDigest binary(20) UNIQUE)
   insert into @NotNeededFiles(FileDigest) (select FileDigest from tbFile where FileName like '%.esd%'  except select FileDigest from tbFileForRevision)
   delete from tbFileOnServer where FileDigest in (select FileDigest from @NotNeededFiles)
   delete from tbFile where FileDigest in (select FileDigest from @NotNeededFiles)
   ```
1. Start the software updates synchronization on your top-level site in Configuration Manager and wait for it to complete. A full synchronization occurs because we made a change to the classifications Configuration Manager when we removed **Upgrades**. (For more information, see [Synchronize software updates](../get-started/synchronize-software-updates.md).
1. Select the **Upgrades** classification in the software update point component properties. Then, start another software updates synchronization to bring the **Upgrades** back into WSUS and Configuration Manager. You don't have to enable the **Upgrades** classification in WSUS since Configuration Manager will do it for you.
1. If your clients received the **0xC1800118** error code when downloading an upgrade, you'll need to delete the data store used by the Windows Update Agent. You may also have to delete the hidden ~BT folder on the device. The next time the client scans, it will be a full scan against the WSUS server rather than a delta. You can use a PowerShell script that's similar to the following sample script:  
   ```PowerShell
   stop-service wuauserv
   remove-item -path c:\windows\softwaredistribution\datastore -recurse -force
   # If the device has a hidden ~BT folder on the c drive, delete it too by uncommenting the next line.
   # remove-item -path c:\~BT -recurse -force
   start-service wuauserv
   ```

## Next steps
[Prepare for software updates management](../get-started/prepare-for-software-updates-management.md)
