---
title: Deprecated features
titleSuffix: Configuration Manager
description: Learn about the features that Configuration Manager no longer supports.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 287a6324-ae65-4d38-b2ef-198d47c91231
author: mestew
ms.author: mstewart
manager: dougeby
---

# Removed and deprecated features for Configuration Manager

*Applies to: Configuration Manager (current branch)*

This article lists the features that are deprecated or removed from support for Configuration Manager. Deprecated features will be removed in a future update. These future changes might affect your use of Configuration Manager.  

This information is subject to change with future releases. It might not include each deprecated Configuration Manager feature.

## Deprecated features

The following features are deprecated. You can still use them now, but Microsoft plans to end support in the future.

|Feature|Deprecation first announced|Support&nbsp;removed|
|-----------|---|--------------|
|The implementation for sharing content from Azure has changed. Use a content-enabled cloud management gateway. You won't be able to create a traditional cloud distribution point in the future.|February 2019|TBD<sup>[Note 1](#bkmk_note1)</sup>|
|Classic service deployment to Azure for cloud management gateway and cloud distribution point. For more information, see [Plan for CMG](../../../clients/manage/cmg/plan-cloud-management-gateway.md#azure-resource-manager).|November 2018|TBD<sup>[Note 1](#bkmk_note1)</sup>|

### <a name="bkmk_note1"></a> Note 1: Support removed TBD

The specific timeframe is to be determined (TBD). Microsoft recommends that you change to the new process or feature, but you can continue to use the deprecated process or feature for the near future.

## Unsupported and removed features

The following features are no longer supported. In some cases, they're no longer in the product.

|Feature|Deprecation first announced|Support&nbsp;removed|  
|-----------|---|--------------|  
| Desktop Analytics option to **View recent data** for device enrollment and security updates.<!-- 7080949 --> For more information, see [Data latency](../../../../desktop-analytics/troubleshooting.md#data-latency).|May 2020|July 2020|
| Windows Analytics and Upgrade Readiness integration. For more information, see [KB 4521815: Windows Analytics retirement on January 31, 2020](https://support.microsoft.com/help/4521815/windows-analytics-retirement). | October 14, 2019 | January 31, 2020 |
| Device health attestation assessment for conditional access compliance policies <!--1235616 aka 3608202--> For more information, see [What happened to hybrid MDM](../../../../mdm/understand/what-happened-to-hybrid.md).| July 3, 2019 | Version 1910 |
| The Configuration Manager Company Portal app | May 21, 2019 | Version 1910 |
| The application catalog, including both site system roles: the application catalog website point and web service point. For more information, see [Remove the application catalog](../../../../apps/plan-design/plan-for-and-configure-application-management.md#bkmk_remove-appcat). | May 21, 2019 | Version 1910 |
|Certificate-based authentication with Windows Hello for Business settings in Configuration Manager<br>For more information, see [Windows Hello for Business settings](../../../../protect/deploy-use/windows-hello-for-business-settings.md).|December 2017|Version 1910|
|System Center Endpoint Protection for Mac and Linux<br>For more information, see [End of support blog post](https://techcommunity.microsoft.com/t5/configuration-manager-blog/end-of-support-for-scep-for-mac-and-scep-for-linux-on-december/ba-p/286257).|October 2018|December 31, 2018|
|On-premises conditional access<br>For more information, see [What happened to hybrid MDM](../../../../mdm/understand/what-happened-to-hybrid.md).|January 30, 2019|September 1, 2019|
|Hybrid mobile device management (MDM)<br>For more information, see [What happened to hybrid MDM](../../../../mdm/understand/what-happened-to-hybrid.md).<br><br>Starting with the 1902 Intune service release, expected at the end of February 2019, new customers can't create a new hybrid connection.<!--Intune feature 2683117-->|August 14, 2018|September 1, 2019|
|Security Content Automation Protocol (SCAP) extensions. <!--3607889--><br>The previous certified version is still available on the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=48741).|September 2018|Version 1810|
|The **Silverlight user experience** for the application catalog website point is no longer supported. Users should use the new Software Center. For more information, see [Configure Software Center](../../../../apps/plan-design/plan-for-software-center.md#bkmk_userex).<!--1358309-->|August 11, 2017| Version 1806|
|The previous version of Software Center.<br><br>For more information about the new Software Center, see [Plan for and configure application management](../../../../apps/plan-design/plan-for-and-configure-application-management.md#bkmk_userex).|December 13, 2016|Version 1802|
|Management of Virtual Hard Disks (VHDs) with Configuration Manager. <br><br>This deprecation includes removal of options to create a new VHD or manage a VHD using a task sequence, and the removal of the Virtual Hard Disks node from the Configuration Manager console. <br><br>Existing VHDs are not deleted, but are no longer accessible from within the Configuration Manager console.  |January 6, 2017 |Version 1710|
|Task sequences: <br /> - Convert Disk to Dynamic <br /> - Install Deployment Tools |November 18, 2016|Version 1710|
|Upgrade Assessment Tool<br><br>The Upgrade Assessment Tool depends on both Configuration Manager and the Application Compatibility Toolkit (ACT) 6.x. The final version of ACT was shipped in the Windows 10 v1511 ADK. As there are no further updates to ACT, support for the Upgrade Assessment Tool is discontinued. Deprecation notice was added to the [download page for UAT](https://www.microsoft.com/software-download/windows10) on September 12, 2016. | September 12, 2016  | July 11, 2017 |
|Software update points with a network load balancing (NLB) cluster | February 27, 2016 | Version 1702 |
|Task sequences: <br /> - OSDPreserveDriveLetter  <br /><br /> During an operating system deployment, by default, Windows Setup now determines the best drive letter to use (typically C:). If you want to specify a different drive to use, you can change the location in the Apply Operating System task sequence step. Go to the **Select the location where you want to apply this operating system** setting. Select **Specific logical drive letter** and choose the drive that you want to use. |June 20, 2016 |Version 1606 |
|Network Access Protection (NAP)  - as found in System Center 2012 Configuration Manager|July 10, 2015|Version 1511|  
|Out of Band Management - as found in System Center 2012 Configuration Manager|October 16, 2015|Version 1511|

### Features removed in version 1511

The following sections include additional details for features removed with version 1511:

#### <a name="bkmk_amt"></a> Out of Band Management  

With Configuration Manager, native support for AMT-based computers from within the Configuration Manager console has been removed.  

- AMT-based computers remain fully managed when you use the [Intel SCS Add-on for Configuration Manager](https://www.intel.com/content/www/us/en/software/setup-configuration-software.html). The add-on provides you access to the latest capabilities to manage AMT, while removing limitations introduced until Configuration Manager could incorporate those changes.  

- Out of Band Management in System Center 2012 Configuration Manager is not affected by this change.  

#### <a name="bkmk_nap"></a> Network Access Protection

Configuration Manager has removed support for Network Access Protection. The feature has been deprecated in Windows Server 2012 R2, and is removed from Windows 10.  

For network access protection alternatives, see the *Deprecated functionality* section of [Network Policy and Access Services Overview](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831683(v=ws.11)).

## See also

- [Removed and deprecated](removed-and-deprecated.md)
- [Microsoft Support Lifecycle](https://support.microsoft.com/lifecycle)
- [Support for current branch versions of Configuration Manager](../../../servers/manage/current-branch-versions-supported.md)
