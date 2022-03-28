---
description: Learn ow to set the base class for all software distribution package related status messages using SoftWareDistributionPackageEvent.
title: "SoftwareDistributionPackageEvent"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: a2a3025d-3ac2-4253-9537-4743e8fc3d61
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SoftwareDistributionPackageEvent
In Configuration Manager, the `SoftwareDistributionPackageEvent` class is the base class for all software distribution-package-related status messages. Every status message has its own class that is derived from `SoftwareDistributionPackageEvent`; and therefore, all package status messages have the insertion strings of this class. Each status message that is derived from this class must set the base class `SoftwareDistributionPackageEvent` properties.  

## Properties  
 `ClientID`  
 Data type: `String`  

 The SMS identifier of the client raising this event.  

 `PackageId`  
 Data type: `String`  

 The Package ID of the package to which status message refers. It maps to the `PKG_PackageID` field in the software distribution policy and to the **Package ID** in the Configuration Manager console.  

 `PackageName`  
 Data type: `String`  

 The Package ID, but it is an insertion string that appears in the status message text. It maps to the `PKG_PackageID` field in the software distribution policy and to the **Package ID** in the Configuration Manager console. This is insertion string number 4.  

 `PackageVersion`  
 Data type: `String`  

 The package version. It is the value that appears in the status message text. It is not the value that is specified in the Configuration Manager console. It maps to `PKG_SourceVersion` field in the software distribution policy. This is insertion string number 2.  
