---
title: "Prerequisites for reporting"
titleSuffix: "Configuration Manager"
description: "Understand various dependencies that impact your use of reporting in System Center Configuration Manager."
ms.date: 01/29/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9cc508a5-5023-4833-b776-ae9a6971138f
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# Prerequisites for reporting in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

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
|SQL Server 2017 with a minimum of cumulative update 2<br /><br /> -   Standard<br />-   Enterprise|Yes, starting in Configuration Manager version 1710|  
|SQL Server 2016 with SP1<br /><br /> -   Standard<br />-   Enterprise|Yes| 
|SQL Server 2016<br /><br /> -   Standard<br />-   Enterprise|Yes|
|SQL Server 2014 with SP2<br /><br /> -   Standard<br />-   Enterprise|Yes|
|SQL Server 2014 with SP1<br /><br /> -   Standard<br />-   Enterprise|Yes|
|SQL Server 2012 with SP4 <br /><br /> -   Standard<br />-   Enterprise|Yes|  
|SQL Server 2012 with SP3 <br /><br /> -   Standard<br />-   Enterprise|Yes|  
|SQL Server 2008 R2 with SP3<br /><br /> -   Standard<br />-   Enterprise<br />-   Datacenter|Yes, for supported versions of Configuration Manager prior to 1702.|  
|SQL Server Express 2008 R2 with SP3|Not Supported| 




## Next steps
[Operations and maintenance for reporting](operations-and-maintenance-for-reporting.md)
