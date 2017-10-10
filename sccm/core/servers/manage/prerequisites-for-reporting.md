---
title: "Prerequisites for reporting"
titleSuffix: "Configuration Manager"
description: "Understand various dependencies that impact your use of reporting in System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 9cc508a5-5023-4833-b776-ae9a6971138f
caps.latest.revision: 5
caps.handback.revision: 0
author: Dougebyms.author: dougebymanager: angrobe

---
# Prerequisites for reporting in System Center Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*
Reporting in System Center Configuration Manager has external dependencies and dependencies within the product.  

## Dependencies external to Configuration Manager  
 The following table lists the external dependencies for reporting.  

|Prerequisite|More information|  
|------------------|----------------------|  
|SQL Server Reporting Services|Before you can use reporting in Configuration Manager, you must install and configure SQL Server Reporting Services.<br /><br /> For information about planning and deploying Reporting Services in your environment, see the [Reporting Services](http://go.microsoft.com/fwlink/p/?LinkId=212032) section in the SQL Server 2008 Books Online.|  
|Site system role dependencies for the computers that run the reporting services point.|[Supported configurations for System Center Configuration Manager](../../../core/plan-design/configs/supported-configurations.md)|  

## Dependencies internal to Configuration Manager  
 The following table lists the dependencies for reporting in Configuration Manager.  

|Prerequisite|More information|  
|------------------|----------------------|  
|Reporting services point|The reporting services point site system role must be configured before you can use reporting in Configuration Manager. For more information about how to install and configure a reporting services point, see [Configuring reporting in System Center Configuration Manager](../../../core/servers/manage/configuring-reporting.md).|  

## Supported SQL Server versions for the Reporting Services Point  
 The Reporting Services database can be installed on either the default instance or a named instance of a 64-bit SQL Server installation. The SQL Server instance can be co-located with the site system server, or on a remote computer.  

 The following table lists the SQL Server versions that are supported by the reporting services point.  

|SQL Server version|Reporting Services point|  
|------------------------|------------------------------|  
|SQL Server 2008 SP2 with a minimum of cumulative update 9<br /><br /> -   Standard<br />-   Enterprise<br />-   Datacenter|Yes|  
|SQL Server 2008 SP3 with a minimum of cumulative update 4<br /><br /> -   Standard<br />-   Enterprise<br />-   Datacenter|Yes|  
|SQL Server 2008 R2 with SP1 and with a minimum of cumulative update 6<br /><br /> -   Standard<br />-   Enterprise<br />-   Datacenter|Yes|  
|SQL Server 2008 R2 with SP2<br /><br /> -   Standard<br />-   Enterprise<br />-   Datacenter|Yes|  
|SQL Server Express 2008 R2 with SP1 and with a minimum of cumulative update 4|Not Supported|  
|SQL Server Express 2008 R2 with SP2|Not Supported|  
|SQL Server 2012 and with a minimum of cumulative update 2<br /><br /> -   Standard<br />-   Enterprise|Yes|  
|SQL Server 2012 with SP1 and no minimum cumulative update<br /><br /> -   Standard<br />-   Enterprise|Yes|  
|SQL Server 2014<br /><br /> -   Standard<br />-   Enterprise|Yes|
|SQL Server 2016<br /><br /> -   Standard<br />-   Enterprise|Yes|
|SQL Server 2016 with SP1<br /><br /> -   Standard<br />-   Enterprise|Yes|
## Next steps
[Operations and maintenance for reporting](operations-and-maintenance-for-reporting.md)
