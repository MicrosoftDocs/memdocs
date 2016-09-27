---
title: "Release notes for System Center Configuration Manager"
ms.custom: na
ms.date: 08/16/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 030947fd-f5e0-4185-8513-2397fb2ec96f
caps.latest.revision: 41
caps.handback.revision: 0
author: Brenduns

---
# Release notes for System Center Configuration Manager
With System Center Configuration Manager, product release notes are limited to urgent issues that are not yet fixed in the product (available through a in-console update), or detailed in a Microsoft Knowledge Base article.  

 For known issues that affect core scenarios, this information is conveyed in the on-line product documentation in the System Center Configuration Manager documentation library.  

> [!TIP]  
>  This topic contains release notes for the current branch of System Center Configuration Manager. For the Technical Preview for System Center Configuration Manager, see [Technical Preview for System Center Configuration Manager](../../../../core/get-started/technical-preview.md)  

## Setup and upgrade  



### The  SQL Server backup model in use by Configuration Manager can change from full to simple  
 When you upgrade to System Center Configuration Manager version 1511, the SQL Server backup model in use by Configuration Manager can change from full to simple.  

-   If you use a custom SQL Server backup task with the full backup model (instead of the built-in Backup task for Configuration Manager), the upgrade can change your backup model from full to simple.  

**Workaround**: After upgrade to version 1511, review your SQL Server configuration and restore it to full if necessary.  

### When you add a service window to a new site server, service windows that were   configured for another site server are deleted  
 When you use service windows with System Center Configuration Manager version 1511, you can only configure service windows for  a single site server in a hierarchy. After configuring service windows on one server, when you then configure a service window on a second site server, the service windows on the first site server are silently deleted, with no warning or errors.  

**Workaround**: Install the hotfix from the [Microsoft Knowledge Base article 3142341](http://support.microsoft.com/kb/3142341). This issue is also resolved when you install the 1602 update for System Center Configuration Manager.  

### An update is stuck with a state of Downloading in the Updates and Servicing node of the Configuration Manager console  
During the automatic download of updates by an on-line service connection point, an update can become stuck with a stat of Downloading. When the download of an update is stuck, entries similar to the following appear in the indicated log files:  

DMPdownloader log:  

-   ERROR: Failed to download redist for 037cd17e-4d7b-40e1-802b-14bb682364c7 with command  /RedistUrl http://go.microsoft.com/fwlink/?LinkID=724436 /LnManifestUrl http://go.microsoft.com/fwlink/?LinkID=724434 /RedistVersion 112015 /NoUI  "D:\ConfigMgr\EasySetupPayload\037cd17e-4d7b-40e1-802b-14bb682364c7\redist"  

ConfigMgrSetup.log:  

-   Error: failed to verify 'd:\ConfigMgr\EasySetupPayload\037cd17e-4d7b-40e1-802b-14bb682364c7\redist\sqlncli.msi' authenticode signature.  

-   Error: file signature check failed for 'd:\ConfigMgr\EasySetupPayload\037cd17e-4d7b-40e1-802b-14bb682364c7\redist\sqlncli.msi  

**Workaround**: On the site server, modify the following registry key to match the following, and then either restart the SMS_Executive service, or wait up to 24 hours for the next automatic download cycle.  

-   **Key to edit**: HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\WinTrust\Trust Providers\Software Publishing  

-   **Value for State**:  Set to **146944** Decimal or **0x00023e00** Hexadecimal  

### Pre-release features introduced in System Center Configuration Manager 1602  

Pre-release features are included in the product for early testing in a production environment, but should not be considered production ready.  

Beginning with update 1606, you must give consent before you can use pre-release features. For more information, see [Use pre-release features from updates](../../../../core/servers/manage/install-in-console-updates.md).

System Center Configuration Manager release 1602 introduces two pre-release features:  

-   Conditional access for PCs managed by System Center Configuration Manager. For more information, see [Manage access to O365 services for PCs managed by System Center Configuration Manager](../../../../protect/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm.md).
    - After you install update 1602, the feature type displays as released even though it is pre-release.
    - If you then update from 1602 to 1606, the feature type displays as released even through it remains pre-release.
    - If you update from version 1511 directly to 1606, the feature type displays as pre-release.


-   Servicing a cluster aware collection. For more information, see [Service a server group](../../../../core/get-started/capabilities-in-technical-preview-1605.md#BKMK_ServerGroups) in [Capabilities in Technical Preview 1605 for System Center Configuration Manager](../../../../core/get-started/capabilities-in-technical-preview-1605.md).  




### Recovery options for a secondary site are not available in the console  
After recovery of a secondary site fails, the option **Recover Secondary Site** might no longer be available in the Configuration Manager console.  

This issue affects System Center Configuration Manager version 1511 and 1602, and is expected to be resolved in a future update.  

**Workaround**: Use one of the following methods to recover (reinstall) the secondary site:  

-   Use **Preinst.exe** and the **/delsite** command to remove the secondary site, and then reinstall the secondary site. For information about preinst.exe, see [Hierarchy Maintenance Tool (Preinst.exe) for System Center Configuration Manager](../../../../core/servers/manage/hierarchy-maintenance-tool-preinst.exe.md)  

-   Run the following script to start the secondary site recovery. You run this script on the database at the primary parent site of the secondary site you want to recover:  

    ```  
    declare @SiteCode NVARCHAR(3)=N'<replace with secondary site code>'   

    UPDATE Sites SET Status = 9  
                    , DetailedStatus = 3  
    FROM Sites WHERE SiteCode = @SiteCode  

    UPDATE SCP SET SCP.Value1 = 9  
                    , SCP.Value2 = N'3'  
    FROM SC_SiteDefinition_Property SCP INNER JOIN SC_SiteDefinition SC ON SC.SiteNumber = SCP.SiteNumber  
    WHERE SC.SiteCode = @SiteCode AND SCP.[Name] = N'Requested Status'  
    ```  

###  Setup fails when using redist files from the CD.Latest folder with a manifest verification error
When you run Setup from a CD.Latest folder created for version 1606 and use the redist files included with that CD.Latest folder, Setup fails with the following errors in the Configuration Manager Setup log:

  - ERROR: File hash check failed for defaultcategories.dll
  - ERROR: Manifest verification failed. Wrong version of manifest?

**Workaround:**  Use one of the following:
 - During Setup choose to download the most current redist files from Microsoft to use instead of those included in the CD.Latest folder.
 - Manually delete the *cd.latest\redist\languagepack\zhh* folder, and then run Setup again.

## Backup and recovery
### Pre\-production client is not available after a site restore
With version 1602, when you use pre-production clients and you restore the top-tier site of your hierarchy from a backup, the pre\-production client version is not available after the site is restored.  

**Workaround:**  After restoring the top-tier site of your hierarchy you must manually copy the pre\-production client files so that Configuration Manager can process them and restore them to use:
1. On the top-tier site server computer, copy the contents of the *&lt;CM_Install_Location\>\\Client* folder to the *&lt;CM_Install_Location\>\\StagingClient* folder.

2. Create an empty file named **client.acu** and copy or paste this file into the *&lt;CM_Install_Location\>\\Inboxes\\hman.box* folder on the site server. (This file can be a text file that has been renamed, so long as it no longer has the txt extension). After this file is placed in the hman.box folder, the Hierarchy Manager on the site server will start and process the client files and restore the pre\-production client files for use.

This issue is resolved in version 1606.


## Client deployment and upgrade  

### Expansion to central administration site stops automatic client upgrades  
In version 1511 only, you will not be able to run automatic client upgrades for any site that is expanded from a primary site to a central administration site. When the site is expanded, the authoritative site on the client upgrade package is not correctly set to the new central administration site, which prevents automatic client upgrades from running successfully. This issue only exists for version 1511. In version 1602 and later, this issue is fixed.  

**Workaround:** Run the following SQL script on the central administration site database. After you run the script, automatic client upgrades should begin running normally.  

  ```  
  DECLARE @RootSite AS NVARCHAR(3)  
  DECLARE @SourceServer AS NVARCHAR(255)  
  DECLARE @FullClientPkgSource AS NVARCHAR(255)  
  DECLARE @UpgradePkgSource AS NVARCHAR(255)  

  SELECT @RootSite = SiteCode, @SourceServer = SiteServer  
  FROM sites  
  WHERE ISNULL(ReportToSite, N'') = N''  

  SELECT @FullClientPkgSource = N'\\' + @SourceServer + N'\SMS_' + @RootSite + N'\Client'  
  SELECT @UpgradePkgSource = N'\\' + @SourceServer + N'\SMS_' + @RootSite + N'\ClientUpgrade'  

  UPDATE SMSPackages_G  
  SET Source = @FullClientPkgSource, SourceSite = @RootSite  
  WHERE PkgID IN  
      (SELECT FullPackageID FROM ClientDeploymentSettings)  

  UPDATE SMSPackages_G  
  SET Source = @UpgradePkgSource, SourceSite = @RootSite  
  WHERE PkgID IN  
      (SELECT UpgradePackageID FROM ClientDeploymentSettings)  

  UPDATE ProgramOffers_G  
  SET SourceSite = @RootSite  
  WHERE OfferID IN  
      (SELECT UpgradeAdvertisementID FROM ClientDeploymentSettings)  
  ```  

## Operating system deployment  

### Issue with the Windows ADK for Windows 10, version 1511  
When you run a task sequence from Software Center that uses a Windows PE v.10.0.10586 boot image from the Windows ADK 10, version 1511, when the computer restarts into Windows PE, it will fail when "Initializing hardware devices" with the error: **Windows PE initialization failed with error code 0x80220014**  

**Workaround**: Use the original Windows 10 ADK. For more information, see the following System Center Configuration Manager Team Blog: [Issue with the Windows ADK for Windows 10](http://blogs.technet.com/b/configmgrteam/archive/2015/11/20/issue-with-the-windows-adk-for-windows-10-version-1511.aspx)  

### Dynamic application installation fails during task sequence which successfully completes  
When you deploy a task sequence that uses the option **Install applications according to dynamic variable list**, and one of the applications fail to install for any reason, the task sequence reports success. This occurs regardless of how you configure the following options:  

-   **Continue on error** (on the Options tab of the Install Application step)  

-   **If an application installation fails, continue installing other applications in the list** (on the Properties tab of the Install Application step)  

You can view the smsts.log, to determine if an application failed to install.  

**Workaround**: Use the **_TSAppInstallStatus** variable as a condition on a subsequent steps in a task sequence with a condition to fail the task sequence if there was an error with one of the dynamic applications.  

### SMB might not work properly after you use a task sequence to install Windows 10  
When you use a task sequence to install a Windows 10 image, SMB might not work properly after the Configuration Manager client is installed. For example, the following task sequence steps might fail:  

-   Restore User State when used with a state migration point  

-   Connect to Network Folder  

From an F8 administrator command prompt, you can still PING the computer for example, but any SMB network traffic (such as NET USE from a command prompt) might fail with error 1231 - the network location cannot be reached.  

**Workaround**:  
Add a Run Command Line task sequence step after the Setup Windows and ConfigMgr task sequence step to stop, and then start the Workstation service as follows:    
**net stop workstation /y & net start workstation**  

### Servicing plans create a lot of duplicate software update groups and deployments by default  
By default, the Create Servicing Plan wizard currently runs after every software updates synchronization. Each time the wizard runs, it creates a new software update group and deployment. If you have a software updates synchronization schedule that runs multiple times a day, for example, the Create Servicing Plan wizard will create multiple, and likely identical, software update groups and deployments each day.  

**Workaround**:    
After you create a serving plan, open the properties for the servicing plan, go to the **Evaluation Schedule** tab,  select **Run the rule on a schedule**, click **Customize**, and create a custom schedule. For example, you can have the servicing plan run every 60 days.  

## Mobile device management  

### Cannot create an enrollment profile on a primary site  
An administrator cannot create an enrollment profile in the System Center Configuration Manager administration console that connects to a primary site. When attempting to enroll, the administrator will see an error "DEP token has not been updated. Upload a DEP token" in the enrollment profile wizard. This error occurs although a valid DEP token has been uploaded to the central administration site.  

**Workaround**: Create an enrollment profile in the System Center Configuration Manager console that connects to central administration site.  

### DEP cannot use non-alpha-numeric characters in enrollment profiles  
Enrollment profiles associated with Apple's Device Enrollment Profile (DEP) cannot use non-alpha numeric characters in the **Name**, **Description**, **Department** and **Phone number** fields for the enrollment profile when DEP is enabled. Using non-alpha-numeric characters in these fields will create an enrollment profile but the profile cannot be uploaded to Apple. No error message or warning is provided by the Apple server and profiles won't be deployed to DEP-managed devices.  

**Workaround**:
  None.

### Full wipe disables Windows 10 devices with less than 4 GB RAM

Performing full wipe on Windows 10 RTM devices (versions earlier than version 1511) with less than 4 GB of RAM can leave the device unusable. After attempting to wipe the device it cannot start and unresponsive.

**Workaround**: Ensure Windows 10 RTM PCs have at least 4 GB of RAM available before performing a full wipe on the device. To view the version number of Windows 10 devices, enter 'winver' at a command prompt. If the device has already been wiped and is no longer responsive, use a bootable Windows 10 USB drive to start and recover access to the device.

### When a user belongs to two or more user collections that a terms and conditions policy is deployed to, the user sees multiple sets of the same terms  
When an administrator deploys a set of terms to multiple user collections, and a user is a member of more than one of these collections, that user will be presented multiple copies of identical terms when opening Company Portal.  For example, if a user named "SampleUser" is a member of two different user collections, one called "CompanyEmployeesFTE" and "CompanyEmployeesNA,"" and the terms and conditions called "CompanyTerms" is deployed to both CompanyEmployeesFTE and CompanyEmployeesNA, SampleUser will see two identical sets of CompanyTerms on the terms acceptance page. Since the users can only accept all or decline all of the terms, there is no danger of being in an ambiguous acceptance state (where the user has both accepted and rejected the terms). The Terms and Conditions acceptance report will include only one row for each set of terms for each user, so there is no error in the report. The only effect is that the user will see two sets of terms on the acceptance page.  

**Workaround**: Make sure each user is only included in one collection to which the terms are deployed.  

## Reports and monitoring  

### The Health Attestation Report is empty even though health attestation data was previously collected  
When an administrative user with a security role that includes the **Read** permission to the **Health Attestation** permission group views the Health Attestation report, the report is empty and fails to display data. This is because permissions to view data in the Health Attestation report is linked to the **User Device Affinity** permission group instead of the Health Attestation permission group.  

This issue affects System Center Configuration Manager with update 1602, and is expected to be resolved in a future update.  

**Workaround**: Assign the administrative user a security group that includes the **Read** permission to the **User Device Affinities** permission group.  

### Conditional access  

#### The same User Collection is not blocked from being added to both Exempted and Targeted Collections.  
This only happens when you add the same **User Collection** to the **Exempted Collection** page **before** adding it to the **Targeted Collection** page.  If you first add a **User Collection** to the **Targeted Collections** page, and then try to add the same **User Collection** to the **Exempted Collection** page, you should see the normal blocking message.  

This issue affects System Center Configuration Manager conditional access for **Exchange On-Premises** with update 1602, and is expected to be resolved in a future update.  

**Workaround:** Add the **User Collection** to **Targeted Collections** page before selecting **User Collection** on the **Exempted Collection** page, or make sure you are not adding the same **User Collection** to both Targeted and Exempted Collections.

