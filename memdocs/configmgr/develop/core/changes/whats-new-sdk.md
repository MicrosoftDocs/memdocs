---
title: SDK what's new
titleSuffix: Configuration Manager
description: Learn about the latest additions or changes to the Configuration Manager software development kit (SDK).
ms.date: 12/01/2021
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: conceptual
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth
---

# What's new in the Configuration Manager SDK

This article lists any recent additions or changes to the Configuration Manager software development kit (SDK).

## External dependencies require .NET 4.6.2

<!--10529267-->

Starting in version 2111, all Configuration Manager libraries are built using Microsoft .NET Framework version 4.6.2 or later. If you develop an application or tool that depends upon these libraries, it also needs to support .NET 4.6.2 or later. Microsoft recommends using .NET Framework version 4.8.

Applications or tools that use Configuration Manager WMI classes and methods, REST APIs, or PowerShell cmdlets aren't affected.

If you develop a third-party add-on to Configuration Manager, you should test your add-on with every monthly [technical preview branch release](../../../core/get-started/technical-preview.md). Regular testing helps confirm compatibility, and allows for early reporting of any issues with standard interfaces.

## Configuration Manager SDK redistributable files available on NuGet

### Client messaging

[Client messaging SDK package](https://www.nuget.org/packages/Microsoft.ConfigurationManagement.Messaging/)

### Management point API (MPAPI)

The MPAPI contains the management point interface libraries.

- [Microsoft.ConfigurationManagement.MPAPI.i386](https://www.nuget.org/packages/Microsoft.ConfigurationManagement.MPAPI.i386/)

- [Microsoft.ConfigurationManagement.MPAPI.amd64](https://www.nuget.org/packages/Microsoft.ConfigurationManagement.MPAPI.amd64/)

For more information, see the [MPAPI documentation](/previous-versions/system-center/developer/cc144951(v=msdn.10)).

### Install status MIF COM library (ISMIFCOM)

ISMIFCOM is a COM library with a class wrapper for the install status MIF functions.

- [Microsoft.ConfigurationManagement.ISMIFCOM.i386](https://www.nuget.org/packages/Microsoft.ConfigurationManagement.ISMIFCOM.i386/)

- [Microsoft.ConfigurationManagement.ISMIFCOM.amd64](https://www.nuget.org/packages/Microsoft.ConfigurationManagement.ISMIFCOM.amd64/)

For more information, see the [ISMIFCOM documentation](../../reference/core/servers/manage/status-mif-functions.md).

### Data discovery record creation libraries

SMSRsGen and SMSRsGenCtl are legacy COM libraries used to create data discovery records (DDRs).

> [!IMPORTANT]
> These are legacy libraries. The current recommendation is to use the Client Messaging SDK [DiscoveryDataRecordFile class](/previous-versions/system-center/developer/mt778052(v=cmsdk.12)). Use the latest [Client Messaging SDK package](https://www.nuget.org/packages/Microsoft.ConfigurationManagement.Messaging/) from NuGet.

- [Microsoft.ConfigurationManagement.SMSRsGen.i386](https://www.nuget.org/packages/Microsoft.ConfigurationManagement.SMSRsGen.i386/)

- [Microsoft.ConfigurationManagement.SMSRsGen.amd64](https://www.nuget.org/packages/Microsoft.ConfigurationManagement.SMSRsGen.amd64/)

- [Microsoft.ConfigurationManagement.SMSRsGenCtl.i386](https://www.nuget.org/packages/Microsoft.ConfigurationManagement.SMSRsGenCtl.i386/)

- [Microsoft.ConfigurationManagement.SMSRsGenCtl.amd64](https://www.nuget.org/packages/Microsoft.ConfigurationManagement.SMSRsGenCtl.amd64/)

For more information, see the [SMSResGen documentation](../../reference/core/servers/configure/smsresgen-com-automation-class.md)

## See also

- [Configuration Manager SDK](../../../develop/core/misc/system-center-configuration-manager-sdk.md)

- [Get started with Configuration Manager cmdlets for Windows PowerShell](/powershell/sccm/configurationmanager/)
