---
description: Learn how to set a distribution point in maintenance mode using SetDPMaintenanceMode class method in Configuration Manager.
title: SetDPMaintenanceMode method
titleSuffix: Configuration Manager
ms.date: 05/24/2019
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: fd03d3a8-10db-4e0f-94d7-86f914ada72f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---

# SetDPMaintenanceMode method in class SMS_DistributionPoint

<!--3555754-->

The `SetDPMaintenanceMode` WMI class method in Configuration Manager sets a distribution point in maintenance mode. For more information, see [Maintenance mode](../../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_maint).

The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```MOF
uint32 SetDPMaintenanceMode(
    [in] string NALPath,
    [in] uint32 Mode
);
```  

## Parameters

### `NALPath`

Data type: `String`

Qualifiers: `[in]`

 Network abstraction layer (NAL) path to the distribution point server.  

### `Mode`

Data type: `uint32`

Qualifiers: `[in]`

`1` to enable maintenance mode, `0` to disable  


## Return values

An `uint32` data type that's `0` indicates success. A non-zero hresult indicates failure.  

For more information about handling returned errors, see [About Configuration Manager errors](../../../../core/understand/about-configuration-manager-errors.md).  


## Requirements  

### Runtime requirements

For more information, see [Configuration Manager server runtime requirements](../../../../core/reqs/server-runtime-requirements.md).  

### Development requirements

For more information, see [Configuration Manager server development requirements](../../../../core/reqs/server-development-requirements.md).  


## See also

[SMS_DistributionPointInfo Server WMI Class](sms_distributionpointinfo-server-wmi-class.md)
