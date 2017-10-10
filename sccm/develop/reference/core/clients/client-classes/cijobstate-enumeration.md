---
title: "CIJobState Enumeration"
ms.custom: ""
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.reviewer: ""
ms.suite: ""
ms.technology:
  - "configmgr-other"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to:
  - "System Center Configuration Manager (current branch)"
ms.assetid: 3bdac2a9-16af-4dbb-bea2-3075837acd0esearchScope: - ConfigMgr SDK
caps.latest.revision: 6
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# CIJobState Enumeration
In System Center Configuration Manager, the `CIJobState` enumeration defines configuration item agent job states. This enumeration is used by the [ICIINFO Interface](../../../../../develop/reference/core/clients/client-classes/iciinfo-interface.md).  

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
