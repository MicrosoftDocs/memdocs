---
title: "Release notes - Configuration Manager | Microsoft Docs"
description: "Consult these notes for urgent issues that are not yet fixed in the product or covered in a Microsoft Knowledge Base article."
ms.custom: na
ms.date: 05/31/2017
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
ms.author: brenduns
manager: angrobe

---
# Release notes for System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

With System Center Configuration Manager, product release notes are limited to urgent issues that are not yet fixed in the product (available through a in-console update), or detailed in a Microsoft Knowledge Base article.  

 For known issues that affect core scenarios, this information is conveyed in the on-line product documentation in the System Center Configuration Manager documentation library.  

> [!TIP]  
>  This topic contains release notes for the current branch of System Center Configuration Manager. For the Technical Preview for System Center Configuration Manager, see [Technical Preview for System Center Configuration Manager](../../../../core/get-started/technical-preview.md)  

## Setup and upgrade  

### After you update a Configuration Manager console using ConsoleSetup.exe from the site server folder, recent language pack changes are not available
<!--  SMS 486420  Applicability should be 1610 and 1702.  -->
After you run an in-place update to a console by using ConsoleSetup.exe from a site servers installation folder, recently installed langauge packs might not be availble. This occurs when:
- Your site runs version 1610 or 1702.
- The console is updated in-place by using ConsoleSetup.exe from the site server installation folder.

When this issue occurs, the reinstalled console does not use the latest set of language packs that were configured. No errors are returned, but language packs avaialble to the console will not have changed.  

**Workaround:** Uninstall the current console, and then reinstall the console as a new installation. You can use ConsoleSetup.exe from the site servers installation folder. During the installation, be sure to select the language pack files you want to use.


### With version 1702, the default site boundary group is configured for use for site assignment
<!--  SMS 486380   Applicability should only be to 1702. -->
With version 1702, the default site boundary groups Reference tab has a check for **Use this boundary group for site assignment**, lists the site as the **Assigned site**, and is grayed out so that the configuration cannot be edited or removed.

**Workaround:** None. You can ignore this setting. Although the group is enabled for site assignment, the default site boundary group is not used for site assignment. With 1702, this configuration ensures the default site boundary group is associated with the correct site.



### When installing a Long-Term Service Branch site using version 1606, a Current Branch site is installed
<!-- Consider move to core content  -->
When you use the version 1606 baseline media from the October 2016 release to install a Long-Term Servicing Branch (LTSB) site, Setup installs a Current Branch site instead. This occurs because the option to install a service connection point with the site install is not selected.

 - Although a service connection point is not required, it must be selected to install during Setup to install a LTSB site.

After Setup completes you can uninstall the service connection point.  However, you must have a service connection point in offline or online mode to submit telemetry data and to get security updates for both Current Branch and LTSB sites.

If your site installed as a Current Branch site but you wanted to install the LTSB, you can uninstall the site and then reinstall it. Alternately, you can call [Microsoft Help and Support](http://go.microsoft.com/fwlink/?LinkId=243064) for assistance.  

To confirm which branch installed, in the console at **Administration** > **Site Configuration** > **Sites**, and open **Hierarchy Settings**. The option to convert the site to a Current Branch site is only available when the site runs the LTSB.  

**Workaround:**  None.   



### The  SQL Server backup model in use by Configuration Manager can change from full to simple  
<!-- Confirm applicability for upgrade to later baselines. 1511 is out of support. 1606 is minmum supported baseline  -->

 When you upgrade to System Center Configuration Manager version 1511, the SQL Server backup model in use by Configuration Manager can change from full to simple.  

-   If you use a custom SQL Server backup task with the full backup model (instead of the built-in Backup task for Configuration Manager), the upgrade can change your backup model from full to simple.  

**Workaround**: After upgrade to version 1511, review your SQL Server configuration and restore it to full if necessary.  



### An update is stuck with a state of Downloading in the Updates and Servicing node of the Configuration Manager console  
<!-- Source bug pending. Consider move to core content.  -->
During the automatic download of updates by an on-line service connection point, an update can become stuck with a stat of Downloading. When the download of an update is stuck, entries similar to the following appear in the indicated log files:  

DMPdownloader log:  

-   ERROR: Failed to download redist for 037cd17e-4d7b-40e1-802b-14bb682364c7 with command  /RedistUrl http://go.microsoft.com/fwlink/?LinkID=724436 /LnManifestUrl http://go.microsoft.com/fwlink/?LinkID=724434 /RedistVersion 112015 /NoUI  "D:\ConfigMgr\EasySetupPayload\037cd17e-4d7b-40e1-802b-14bb682364c7\redist"  

ConfigMgrSetup.log:  

-   Error: failed to verify 'd:\ConfigMgr\EasySetupPayload\037cd17e-4d7b-40e1-802b-14bb682364c7\redist\sqlncli.msi' authenticode signature.  

-   Error: file signature check failed for 'd:\ConfigMgr\EasySetupPayload\037cd17e-4d7b-40e1-802b-14bb682364c7\redist\sqlncli.msi  

**Workaround**: On the site server, modify the following registry key to match the following, and then either restart the SMS_Executive service, or wait up to 24 hours for the next automatic download cycle.  

-   **Key to edit**: HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\WinTrust\Trust Providers\Software Publishing  

-   **Value for State**:  Set to **146944** Decimal or **0x00023e00** Hexadecimal  


###  Setup fails when using redist files from the CD.Latest folder with a manifest verification error
<!-- Source bug pending  -->

When you run Setup from a CD.Latest folder created for version 1606 and use the redist files included with that CD.Latest folder, Setup fails with the following errors in the Configuration Manager Setup log:

  - ERROR: File hash check failed for defaultcategories.dll
  - ERROR: Manifest verification failed. Wrong version of manifest?

**Workaround:**  Use one of the following:
 - During Setup choose to download the most current redist files from Microsoft to use instead of those included in the CD.Latest folder.
 - Manually delete the *cd.latest\redist\languagepack\zhh* folder, and then run Setup again.

### Service connection tool throws an exception when SQL server is remote, or when Shared Memory is disabled
Beginning with version 1606, the service connection tool generates an exception when one of the following is true:  
 -	Your site database is remote from the computer that hosts the service connection point and uses a non-standard port (a port other than 1433)
 - 	Your site database is on the same server as the service connection point but SQL protocol **Shared Memory** is disabled

The exception is similar to the following:
 - *Unhandled Exception: System.Data.SqlClient.SqlException: A network-related or instance-specific error occurred while establishing a connection to SQL Server. The server was not found or was not accessible. Verify that the instance name is correct and that SQL Server is configured to allow remote connections. (provider: Named Pipes Provider, error: 40 - Could not open a connection to SQL Server) --*

**Workaround**: During use of the tool you must modify the registry of the server that hosts the service connection point to include information about the SQL Server port:

   1.	Before using the tool, edit the following registry key and add the number of the port that is in use to the name of the SQL Server:
    - Key:   HKLM\Microsoft\SMS\COMPONENTS\SMS_DMP_UPLOADER\
	  - Value: &lt;SQL Server Name>
    - Add: **,&lt;PORT>**

    For example, to add port *15001* to a server named *testserver.test.net*, the resultant key would be: ***HKLM\Software\Microsoft\SMS\COMPONENTS\SMS_DMP_UPLOADER\testserver.test.net,15001***

   2.	After adding the port to the registry, the tool should function normally.  

   3.	After your use of the tool is complete, for both the **-connect** and **-import** steps, change the registry key back to the original value.  




<!-- No current Backup and Recovery relenotes
## Backup and recovery
-->



## Client deployment and upgrade  

### Client installation fails with error code 0x8007064c
<!--- SMS 486973 -->

When you deploy the client to Windows computers, the installation fails. The ccmsetup.log file contains an entry "File 'C:\WINDOWS\ccmsetup\Silverlight.exe' returned failure exit code 1612. Fail the installation" followed by "InstallFromManifest failed 0x8007064c".

**Workaround**
This is caused by a corrupted, previously installed version of Silverlight. You can try running the following tool on the affected computer to fix this:
[https://support.microsoft.com/help/17588/fix-problems-that-block-programs-from-being-installed-or-removed](https://support.microsoft.com/help/17588/fix-problems-that-block-programs-from-being-installed-or-removed)

## Operating system deployment  

### If the boot image contains drivers, the image fails to reload the current Windows PE version from the Windows Assessment and Deployment Kit (ADK)
<!-- 495087 -->
You can use the Update Distribution Point Wizard to update distribution points with a boot image stored in with the latest version of Windows PE from the installation directory of the Windows Assessment and Deployment Kit (ADK). To update, open the Update Distribution Point Wizard and select **Reload this boot image with the current PE version from the Windows ADK**.

However, if your boot image contains drivers, the update fails. Instead, the wizard reloads the image from the ADK, displays an exception dialog box that the user can dismiss, and then shows a success screen. However, the latest Configuration Manager client components will not be added to the boot image. The boot image will not be updated on the distribution point

**Workaround**: Run the Update Distribution Point Wizard twice.

1. Run the wizard with **Reload this boot image with the current Windows PE version from the Windows ADK** selected. This will get the latest version of Windows PE.
2. Run the wizard again with **Reload this boot image with the current Windows PE version from the Windows ADK** not selected. This wil get the latest client binaries and update the boom image on the distribution point.

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

### When a high-risk deployment dialog is visible to a user, subsequent high-risk dialogs with a sooner deadline are not displayed
After you create and deploy a high-risk task deployment to users, a high-risk dialog box is displayed to the user. If the user does not close the dialog box, you create and deploy another high-risk deployment with a sooner deadline than the first, the user will not receive an updated dialog box until they have closed the original dialog box. The deployments will still run at the configured deadlines.

**Workaround**:  
The user must close the dialog box for the first high-risk deployment to see the dialog box for the next high-risk deployment.

## Software updates

### Importing an Office 365 client settings from a configuration file fails when it contains unsupported languages
When you import the Office 365 client settings from an existing XML configuration file, and the file contains languages that are not supported by the Office 365 ProPlus client, an error will occur. For details, see [deploy Office 365 apps to clients from the Office 365 Client Management dashboard](/sccm/sum/deploy-use/manage-office-365-proplus-updates#to-deploy-office-365-apps-to-clients-from-the-office-365-client-management-dashboard).

**Workaround**:    
Use only the [languages supported by the Office 365 ProPlus client](https://technet.microsoft.com/library/cc179219&#40;v=office.16&#41;.aspx) in the XML configuration file.  

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

### Android for Work email profiles that use certificate authentication are not applied to devices
<!--  487657 -->
When an Android for Work email profile is created, there are two options for authentication. One is username and password, and the other is certificates. At this time, the certificates option is not working. If the profile is created with the authentication method set to **certificates**, the profile is not applied to the device and the user will be prompted to enter email account details manually.

**WORKAROUND**: None. Admins must either use the **username and password** option, or wait until this issue has been resolved.

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

## Endpoint Protection
<!--  Product Studio bug 485370 added 04 19 2017 -->
### Antimalware policy fails to apply on Windows Server 2016 Core
Antimalware policy fails to apply on Windows Server 2016 Core.  The error code is 0x80070002.  There is a missing dependency for ConfigSecurityPolicy.exe.

**Workaround:**  This issue is resolved by [Knowledge Base article 4019472](https://support.microsoft.com/help/4019472/windows-10-update-kb4019472) distributed May 9, 2017.

<!-- Product Studio bug 462286 added  05 25 2017 and valid until July 2017 GA release -->
### Windows Defender Advanced Threat Protection policies fail on older client agents

Windows Defender Advanced Threat Protection policies created from a Configuration Manager version 1610 or later site server fail to apply to Configuration Manager version 1606 and earlier clients.  The clients are not on-boarded and the policy evaluation reports an error. The **Deployment state** in Windows Defender Advanced Threat Protection configuration shows **Error**.

**WORKAROUND**: Upgrade the Configuration Manager client to version 1610 or later.
