---
title: "Monitor app usage with software metering in System Center Configuration Manager"
ms.custom: na
ms.date: 2015-12-08
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: 
  - configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b1fdaee2-2816-4447-94cd-609f6948f215
caps.latest.revision: 8
author: barlanmsft
translation.priority.ht: 
  - cs-cz
  - de-de
  - en-gb
  - es-es
  - fr-fr
  - hu-hu
  - it-it
  - ja-jp
  - ko-kr
  - nl-nl
  - pl-pl
  - pt-br
  - pt-pt
  - ru-ru
  - sv-se
  - tr-tr
  - zh-cn
  - zh-tw
---
# Monitor app usage with software metering in System Center Configuration Manager
Use software metering in System Center Configuration Manager to monitor and collect software usage data from Windows PCs.  
  
 To collect this usage data, configure software metering rules or use inventory collected by Configuration Manager to generate these rules automatically. Clients evaluate these rules and collect metering data to send to the site. The Configuration Manager client continues to collect usage data when there is no connection to the site and sends this information when the connection is re-established.  
  
 After you collect usage data from clients, you can view the data in different ways, which includes using collections, queries, and reporting. This data, combined with data from software inventory, can help your organization to determine the following:  
  
-   How many copies of a particular app have been deployed to PCs in your organization. Among those PCs, you can determine how many users actually run the app.  
  
-   How many licenses of a particular app you have to purchase when you renew your license agreement with the app vendor.  
  
-   Whether users are still running a particular app. If the app is not being used, you might retire it.  
  
-   Which times of the day an app is most frequently used.  
  
> [!IMPORTANT]  
>  Software metering is used to monitor Windows desktop apps with a filename ending in **.exe**. Software metering does not monitor modern Windows apps (such as those used by Windows 8).  
  
 This topic contains an example scenario about how you might use software metering to solve a business problem. For details of all the options you can use, see [Software metering in System Center Configuration Manager](../../apps/deploy-use/software-metering.md).  
  
## Example scenario for using software metering  
 In this section, you'll create an example software metering rule that can help you solve the following business requirements:  
  
-   Determine how many copies of a particular app are in your company  
  
-   Discover any unused copies of an app  
  
-   Determine which users regularly use a particular app  
  
 Woodgrove Bank has deployed Microsoft Office 2010 as its standard office productivity suite. However, to support a legacy application, some computers must continue to run Microsoft Office Word 2003. The IT department wants to reduce support and licensing costs by removing these copies of Word 2003 if the legacy application is no longer used. The help desk also wants to identify which users use the legacy application.  
  
 John is Woodgrove Bank's IT Systems Manager who uses software metering in Configuration Manager to achieve these business objectives. He performs the actions in the following table:  
  
|Process|Details|  
|-------------|-------------|  
|John checks the prerequisites for software metering and confirms that the reporting services point is installed and operational.|[Prerequisites for software metering](../../apps/deploy-use/software-metering.md#BKMK_Pre)|  
|John configures the default client settings for software metering:<br /><br /> He enables software metering and uses the default data collection schedule of once every seven days.<br /><br /> He configures software inventory to inventory files that have the extension .exe by configuring the software inventory client setting **Inventory these file types**.<br /><br /> He adds a new software metering rule, named **woodgrove.exe**, to monitor the legacy application.|[Configure software metering](../../apps/deploy-use/software-metering.md#BKMK_Config)<br /><br /> [Create software metering rules](../../apps/deploy-use/software-metering.md#BKMK_Create)|  
|John waits for seven days, after which the client computers begin to report usage data for the **woodgrove.exe** executable.||  
|John uses the Configuration Manager report **Install base for all metered software programs** to see which computers have the application **woodgrove.exe** loaded.|[Monitor software metering](../../apps/deploy-use/software-metering.md#BKMK_Monitor)|  
|After six months, John runs the report **Computers that have a metered program installed, but have not run the program since a specified date**, specifying the software metering rule and a date six months in the past. This report identifies 120 computers that have not run the program in the past six months.|[Monitor software metering](../../apps/deploy-use/software-metering.md#BKMK_Monitor)|  
|John makes some further checks to confirm that the legacy application is not required on the identified computers. He then uninstalls the legacy application and the copy of Word 2003 from these computers.<br /><br /> John runs the report **Users that have run a specific metered software program** to provide the help desk with a list of users who continue to use the legacy application.|No additional information.|  
|John continues to check the software metering reports weekly and takes remedial action if necessary.|[Monitor software metering](../../apps/deploy-use/software-metering.md#BKMK_Monitor)|  
  
 As a result of this course of action, IT support and licensing costs are reduced by removing the applications that are no longer required. In addition, the help desk now has the list that it wanted of the users who run the legacy application.  
  
## See Also  
 [Monitor applications with System Center Configuration Manager](../Topic/Monitor%20applications%20with%20System%20Center%20Configuration%20Manager.md)