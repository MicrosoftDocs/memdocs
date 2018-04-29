---
title: "SoftDistDownloadCompletedEvent"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: fc9e6152-e147-4818-a3cf-2f5f8cfd087e
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SoftDistDownloadCompletedEvent
In Configuration Manager, the `SoftDistDownloadCompletedEvent` message is sent when the download for a package is completed. The message appears in **Package Status** in the Configuration Manager console.  

 `SoftDistDownloadCompletedEvent` is derived from the [SoftwareDistributionPackageEvent](../../../develop/reference/core/servers/manage/softwaredistributionpackageevent.md) class, and each base class property must be set.  

 The text of the status message is:  

 %11Content download for the package "%4" - "%2" has completed successfully.%0  

## Properties  
 `DummyString1`  
 Data type: `String`  

 This property does not have to be set.  

 `DummyString3`  
 Data type: `String`  

 This property does not have to be set.  

 `PackageId`  
 Data type: `String`  

 Derived from `SoftwareDistributionPackageEvent`.  

 `PackageName`  
 Data type: `String`  

 Derived from `SoftwareDistributionPackageEvent`.  

 `PackageVersion`  
 Data type: `String`  

 Derived from `SoftwareDistributionPackageEvent`.  

## See Also  
 [Status Message Types](../../../develop/reference/core/servers/manage/status-message-types.md)
