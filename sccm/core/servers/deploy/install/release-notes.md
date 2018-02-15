---
title: "Release notes "
titleSuffix: "Configuration Manager"
description: "Consult these notes for urgent issues that are not yet fixed in the product or covered in a Microsoft Knowledge Base article."
ms.custom: na
ms.date: 02/14/2017
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
author: mestew
ms.author: mstewart
manager: dougeby

---
# Release notes for System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

With Configuration Manager, product release notes are limited to urgent issues. These issues are not yet fixed in the product, or detailed in a Microsoft Knowledge Base article.  

Feature-specific documentation includes information about known issues that affect core scenarios.  

> [!TIP]  
>  This topic contains release notes for the current branch of Configuration Manager. For information on the technical preview branch, see [Technical Preview for System Center Configuration Manager](../../../../core/get-started/technical-preview.md)  

For information about the new features introduced with different versions, see the following articles:
- [What's new in version 1710](/sccm/core/plan-design/changes/whats-new-in-version-1710)
- [What's new in version 1706](/sccm/core/plan-design/changes/whats-new-in-version-1706)  
- [What's new in version 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702)



## Setup and upgrade  


### When installing a Long-Term Service Branch site using version 1606, a Current Branch site is installed
<!-- Consider move to core content  -->
When you use the version 1606 baseline media from the October 2016 release to install a Long-Term Servicing Branch (LTSB) site, Setup installs a Current Branch site instead. This behavior occurs because the option to install a service connection point with the site install is not selected.

 - Although a service connection point is not required, it must be selected to install during Setup to install an LTSB site.

After Setup completes, you can uninstall the service connection point. However, you must have a service connection point in offline or online mode to submit telemetry data and to get security updates for both Current Branch and LTSB sites.

If your site installed as a Current Branch site but you wanted to install the LTSB, you can uninstall the site and then reinstall it. Alternately, you can call [Microsoft Help and Support](http://go.microsoft.com/fwlink/?LinkId=243064) for assistance.  

To confirm which branch installed, in the console at **Administration** > **Site Configuration** > **Sites**, and open **Hierarchy Settings**. The option to convert the site to a Current Branch site is only available when the site runs the LTSB.  

**Workaround:** None.   


### An update persists in Downloading state in the Updates and Servicing node of the console  
<!-- Source bug pending. Consider move to core content.  8/15 Seeking validation of issue from Dev.  -->
During the automatic download of updates by an on-line service connection point, an update can become stuck with a status of Downloading. When the download of an update is stuck, entries similar to the following appear in the indicated log files:  

DMPdownloader log:  
`ERROR: Failed to download redist for 037cd17e-4d7b-40e1-802b-14bb682364c7 with command  /RedistUrl http://go.microsoft.com/fwlink/?LinkID=724436 /LnManifestUrl http://go.microsoft.com/fwlink/?LinkID=724434 /RedistVersion 112015 /NoUI  "D:\ConfigMgr\EasySetupPayload\037cd17e-4d7b-40e1-802b-14bb682364c7\redist"`  

ConfigMgrSetup.log:  
`Error: failed to verify 'd:\ConfigMgr\EasySetupPayload\037cd17e-4d7b-40e1-802b-14bb682364c7\redist\sqlncli.msi' authenticode signature.`  
`Error: file signature check failed for 'd:\ConfigMgr\EasySetupPayload\037cd17e-4d7b-40e1-802b-14bb682364c7\redist\sqlncli.msi`  

**Workaround**: On the site server, modify the following registry key to match the following value:  

-   **Key to edit**: HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\WinTrust\Trust Providers\Software Publishing  

-   **Value for State**: Set to **146944** Decimal or **0x00023e00** Hexadecimal  

Then either restart the SMS_Executive service, or wait up to 24 hours for the next automatic download cycle.

### When using redistributable files from the CD.Latest folder, setup fails with a manifest verification error
<!-- Source bug pending    8/15 Seeking validation of issue from Dev.   -->

When you run Setup from the CD.Latest folder created for version 1606, and use the redistributable files included with that CD.Latest folder, Setup fails with the following errors in the Configuration Manager Setup log:

  `ERROR: File hash check failed for defaultcategories.dll`  
  `ERROR: Manifest verification failed. Wrong version of manifest?`

**Workaround:** Use one of the following options:
 - During Setup, choose to download the most current redistributable files from Microsoft. Use the latest redistributable files instead of the files included in the CD.Latest folder.
 - Manually delete the *cd.latest\redist\languagepack\zhh* folder, and then run Setup again.



<!-- ## Backup and recovery  -->


## Client deployment and upgrade  

### Client installation fails with error code 0x8007064c
<!--- SMS 486973  applies 1606 to 1706. Not yet fixed. -->
*The following issue applies to all active versions of Configuration Manager.*  

When you deploy the client to Windows computers, the installation fails. The ccmsetup.log file contains the following entries: 

`File 'C:\WINDOWS\ccmsetup\Silverlight.exe' returned failure exit code 1612. Fail the installation`  
`InstallFromManifest failed 0x8007064c`

**Workaround**: A corrupted, previously installed version of Silverlight causes this issue. To fix this issue, run the following tool on the affected computer:
[Fix problems that block programs from being installed or removed](https://support.microsoft.com/help/17588/fix-problems-that-block-programs-from-being-installed-or-removed).

## Operating system deployment  

### Servicing plans create many duplicate software update groups and deployments by default  
By default, the Create Servicing Plan wizard currently runs after every software updates synchronization. Each time the wizard runs, it creates a new software update group and deployment. If you have a software updates synchronization schedule that runs multiple times a day, the Create Servicing Plan wizard creates multiple software update groups and deployments each day.  

**Workaround**: After you create a serving plan, open the properties for the servicing plan, go to the **Evaluation Schedule** tab,  select **Run the rule on a schedule**, click **Customize**, and create a custom schedule. For example, you can have the servicing plan run every 60 days.  



## Software updates

### Importing an Office 365 client settings from a configuration file fails when it contains unsupported languages
<!-- 489258  Fixed in 1706  -->
*The following issue applies to version 1702 and earlier.*   

When you import the Office 365 client settings from an existing XML configuration file, and the file contains languages that are not supported by the Office 365 ProPlus client, an error occurs. For more information, see: [Deploy Office 365 apps to clients from the Office 365 Client Management dashboard](/sccm/sum/deploy-use/manage-office-365-proplus-updates#to-deploy-office-365-apps-to-clients-from-the-office-365-client-management-dashboard).

**Workaround**: Use only the [languages supported by the Office 365 ProPlus client](https://technet.microsoft.com/library/cc179219&#40;v=office.16&#41;.aspx) in the XML configuration file.  



## Mobile device management  

### Beginning with version 1710, you can no longer deploy Windows Phone 8.1 VPN profiles to Windows 10   <!-- 503274  Should be fixed by 1802, if not sooner -->
In 1710, it is no longer possible to create a VPN profile using the Windows Phone 8.1 workflow that is also applicable to Windows 10 devices. For these profiles, the Supported Platforms page is no longer shown in the creation wizard. Windows Phone 8.1 is automatically selected on the back-end. The Supported Platforms page is available in the profile properties, but it does not display the Windows 10 options.

**Workaround**: Use the Windows 10 VPN profile workflow for Windows 10 devices. If this option is not feasible for your environment, contact support. Support can help you add the Windows 10 targeting.


### Full wipe disables Windows 10 devices with less than 4 GB of memory
Performing full wipe on devices running Windows 10, version 1507, with less than 4 GB of RAM can leave the device unusable. After attempting to wipe the device, it cannot start and is unresponsive.

**Workaround**: Ensure Windows 10 devices have at least 4 GB of memory available before you perform a full wipe. To view the version number of Windows 10 devices, enter 'winver' at a command prompt. If you have already wiped the device, and it is no longer responsive, use a bootable Windows 10 USB drive to recover the device.


### When a user belongs to two or more user collections to which you deploy a terms and conditions policy, the user sees multiple sets of the same terms  
<!-- 454394    -->
If you deploy a set of terms to multiple user collections, and a user is a member of more than one of these collections, that user sees multiple copies of identical terms in the Company Portal. For example:
- A user named "SampleUser" is a member of two different user collections, "CompanyEmployeesFTE" and "CompanyEmployeesNA"
- You deploy the "CompanyTerms" terms and conditions to both CompanyEmployeesFTE and CompanyEmployeesNA
- SampleUser sees two identical sets of CompanyTerms on the terms acceptance page in the Company Portal. 

Users can only accept all or decline all of the terms. Thus there is no danger of an ambiguous acceptance state. (Such ambiguous state is where the user accepts and rejects the same terms). The Terms and Conditions acceptance report includes only one row for each set of terms per user, so there is no error in the report. The only effect is that the user sees two sets of terms on the acceptance page.  

**Workaround**: Make sure each user is only included in one collection to which the terms are deployed.  


<!-- ## Reports and monitoring    -->
<!-- ## Conditional access   -->
<!-- ## Endpoint Protection -->
