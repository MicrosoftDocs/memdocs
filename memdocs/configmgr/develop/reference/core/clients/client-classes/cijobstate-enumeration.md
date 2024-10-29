---
description: Learn how CIJobState enumeration defines configuration item agent job states and is used by ICIINFO Interface.
title: CIJobState Enumeration
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 3bdac2a9-16af-4dbb-bea2-3075837acd0e
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# CIJobState Enumeration
In Configuration Manager, the `CIJobState` enumeration defines configuration item agent job states. This enumeration is used by the [ICIINFO Interface](../../../../../develop/reference/core/clients/client-classes/iciinfo-interface.md).  

## Syntax  

```  
typedef enum tagCIJobState  
{  
  ciJobStateNone = 0,  
  ciJobStateAvailable,  
  ciJobStateSubmitted,  
  ciJobStateDetecting,  
  ciJobStateDownloadingCIDef,  
  ciJobStateDownloadingSdmPkg,  
  ciJobStatePreDownload,  
  ciJobStateDownloading,  
  ciJobStateWaitInstall,  
  ciJobStateInstalling,  
  ciJobStatePendingSoftReboot,  
  ciJobStatePendingHardReboot,  
  ciJobStateWaitReboot,  
  ciJobStateVerifying,  
  ciJobStateInstallComplete,  
  ciJobStateError,  
  ciJobStateWaitServiceWindow  
} CIJobState;  
```  

## Elements  
 `ciJobStateNone`  
 No state.  

 `ciJobStateAvailable`  
 Available.  

 `ciJobStateSubmitted`  
 Submitted.  

 `ciJobStateDetecting`  
 Being detected.  

 `ciJobStateDownloadingCIDef`  
 Downloading configuration item definition.  

 `ciJobStateDownloadingSdmPkg`  
 Downloading a System Definition Model (SDM) package.  

 `ciJobStatePreDownload`  
 Pre-download.  

 `ciJobStateDownloading`  
 Downloading.  

 `ciJobStateWaitInstall`  
 Wait for installation.  

 `ciJobStateInstalling`  
 Installing.  

 `ciJobStatePendingSoftReboot`  
 Suspend operation for soft reboot.  

 `ciJobStatePendingHardReboot`  
 Suspend operation for hard reboot.  

 `ciJobStateWaitReboot`  
 Wait for reboot.  

 `ciJobStateVerifying`  
 Verifying.  

 `ciJobStateInstallComplete`  
 Installation complete.  

 `ciJobStateError`  
 Error.  

 `ciJobStateWaitServiceWindow`  
 Wait for maintenance window.  

## See Also  
 [ICIINFO Interface](../../../../../develop/reference/core/clients/client-classes/iciinfo-interface.md)
