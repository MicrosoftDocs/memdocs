---
title: "Monitor Linux and UNIX clients | System Center Configuration Manager"
ms.custom: na
ms.date: 2015-12-08
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d827cf91-b18f-4ee7-b538-24ba6f003ab9
caps.latest.revision: 6
author: Mtillman
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
# How to monitor clients for Linux and UNIX servers in System Center Configuration Manager
You can view information from Linux and UNIX servers in the System Center Configuration Manager console using the same methods you use to view information from Windows-based clients.  

 The information you can view includes:  

-   Status details from clients, in the Configuration Manager console dashboards  

-   Details about clients in the default Configuration Manager reports  

-   Inventory details in the Resource Explorer  

 The following sections provide information about using the resource explorer and reports to view details about your Linux and UNIX servers.  

##  <a name="BKMK_UseResourceExpforLnU"></a> How to use Resource Explorer to View Inventory for Linux and UNIX Servers  
 You can view hardware and installed software details on Linux and UNIX servers by using Resource Explorer.  

 After a Configuration Manager client submits hardware inventory to the Configuration Manager site, you can use Resource Explorer to view this information. The Configuration Manager client for Linux and UNIX does not add new classes or views for inventory to the Resource Explorer. The Linux and UNIX inventory data maps to existing WMI classes. You can view the inventory details for your Linux and UNIX servers in the Windows-based classifications using Resource Explorer.  

 For example, you can collect the list of all natively installed programs found on your Linux and UNIX servers. Examples of natively installed programs include **.rpms** in Linux or **.pkgs** in Solaris. After inventory has been submitted by a Linux or UNIX client, you can view the list of all the natively installed Linux or UNIX programs in Resource Explorer in the Configuration Manager console.  

 For information about how to use Resource Explorer, see [How to use Resource Explorer to view hardware inventory in System Center Configuration Manager](../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md).  

##  <a name="BKMK_UseReportsforLnU"></a> How to use Reports to View Information for Linux and UNIX Servers  
 Reports for Configuration Manager include information from Linux and UNIX servers along with information from Windows-based computers. No additional configurations are required to integrate the Linux and UNIX data in the reports.  

 For example, if you run the report named Count of Operating System Versions, it displays the list of the different operating systems and the number of clients that are running each operating system. The report is based on the hardware inventory information that was sent by the different Configuration Manager clients that run on the different operating systems.  

 It is also possible to create custom reports that are specific to Linux and UNIX server data. The **Caption** property of the hardware inventory class **Operating System** is a useful attribute that you can use to identify specific Operating Systems in the report query.  

 For information about reports in Configuration Manager, see [Reporting in System Center Configuration Manager](../../../core/servers/manage/reporting.md).  
