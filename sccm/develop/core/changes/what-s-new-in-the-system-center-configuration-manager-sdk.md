---
title: SDK what's new
titleSuffix: Configuration Manager
description: Learn about the latest additions or changes to the Configuration Manager software development kit (SDK).
ms.date: 04/12/2018
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 0ed5fda0-71b4-471b-bcf7-20d4e3802bb3
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# What's new in the System Center Configuration Manager SDK
This article lists any recent additions or changes to the Configuration Manager software development kit (SDK).  


## Configuration Manager SDK redistributables available on NuGet   
In addition to the [Client Messaging SDK package](https://www.nuget.org/packages/Microsoft.ConfigurationManagement.Messaging/), additional libraries are now available on NuGet.


### Management point API (MPAPI)

The MPAPI contains the management point interface libraries.

- [Microsoft.ConfigurationManagement.MPAPI.i386](https://www.nuget.org/packages/Microsoft.ConfigurationManagement.MPAPI.i386/)  

- [Microsoft.ConfigurationManagement.MPAPI.amd64](https://www.nuget.org/packages/Microsoft.ConfigurationManagement.MPAPI.amd64/)  

For more information, see the [MPAPI documentation](https://msdn.microsoft.com/library/cc144951.aspx) for these libraries on MSDN.  

> [!Note]  
> The MPAPI documentation is planned to migrate to the docs.microsoft.com platform in the future.  


### Install status MIF COM library (ISMIFCOM)

ISMIFCOM is a COM library with a class wrapper for the install status MIF functions.  

- [Microsoft.ConfigurationManagement.ISMIFCOM.i386](https://www.nuget.org/packages/Microsoft.ConfigurationManagement.ISMIFCOM.i386/)  

- [Microsoft.ConfigurationManagement.ISMIFCOM.amd64](https://www.nuget.org/packages/Microsoft.ConfigurationManagement.ISMIFCOM.amd64/)

For more information, see the [ISMIFCOM documentation](/sccm/develop/reference/core/servers/manage/status-mif-functions).


### Data discovery record creation libraries 

SMSRsGen and SMSRsGenCtl are legacy COM libraries used to create data discovery records (DDRs). 

> [!Important]  
> These are legacy libraries. The current recommendation is to use the Client Messaging SDK [DiscoveryDataRecordFile class](https://msdn.microsoft.com/library/microsoft.configurationmanagement.messaging.messages.server.discoverydatarecordfile.aspx). Use the latest [Client Messaging SDK package](https://www.nuget.org/packages/Microsoft.ConfigurationManagement.Messaging/) from NuGet.  

- [Microsoft.ConfigurationManagement.SMSRsGen.i386](https://www.nuget.org/packages/Microsoft.ConfigurationManagement.SMSRsGen.i386/)  

- [Microsoft.ConfigurationManagement.SMSRsGen.amd64](https://www.nuget.org/packages/Microsoft.ConfigurationManagement.SMSRsGen.amd64/)  

- [Microsoft.ConfigurationManagement.SMSRsGenCtl.i386](https://www.nuget.org/packages/Microsoft.ConfigurationManagement.SMSRsGenCtl.i386/)  

- [Microsoft.ConfigurationManagement.SMSRsGenCtl.amd64](https://www.nuget.org/packages/Microsoft.ConfigurationManagement.SMSRsGenCtl.amd64/)  

For more information, see the [SMSResGen documentation](/sccm/develop/reference/core/servers/configure/smsresgen-com-automation-class)  


## See Also  
- [Configuration Manager SDK](../../../develop/core/misc/system-center-configuration-manager-sdk.md)  
- [Get started with Configuration Manager cmdlets for Windows PowerShell](https://docs.microsoft.com/powershell/sccm/configurationmanager/)  