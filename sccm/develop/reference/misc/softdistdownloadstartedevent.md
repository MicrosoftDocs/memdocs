---
title: "SoftDistDownloadStartedEvent"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: aa6b5aa8-1de9-4057-8c91-c996ed72c1a1
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SoftDistDownloadStartedEvent
In Configuration Manager, the `SoftDistDownloadStartedEvent` message is sent when the download for a package is completed. The message appears in **Package Status** in the Configuration Manager console.  

 `SoftDistDownloadStartedEvent` is derived from the [SoftwareDistributionPackageEvent](../../../develop/reference/core/servers/manage/softwaredistributionpackageevent.md) class, and each base class property must be set.  

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
