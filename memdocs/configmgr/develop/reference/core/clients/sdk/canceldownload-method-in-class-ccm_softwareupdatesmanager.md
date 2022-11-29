---
description: Learn how to cancel an in-progress download of software updates during a deployment using the CancelDownload class method.
title: CancelDownload method in class CCM_SoftwareUpdatesManager
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 890faba7-0382-4189-adc6-8ea16a9296da
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# CancelDownload Method in Class CCM_SoftwareUpdatesManager
The `CancelDownload` WMI class method, in Configuration Manager, cancels an in-progress download of software updates during a deployment.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
UInt32 CancelDownload();  
```  

#### Parameters  
 None.  

## Return Values  
 A `UInt32` data type that is 0 to indicate success or nonzero to indicate failure.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).  

## Remarks  
 The `CancelDownload` method cancels the download only for deployments that are initiated by the Software Updates Client Agent or through the Configuration Manager SDK. If the software updates deployment was initiated as the result of a deadline, the call to this method fails.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  

## See Also  
 [CCM_SoftwareUpdatesManager Client WMI Class](../../../../../develop/reference/core/clients/sdk/ccm_softwareupdatesmanager-client-wmi-class.md)
