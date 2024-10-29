---
title: SoftDistDownloadFailedEvent
titleSuffix: Configuration Manager
description: In Configuration Manager, the SoftDistDownloadFailedEvent message is raised when a download for a package fails. It appears in Package Status in the Configuration Manager console.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 8ab548ad-ebec-48cc-b0dc-5541b17044f9
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SoftDistDownloadFailedEvent
In Configuration Manager, the `SoftDistDownloadFailedEvent` message is raised when a download for a package fails. It appears in **Package Status** in the Configuration Manager console.  

 `SoftDistDownloadFailedEvent` is derived from the [SoftwareDistributionPackageEvent](../../../../../develop/reference/core/servers/manage/softwaredistributionpackageevent.md) class, and each base class property must be set.  

 The text of the status message is:  

 %11Content download for the package "%4" - "%2" has failed.%12.%nPossible cause: The content can't be found on the network, or the content couldn't be accessed. %nSolution: Check to ensure this content has been made available on a distribution point. Check to ensure the access control list allows this program to be accessed. Check to make sure that the file system path for the content, including the path to the cache directory, isn't greater than 255 characters.%0.  

## Properties  
 `ClientID`  
 Data type: `String`  

 The SMS identifier of the client raising this event.  

 `PackageId`  
 Data type: `String`  

 The Package ID of the package to which status message refers. It maps to the `PKG_PackageID` field in the software distribution policy and to the **Package ID** in the Configuration Manager console.  

 `PackageName`  
 Data type: `String`  

 The Package ID, but it's an insertion string that appears in the status message text. It maps to the `PKG_PackageID` field in the software distribution policy and to the **Package ID** in the Configuration Manager console. This is insertion string number 4.  

 `PackageVersion`  
 Data type: `String`  

 The package version. It's the value that appears in the status message text. It isn't the value that is specified in the Configuration Manager console. It maps to `PKG_SourceVersion` field in the software distribution policy. This is insertion string number 2.  

 `Severity`  
 Data type: `Int32`  

 The severity of the failed event. The default value is 2.  
