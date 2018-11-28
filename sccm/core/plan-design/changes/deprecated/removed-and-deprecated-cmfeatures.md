---
title: Deprecated features
titleSuffix: Configuration Manager
description: Learn about the features that Configuration Manager no longer supports.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 287a6324-ae65-4d38-b2ef-198d47c91231
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Removed and deprecated features for Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

This article lists the features that are deprecated or removed from support for Configuration Manager. Deprecated features will be removed in a future update. These future changes might affect your use of Configuration Manager.  

This information is subject to change with future releases. It might not include each deprecated Configuration Manager feature.



## Deprecated features  

|Feature|Deprecation first announced|Support&nbsp;removed|  
|-----------|---|--------------|  
|Classic service deployment to Azure for cloud management gateway and cloud distribution point. For more information, see [Plan for CMG](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#azure-resource-manager).|November 2018|The first version released after July 1, 2019| 
|System Center Endpoint Protection for Mac and Linux<br>For more information, see [End of support blog post](https://go.microsoft.com/fwlink/?linkid=870182).|October 2018|December 31, 2018|
|Hybrid mobile device management. For more information, see [What is hybrid MDM](/sccm/mdm/understand/hybrid-mobile-device-management).<!--Intune feature 2683117-->|August 14, 2018|September 1, 2019|
|The **Silverlight user experience** for the application catalog website point is no longer supported. Users should use the new Software Center. NOTE: The application catalog website point and web service point roles are still supported. In some scenarios, the new Software Center communicates with the application catalog website point. For more information, see [Configure Software Center](/sccm/apps/plan-design/plan-for-and-configure-application-management#bkmk_userex).<!--1358309-->|August 11, 2017| Version 1806|
|The previous version of Software Center.<br><br>For more information about the new Software Center, see [Plan for and configure application management](/sccm/apps/plan-design/plan-for-and-configure-application-management##bkmk_userex).|December 13, 2016|Version 1802|
|Management of Virtual Hard Disks (VHDs) with Configuration Manager. </br></br>This deprecation includes removal of options to create a new VHD or manage a VHD using a task sequence, and the removal of the Virtual Hard Disks node from the Configuration Manager console. </br></br>Existing VHDs are not deleted, but are no longer accessible from within the Configuration Manager console.  |January 6, 2017 |Version 1710|
|Task sequences: <br /> - Convert Disk to Dynamic <br /> - Install Deployment Tools |November 18, 2016|Version 1710|
|System Center Configuration Manager Upgrade Assessment Tool. </br></br>The Upgrade Assessment Tool depends on both System Center Configuration Manager and the Application Compatibility Toolkit (ACT) 6.x. The final version of ACT was shipped in the Windows 10 v1511 ADK. As there are no further updates to ACT, support for the Upgrade Assessment Tool is discontinued. </br></br>The Upgrade Assessment Tool is replaced by the [Upgrade Readiness](/sccm/core/clients/manage/upgrade/upgrade-analytics) feature. Deprecation notice was added to the [download page for UAT](https://www.microsoft.com/download/details.aspx?id=37145) on September 12, 2016. | September 12, 2016  | July 11, 2017 |
|Software update points with a network load balancing (NLB) cluster | February 27, 2016 | Version 1702 | 
|Task sequences: <br /> - OSDPreserveDriveLetter  <br /><br /> During an operating system deployment, by default, Windows Setup now determines the best drive letter to use (typically C:). If you want to specify a different drive to use, you can change the location in the Apply Operating System task sequence step. Go to the **Select the location where you want to apply this operating system** setting. Select **Specific logical drive letter** and choose the drive that you want to use. |June 20, 2016 |Version 1606 |
|Network Access Protection (NAP)  - as found in System Center 2012 Configuration Manager|July 10, 2015|Version 1511|  
|Out of Band Management - as found in System Center 2012 Configuration Manager|October 16, 2015|Version 1511|



## Features removed in version 1511
The following sections include additional details for features removed with version 1511:

###  <a name="bkmk_amt"></a> Out of Band Management  
 With Configuration Manager, native support for AMT-based computers from within the Configuration Manager console has been removed.  

-   AMT-based computers remain fully managed when you use the [Intel SCS Add-on for Microsoft System Center Configuration Manager](http://www.intel.com/content/www/us/en/software/setup-configuration-software.html). The add-on provides you access to the latest capabilities to manage AMT, while removing limitations introduced until Configuration Manager could incorporate those changes.  

-   Out of Band Management in System Center 2012 Configuration Manager is not affected by this change.  

###  <a name="bkmk_nap"></a> Network Access Protection  
 System Center Configuration Manager has removed support for  Network Access Protection. The feature has been deprecated in Windows Server 2012 R2, and is removed from Windows 10.  

 For network access protection alternatives, see the *Deprecated functionality* section of [Network Policy and Access Services Overview](https://technet.microsoft.com/library/hh831683.aspx).



## More information
For more information, see:
 - [Removed and deprecated](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated)
 - [Microsoft Support Lifecycle](https://support.microsoft.com/lifecycle)
 - [Support for current branch versions of Configuration Manager](/sccm/core/servers/manage/current-branch-versions-supported).
