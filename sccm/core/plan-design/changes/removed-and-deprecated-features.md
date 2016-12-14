---
title: "Deprecated features | Microsoft Docs"
description: "Learn about the features, products, and operating systems that System Center Configuration Manager no longer supports."
ms.custom: na
ms.date: 12/05/2016
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
author: Brendunsms.author: brendunsmanager: angrobe

---
# Removed and deprecated features for System Center Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*
This topic describes features, products, and operating systems that are removed from support with System Center Configuration Manager or will be removed in a future update (Deprecated). This is intended to provide early warning about future changes that might affect your use of Configuration Manager.  

 This information is subject to change with future releases and might not include each deprecated feature, product, or operating system.  

## How to use this information  
When a feature or operating system is first listed as deprecated, support for using it with Configuration Manager is scheduled to be removed in a future version of Configuration Manager. This information is provided to help assist you in planning for alternatives to using that feature or operating system.  When the first version of Configuration Manager releases in which that support is removed, the details in this topic will update to indicate that specific version.  

When support is removed for a feature or operating system, the feature or operating system remains supported when you use a previous version of Configuration Manager so long as that version of Configuration Manager remains in support. However, when you use a version of Configuration Manager released after the date or version indicated, that version of Configuration Manager does not provide support.

**For example:**
If a feature was scheduled to have its support removed with the first update released after September 2016, this would mean support for that feature would no longer be included in update 1610, which released in October of 2016.
-  With Update 1610, the feature would no longer be supported.
-  This content would update to indicate support was removed with version 1610.
However, if you continue to use an earlier version that supports the feature, like version 1602 or 1606, you can continue to use that feature until the version you use drops out of support.

For more information, see:
 - The [Microsoft Support Lifecycle](https://support.microsoft.com/lifecycle) website
 - [Support for current branch versions of Configuration Manager](/sccm/core/servers/manage/current-branch-versions-supported)

**Deprecated features:**  


|**Feature**|**Deprecation first announced**|**Support removed**|  
|-|-|-|  
|Network Access Protection (NAP)  - as found in System Center 2012 Configuration Manager|7/10/2015|Version 1511|  
|Out of Band Management - as found in System Center 2012 Configuration Manager|10/16/2015|Version 1511|
|Task Sequences: <br /> - Convert Disk to Dynamic <br /> - Install Deployment Tools |11/18/2016|Support for these task sequences ends with the first update released after June 1st, 2017|
|The new Software Center has a new, modern look and apps that would have appeared only in the Silverlight-dependent Application Catalog (user-available apps) now appear in Software Center under the **Applications** tab. The Application Catalog can still be accessed using the link under the **Installation Status** tab of Software Center.<br><br>In the coming months, we will be removing the previous version of Software Center, and it will no longer be available for you to use.<br><br>You can configure clients to use the new Software Center by enabling the client setting **Computer Agent** > **Use new Software Center**.<br><br>For more information about Software Center, see [Plan for and configure application management in System Center Configuration Manager](https://docs.microsoft.com/sccm/apps/plan-design/plan-for-and-configure-application-management).|12/13/2016|To be announced| 

 **Deprecated server operating systems:**  

 |**Operating systems**|**Deprecation first announced**|**Support removed** |  
|-|-|-|  
|Windows Server 2008|7/10/2015|Support ends with the first update released after 12/31/2016  *(See note 1)*|  
|Windows Server 2008 R2|7/10/2015|Support ends with the first update released after 12/31/2016  *(See note 2)*|  

-   *Note 1*:   After support ends, this operating system will no longer be supported for site servers or most site system roles. However, it will remain supported for the distribution point site system role (including pull-distribution point) until deprecation of this support is announced or this operating system's extended support period expires.  

-   *Note 2*:    After support ends, this operating system will no longer be supported for site servers or most site system roles. However, it will remain supported for the state migration point and distribution point site system role (including pull-distribution points, and for PXE and multi-cast) until deprecation of this support is announced or this operating system's extended support period expires.  Beginning with version 1602, you can in-place upgrade the operating system of a site server from Windows Server 2008 R2 to Windows  Server 2012 R2.  

     For more information about in-place upgrade of a site servers operating system, see the [In-place upgrade the operating system of site servers that run Windows Server 2008 R2](../../../core/plan-design/changes/whats-new-in-version-1602.md#bkmk_UpgradeOS) section in [What's changed in System Center Configuration Manager](../../../core/plan-design/changes/what-has-changed-from-configuration-manager-2012.md).



 **Deprecated client operating systems:**  

 Unless noted otherwise, each operating system that is supported as a Configuration Manager client is supported until the Extended Support End Date of that operating system, as detailed in the [Microsoft Support Lifecycle](https://support.microsoft.com/lifecycle).  If Configuration Manager support for an operating system will end prior to the Extended Support End Date, a deprecation date and support removal date for that operating system will be listed here.  

|**Operating systems**|**Deprecation first announced**|**Support removed**|  
|-|-|-|  
|Windows XP|7/10/2015|Version 1511|  
|Windows XP Embedded|7/10/2015|Support ends with the first update released after 12/31/2016|  
|Windows Server 2003|7/10/2015|Version 1511|  
|Windows Server 2003 R2|7/10/2015|Version 1511|  
|Windows Vista|7/10/2015|Version 1511|  
|Mac OS X  10.6 - 10.8|7/10/2015|Version 1511|  
|Windows Mobile 6.0 - 6.5|7/10/2015|Version 1511|  
|Nokia Symbian Belle|7/10/2015|Version 1511|  
|Windows CE 5.0 - 6.0|7/10/2015|Version 1511|  


 **Deprecated support for SQL Server versions as a site database:**  

|**SQL Server versions**|**Deprecation first announced**|**Support removed**|   
|-|-|-|  
|SQL Server 2008|7/10/2015|Version 1511|  
|SQL Server 2008 R2|7/10/2015|Support ends with the first update released after 12/31/2016|  

## Features removed in System Center Configuration Manager  
 Beginning with the initial System Center Configuration Manager release, the following features are removed:

###  <a name="bkmk_amt"></a> Out of Band Management  
 With Configuration Manager, native support for AMT-based computers from within the Configuration Manager console has been removed.  

-   AMT-based computers remain fully managed when you use the [Intel SCS Add-on for Microsoft System Center Configuration Manager](http://www.intel.com/content/www/us/en/software/setup-configuration-software.html)  

-   Use of the Add-on provides you access to the latest capabilities to manage AMT while removing limitations introduced until Configuration Manager could incorporate those changes  

-   Out of Band Management in System Center 2012 Configuration Manager is not affected by this change  

###  <a name="bkmk_nap"></a> Network Access Protection  
 System Center Configuration Manager has removed support for  Network Access Protection. The feature has been deprecated in Windows Server 2012 R2 and is removed from Windows 10.  

 For network access protection alternatives, see the **Deprecated functionality** section of [Network Policy and Access Services Overview](https://technet.microsoft.com/library/hh831683.aspx).  
