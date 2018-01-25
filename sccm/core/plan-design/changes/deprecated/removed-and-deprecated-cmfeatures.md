---
title: "Deprecated for Configuration Manager features"
titleSuffix: "Configuration Manager"
description: "Learn about the features that System Center Configuration Manager no longer supports."
ms.custom: na
ms.date: 01/25/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 287a6324-ae65-4d38-b2ef-198d47c91231
caps.latest.revision: 15
caps.handback.revision: 0
author: mestew
ms.author: mstewart
manager: angrobe

---

# Removed and deprecated features for System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

This article describes features that are removed from support for System Center Configuration Manager, or will be removed in a future update (deprecated). This article provides early notice about future changes that might affect your use of Configuration Manager.  

This information is subject to change with future releases, and might not include each deprecated Configuration Manager feature.

## Deprecated features  

|**Feature**|**Deprecation first announced**|**Support removed**|  
|-|-|-|  
|With the arrival of the new Software Center experience in version 1511, apps that would have appeared only in the Application Catalog (user-available apps) now appear in Software Center. </br></br>With this primary functionality of the Application Catalog now included in Software Center, the web-based Application Catalog experience will no longer be available in the coming months.|August 11, 2017| Support for the Application Catalog web site user experience ends with the first update released after June 1, 2018|
|Software Center has a new, modern look. In the coming months, the previous version of Software Center will no longer be available.<br><br>You can set up clients to use the new Software Center by enabling the client setting, **Computer Agent** > **Use new Software Center**.<br><br>For more information about Software Center, see [Plan for and configure application management in System Center Configuration Manager](https://docs.microsoft.com/sccm/apps/plan-design/plan-for-and-configure-application-management).|December 13, 2016|Support for the previous version of Software Center ends with the first update released after January 1, 2018.|
|Management of Virtual Hard Disks (VHDs) with Configuration Manager. </br></br>This includes removal of options to create a new VHD or manage a VHD using a task sequence, and the removal of the Virtual Hard Disks node from the Configuration Manager console. </br></br>When this support is removed, existing VHDs will not be deleted, but will no longer be accessible from within the Configuration Manager console.  |January 6, 2017 |Version 1710|
|Task sequences: <br /> - Convert Disk to Dynamic <br /> - Install Deployment Tools |November 18, 2016|Version 1710|
|System Center Configuration Manager Upgrade Assessment Tool. </br></br>The Upgrade Assessment Tool depends on both System Center Configuration Manager and the Application Compatibility Toolkit (ACT) 6.x. The final version of ACT was shipped in the Windows 10 v1511 ADK. As there will be no further updates to ACT, support for the Upgrade Assessment Tool will be discontinued. </br></br>The Upgrade Assessment Tool is replaced by the [Upgrade Readiness](/sccm/core/clients/manage/upgrade/upgrade-analytics) feature. Deprecation notice was added to the [download page for UAT](https://www.microsoft.com/download/details.aspx?id=37145) on September 12, 2016. | September 12, 2016  | July 11, 2017 |
|Task sequences: <br /> - OSDPreserveDriveLetter  <br /><br /> During an operating system deployment, by default, Windows Setup now determines the best drive letter to use (typically C:). If you want to specify a different drive to use, you can change the location in the Apply Operating System task sequence step. Go to the **Select the location where you want to apply this operating system** setting. Select **Specific logical drive letter** and choose the drive that you want to use. |June 20, 2016 |Version 1606 |
|Network Access Protection (NAP)  - as found in System Center 2012 Configuration Manager|July 10, 2015|Version 1511|  
|Out of Band Management - as found in System Center 2012 Configuration Manager|October 16, 2015|Version 1511|



<br></br>
Additional details for features removed with version 1511 of System Center Configuration Manager release:

###  <a name="bkmk_amt"></a> Out of Band Management  
 With Configuration Manager, native support for AMT-based computers from within the Configuration Manager console has been removed.  

-   AMT-based computers remain fully managed when you use the [Intel SCS Add-on for Microsoft System Center Configuration Manager](http://www.intel.com/content/www/us/en/software/setup-configuration-software.html). The add-on provides you access to the latest capabilities to manage AMT, while removing limitations introduced until Configuration Manager could incorporate those changes.  

-   Out of Band Management in System Center 2012 Configuration Manager is not affected by this change.  

###  <a name="bkmk_nap"></a> Network Access Protection  
 System Center Configuration Manager has removed support for  Network Access Protection. The feature has been deprecated in Windows Server 2012 R2, and is removed from Windows 10.  

 For network access protection alternatives, see the *Deprecated functionality* section of [Network Policy and Access Services Overview](https://technet.microsoft.com/library/hh831683.aspx).

## More Information
For more information, see:
 - [Removed and Deprecated] (/sccm/core/plan-design/changes/deprecated/removed-and-deprecated.md)
 - The [Microsoft Support Lifecycle](https://support.microsoft.com/lifecycle) website.
 - [Support for current branch versions of Configuration Manager](/sccm/core/servers/manage/current-branch-versions-supported).
