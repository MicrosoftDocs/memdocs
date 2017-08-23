---
title: "Release notes - Configuration Manager | Microsoft Docs"
description: "Consult these notes for urgent issues that are not yet fixed in the product or covered in a Microsoft Knowledge Base article."
ms.custom: na
ms.date: 08/23/2017
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

Information about known issues that affect core scenarios is conveyed in the on-line product documentation, in the System Center Configuration Manager documentation library.  

> [!TIP]  
>  This topic contains release notes for the current branch of System Center Configuration Manager. For the Technical Preview for System Center Configuration Manager, see [Technical Preview for System Center Configuration Manager](../../../../core/get-started/technical-preview.md)  

For information about the new features introduced with different versions, see the following:
- [What's new in version 1706](/sccm/core/plan-design/changes/whats-new-in-version-1706.md)  
- [What's new in version 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702.md)
- [What's new in version 1610](/sccm/core/plan-design/changes/whats-new-in-version-1610.md)



## Setup and upgrade  

### After you update a Configuration Manager console using ConsoleSetup.exe from the site server folder, recent language pack changes are not available
<!--  SMS 486420  Applicability should be 1610 and 1702.  -->
*The following applies to version 1610 and 1702.*   
After you run an in-place update to a console by using ConsoleSetup.exe from a site servers installation folder, recently installed language packs might not be available. This occurs when:
- Your site runs version 1610 or 1702.
- The console is updated in-place by using ConsoleSetup.exe from the site server installation folder.

When this issue occurs, the reinstalled console does not use the latest set of language packs that were configured. No errors are returned, but language packs available to the console will not have changed.  

**Workaround:** Uninstall the current console, and then reinstall the console as a new installation. You can use ConsoleSetup.exe from the site servers installation folder. During the installation, be sure to select the language pack files you want to use.


### With version 1702, the default site boundary group is configured for use for site assignment
<!--  SMS 486380   Applicability should only be to 1702. -->
*The following applies to version 1702.*  
The default site boundary groups Reference tab has a check for **Use this boundary group for site assignment**, lists the site as the **Assigned site**, and is grayed out so that the configuration cannot be edited or removed.

**Workaround:** None. You can ignore this setting. Although the group is enabled for site assignment, the default site boundary group is not used for site assignment. With 1702, this configuration ensures the default site boundary group is associated with the correct site.



### When installing a Long-Term Service Branch site using version 1606, a Current Branch site is installed
<!-- Consider move to core content  -->
When you use the version 1606 baseline media from the October 2016 release to install a Long-Term Servicing Branch (LTSB) site, Setup installs a Current Branch site instead. This occurs because the option to install a service connection point with the site install is not selected.

 - Although a service connection point is not required, it must be selected to install during Setup to install a LTSB site.

After Setup completes you can uninstall the service connection point.  However, you must have a service connection point in offline or online mode to submit telemetry data and to get security updates for both Current Branch and LTSB sites.

If your site installed as a Current Branch site but you wanted to install the LTSB, you can uninstall the site and then reinstall it. Alternately, you can call [Microsoft Help and Support](http://go.microsoft.com/fwlink/?LinkId=243064) for assistance.  

To confirm which branch installed, in the console at **Administration** > **Site Configuration** > **Sites**, and open **Hierarchy Settings**. The option to convert the site to a Current Branch site is only available when the site runs the LTSB.  

**Workaround:**  None.   


### An update is stuck with a state of Downloading in the Updates and Servicing node of the Configuration Manager console  
<!-- Source bug pending. Consider move to core content.  8/15 Seeking validation of issue from Dev.  -->
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
<!-- Source bug pending    8/15 Seeking validation of issue from Dev.   -->

When you run Setup from a CD.Latest folder created for version 1606 and use the redist files included with that CD.Latest folder, Setup fails with the following errors in the Configuration Manager Setup log:

  - ERROR: File hash check failed for defaultcategories.dll
  - ERROR: Manifest verification failed. Wrong version of manifest?

**Workaround:**  Use one of the following:
 - During Setup choose to download the most current redist files from Microsoft to use instead of those included in the CD.Latest folder.
 - Manually delete the *cd.latest\redist\languagepack\zhh* folder, and then run Setup again.


### Service connection tool throws an exception when SQL server is remote, or when Shared Memory is disabled
<!-- 479223   Fixed in 1702 and later   -->
*The following applies to version 1610 and earlier.*  
The service connection tool generates an exception when one of the following is true:  
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


<!-- ## Backup and recovery  -->


## Client deployment and upgrade  

### Client installation fails with error code 0x8007064c
<!--- SMS 486973  applies 1606 to 1706. Not yet fixed. -->
*The following applies to all active versions of Configuration Manager.*   
With all active versions of When you deploy the client to Windows computers, the installation fails. The ccmsetup.log file contains an entry "File 'C:\WINDOWS\ccmsetup\Silverlight.exe' returned failure exit code 1612. Fail the installation" followed by "InstallFromManifest failed 0x8007064c".

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

### Servicing plans create a lot of duplicate software update groups and deployments by default  
By default, the Create Servicing Plan wizard currently runs after every software updates synchronization. Each time the wizard runs, it creates a new software update group and deployment. If you have a software updates synchronization schedule that runs multiple times a day, for example, the Create Servicing Plan wizard will create multiple, and likely identical, software update groups and deployments each day.  

**Workaround**:    
After you create a serving plan, open the properties for the servicing plan, go to the **Evaluation Schedule** tab,  select **Run the rule on a schedule**, click **Customize**, and create a custom schedule. For example, you can have the servicing plan run every 60 days.  


### When a high-risk deployment dialog is visible to a user, subsequent high-risk dialogs with a sooner deadline are not displayed
<!-- Fixed in 1702 and later -->
*The following applies to version 1610 and earlier.*   
After you create and deploy a high-risk task deployment to users, a high-risk dialog box is displayed to the user. If the user does not close the dialog box, you create and deploy another high-risk deployment with a sooner deadline than the first, the user will not receive an updated dialog box until they have closed the original dialog box. The deployments will still run at the configured deadlines.

**Workaround**:  
The user must close the dialog box for the first high-risk deployment to see the dialog box for the next high-risk deployment.



## Software updates

### Importing an Office 365 client settings from a configuration file fails when it contains unsupported languages
<!-- 489258  Fixed in 1706  -->
*The following applies to version 1702 and earlier.*   
When you import the Office 365 client settings from an existing XML configuration file, and the file contains languages that are not supported by the Office 365 ProPlus client, an error will occur. For details, see [deploy Office 365 apps to clients from the Office 365 Client Management dashboard](/sccm/sum/deploy-use/manage-office-365-proplus-updates#to-deploy-office-365-apps-to-clients-from-the-office-365-client-management-dashboard).

**Workaround**:    
Use only the [languages supported by the Office 365 ProPlus client](https://technet.microsoft.com/library/cc179219&#40;v=office.16&#41;.aspx) in the XML configuration file.  



## Mobile device management  

### Full wipe disables Windows 10 devices with less than 4 GB RAM
Performing full wipe on Windows 10 RTM devices (versions earlier than version 1511) with less than 4 GB of RAM can leave the device unusable. After attempting to wipe the device it cannot start and unresponsive.

**Workaround**: Ensure Windows 10 RTM PCs have at least 4 GB of RAM available before performing a full wipe on the device. To view the version number of Windows 10 devices, enter 'winver' at a command prompt. If the device has already been wiped and is no longer responsive, use a bootable Windows 10 USB drive to start and recover access to the device.


### When a user belongs to two or more user collections that a terms and conditions policy is deployed to, the user sees multiple sets of the same terms  
<!-- 454394    -->
When an administrator deploys a set of terms to multiple user collections, and a user is a member of more than one of these collections, that user will be presented multiple copies of identical terms when opening Company Portal.  For example, if a user named "SampleUser" is a member of two different user collections, one called "CompanyEmployeesFTE" and "CompanyEmployeesNA,"" and the terms and conditions called "CompanyTerms" is deployed to both CompanyEmployeesFTE and CompanyEmployeesNA, SampleUser will see two identical sets of CompanyTerms on the terms acceptance page. Since the users can only accept all or decline all of the terms, there is no danger of being in an ambiguous acceptance state (where the user has both accepted and rejected the terms). The Terms and Conditions acceptance report will include only one row for each set of terms for each user, so there is no error in the report. The only effect is that the user will see two sets of terms on the acceptance page.  

**Workaround**: Make sure each user is only included in one collection to which the terms are deployed.  


### Android for Work email profiles that use certificate authentication are not applied to devices
<!--  487657      -->
When an Android for Work email profile is created, there are two options for authentication. One is username and password, and the other is certificates. At this time, the certificates option is not working. If the profile is created with the authentication method set to **certificates**, the profile is not applied to the device and the user will be prompted to enter email account details manually.

**WORKAROUND**: None. Admins must either use the **username and password** option, or wait until this issue has been resolved.



<!-- ## Reports and monitoring    -->
<!-- ## Conditional access   -->


## Endpoint Protection

### Antimalware policy fails to apply on Windows Server 2016 Core
<!--  Product Studio bug 485370 added 04 19 2017   Fixed in 1702 -->
*The following applies to version 1610 and earlier.*  
Antimalware policy fails to apply on Windows Server 2016 Core.  The error code is 0x80070002.  There is a missing dependency for ConfigSecurityPolicy.exe.

**Workaround:**  This issue is resolved by [Knowledge Base article 4019472](https://support.microsoft.com/help/4019472/windows-10-update-kb4019472) distributed May 9, 2017.


### Windows Defender Advanced Threat Protection policies fail on older client agents
<!-- Product Studio bug 462286 added  05 25 2017 and valid until July 2017 GA release      Fixed in 1610 -->
Windows Defender Advanced Threat Protection policies created from a Configuration Manager version 1610 or later site server fail to apply to Configuration Manager version 1606 and earlier clients.  The clients are not on-boarded and the policy evaluation reports an error. The **Deployment state** in Windows Defender Advanced Threat Protection configuration shows **Error**.

**WORKAROUND**: Upgrade the Configuration Manager client to version 1610 or later.
