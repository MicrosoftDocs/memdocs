---
title: "Deprecated features | Microsoft Docs"
description: "Learn about the features, products, and operating systems that System Center Configuration Manager no longer supports."
ms.custom: na
ms.date: 08/16/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: d8c8b44c-1e8a-42b6-bab4-23c72a0a6169
caps.latest.revision: 15
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe

---
# Removed and deprecated features for System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

This topic describes features, products, and operating systems that are removed from support for System Center Configuration Manager, or will be removed in a future update (deprecated). This provides early notice about future changes that might affect your use of Configuration Manager.  

This information is subject to change with future releases, and might not include each deprecated feature, product, or operating system.  

## How to use this information  
When a feature or operating system is first listed as deprecated, support for using it with Configuration Manager is scheduled to be removed in a future version of Configuration Manager. This information is provided to help you plan for alternatives to using that feature or operating system. When the first version of Configuration Manager releases in which that support is removed, this topic is updated to indicate that specific version.  

When support is removed for a feature or operating system, the feature or operating system remains supported when you use a previous version of Configuration Manager, as long as that version of Configuration Manager remains in support. However, when you use a version of Configuration Manager released after the date or version indicated, that version of Configuration Manager does not provide support.

For example, if a feature was scheduled to have its support removed with the first update released after September 2016, support for that feature would no longer be included in update 1610, which released in October of 2016.
-  With Update 1610, the feature would no longer be supported.
-  This topic would be updated to indicate support was removed with version 1610.
However, if you continue to use an earlier version that supports the feature, like version 1602 or 1606, you can continue to use that feature until the version you use drops out of support.

For more information, see:
 - The [Microsoft Support Lifecycle](https://support.microsoft.com/lifecycle) website.
 - [Support for current branch versions of Configuration Manager](/sccm/core/servers/manage/current-branch-versions-supported).




## Deprecated operating systems
### Server operating systems  

|**Operating systems**|**Deprecation first announced**|**Support removed** |  
|-|-|-|  
|Windows Server 2008|July 10, 2015|Version 1511 </br></br>Support as a site system is removed. (See note 1).|  
|Windows Server 2008 R2|July 10, 2015| Version 1702  (See note 2)|  

-   Note 1: This operating system is not supported for site servers or site system roles with the exception of the distribution point and pull-distribution point. You can continue to use this operating system as a distribution point until deprecation of this support is announced, or this operating system's extended support period expires. For more information, see [Installation of System Center Configuration Manager CB and LTSB fails on Windows Server 2008](https://support.microsoft.com/help/4015095).

-   Note 2:    Beginning with version 1702, this operating system is not supported for site servers or most site system roles, however versions prior to 1702 continue to support its use. This operating system does remain supported for the distribution point site system role (including pull-distribution points, and for PXE and multicast) until deprecation of this support is announced, or this operating system's extended support period expires. Beginning with version 1602, you can upgrade in-place the operating system of a site server from Windows Server 2008 R2 to Windows Server 2012 R2.  

     For more information about in-place upgrade of a site servers operating system, see the [In-place upgrade the operating system of site servers that run Windows Server 2008 R2](../../../core/plan-design/changes/whats-new-in-version-1602.md#bkmk_UpgradeOS) section in [What's changed in System Center Configuration Manager](../../../core/plan-design/changes/what-has-changed-from-configuration-manager-2012.md).



### Client operating systems  

 Unless noted otherwise, each operating system that is supported as a Configuration Manager client is supported until the Extended Support End Date of that operating system. For details about Extended Support End Dates, see the [Microsoft Support Lifecycle](https://support.microsoft.com/lifecycle). If Configuration Manager support for an operating system will end prior to the Extended Support End Date, a deprecation date and support removal date for that operating system will be listed here.  

|**Operating systems**|**Deprecation first announced**|**Support removed**|  
|-|-|-|  
|Windows XP|July 10, 2015|Version 1511|  
|Windows XP Embedded <br><br> This includes all [XP-based Embedded operating systems](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices#windows-embedded-computers).|July 10, 2015|Version 1702|  
|Windows Server 2003|July 10, 2015|Version 1511|  
|Windows Server 2003 R2|July 10, 2015|Version 1511|  
|Windows Vista|July 10, 2015|Version 1511|  
|Mac OS X  10.6 - 10.8|July 10, 2015|Version 1511|  
|Windows Mobile 6.0 - 6.5|July 10, 2015|Version 1511|  
|Nokia Symbian Belle|July 10, 2015|Version 1511|  
|Windows CE 5.0 - 6.0|July 10, 2015|Version 1511|  


## Deprecated support for SQL Server versions as a site database  

|**SQL Server versions**|**Deprecation first announced**|**Support removed**|   
|-|-|-|  
|SQL Server 2008|July 10, 2015|Version 1511|  
|SQL Server 2008 R2|July 10, 2015|Version 1702|  

If you need to upgrade your version of SQL Server, We recommend the following methods, from easy to more complex.
1. [Upgrade SQL Server in-place](/sccm/core/servers/manage/upgrade-on-premises-infrastructure#a-namebkmksupconfigupgradedbsrva-upgrade-sql-server-on-the-site-database-server) (recommended).
2. Install a new version of SQL Server on a new computer, and then [use the database move option](/sccm/core/servers/manage/modify-your-infrastructure#a-namebkmkdbconfiga-modify-the-site-database-configuration) of Configuration Manager setup to point your site server to the new SQL Server.
3. Use [backup and recovery](/sccm/protect/understand/backup-and-recovery).


## Deprecated features  

|**Feature**|**Deprecation first announced**|**Support removed**|  
|-|-|-|  
|Network Access Protection (NAP)  - as found in System Center 2012 Configuration Manager|July 10, 2015|Version 1511|  
|Out of Band Management - as found in System Center 2012 Configuration Manager|October 16, 2015|Version 1511|
|Task sequences: <br /> - OSDPreserveDriveLetter  <br /><br /> During an operating system deployment, by default, Windows Setup now determines the best drive letter to use (typically C:). If you want to specify a different drive to use, you can change the location in the Apply Operating System task sequence step. Go to the **Select the location where you want to apply this operating system** setting, select **Specific logical drive letter**, and choose the drive that you want to use. |June 20, 2016 |Version 1606 |
|Task sequences: <br /> - Convert Disk to Dynamic <br /> - Install Deployment Tools |November 18, 2016|Support for these task sequences ends with the first update released after June 1, 2017.|
|Software Center has a new, modern look. In the coming months, the previous version of Software Center will no longer be available.<br><br>You can set up clients to use the new Software Center by enabling the client setting, **Computer Agent** > **Use new Software Center**.<br><br>For more information about Software Center, see [Plan for and configure application management in System Center Configuration Manager](https://docs.microsoft.com/sccm/apps/plan-design/plan-for-and-configure-application-management).|December 13, 2016|Support for the previous version of Software Center ends with the first update released after January 1, 2018.|
|With the arrival of the new Software Center experience in version 1511, apps that would have appeared only in the Application Catalog (user-available apps) now appear in Software Center. </br></br>With this primary functionality of the Application Catalog now included in Software Center, the web-based Application Catalog experience will no longer be available in the coming months.|August 11, 2017| Support for the Application Catalog web site user experience ends with the first update released after June 1, 2018|
|Management of Virtual Hard Disks (VHDs) with Configuration Manager. </br></br>This includes removal of options to create a new VHD or manage a VHD using a task sequence, and the removal of the Virtual Hard Disks node from the Configuration Manager console. </br></br>When this support is removed, existing VHDs will not be deleted, but will no longer be accessible from within the Configuration Manager console.  |January 6, 2017 |Support for VHDs ends with the first update released after June 1, 2017.|
|System Center Configuration Manager Upgrade Assessment Tool. </br></br>The Upgrade Assessment Tool depends on both System Center Configuration Manager and the Application Compatibility Toolkit (ACT) 6.x. The final version of ACT was shipped in the Windows 10 v1511 ADK. As there will be no further updates to ACT, support for the Upgrade Assessment Tool will be discontinued. </br></br>The Upgrade Assessment Tool is replaced by the [Upgrade Readiness](/sccm/core/clients/manage/upgrade/upgrade-analytics) feature. Deprecation notice was added to the [download page for UAT](https://www.microsoft.com/download/details.aspx?id=37145) on 9/12/2016. |9/12/2016  | July 11, 2017 |


<br></br>
Additional details for features removed with version 1511 of System Center Configuration Manager release:

###  <a name="bkmk_amt"></a> Out of Band Management  
 With Configuration Manager, native support for AMT-based computers from within the Configuration Manager console has been removed.  

-   AMT-based computers remain fully managed when you use the [Intel SCS Add-on for Microsoft System Center Configuration Manager](http://www.intel.com/content/www/us/en/software/setup-configuration-software.html). The add-on provides you access to the latest capabilities to manage AMT, while removing limitations introduced until Configuration Manager could incorporate those changes.  

-   Out of Band Management in System Center 2012 Configuration Manager is not affected by this change.  

###  <a name="bkmk_nap"></a> Network Access Protection  
 System Center Configuration Manager has removed support for  Network Access Protection. The feature has been deprecated in Windows Server 2012 R2, and is removed from Windows 10.  

 For network access protection alternatives, see the *Deprecated functionality* section of [Network Policy and Access Services Overview](https://technet.microsoft.com/library/hh831683.aspx).
