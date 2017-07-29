---
title: "ICcmAlternateDownloadProvider Interface | Microsoft Docs"
ms.custom: ""
ms.date: "07/25/2017"
ms.prod: "configuration-manager"
ms.reviewer: ""
ms.suite: ""
ms.technology:
  - "configmgr-other"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to:
  - "System Center Configuration Manager (current branch)"
ms.assetid: 42eb99e9-6421-415d-8e80-7e8f8b322cb3
searchScope:
 - ConfigMgr SDK
caps.latest.revision: 12
author: "lleonard-msft"
ms.author: "alleonar"
manager: "angrobe"
---
# ICcmAlternateDownloadProvider Interface
The **ICcmAlternateDownloadProvider** interface, in Configuration Manager, defines the interface for an alternative download provider to be invoked by Content Transfer Manager to download packages.  

## Syntax  

```  
[  
    uuid(89F7454D-71F7-4F05-8276-FADC8B85F48D),   
    object,   
    pointer_default(unique)   
]  

```  

## Methods  
 The **ICcmAlternateDownloadProvider** interface defines the following methods.  

|||  
|-|-|  
|[ICcmAlternatedownloadProvider : CancelJob Method](../../../../../develop/reference/core/servers/configure/iccmalternatedownloadprovider---canceljob-method.md)|Cancels a job.|  
|[ICcmAlternatedownloadProvider : DownloadContent Method](../../../../../develop/reference/core/servers/configure/iccmalternatedownloadprovider---downloadcontent-method.md)|Instructs the provider to download content.|  
|[ICcmAlternatedownloadProvider : ModifyJobSource Method](../../../../../develop/reference/core/servers/configure/iccmalternatedownloadprovider---modifyjobsource-method.md)|Instructs the provider to modify the source location for a given job.|  
|[ICcmAlternatedownloadProvider : ModifyJobPriority Method](../../../../../develop/reference/core/servers/configure/iccmalternatedownloadprovider---modifyjobpriority-method.md)|Instructs the provider to modify the priority for a given job.|  
|[ICcmAlternatedownloadProvider : ModifyJobTimeout Method](../../../../../develop/reference/core/servers/configure/iccmalternatedownloadprovider---modifyjobtimeout-method.md)|Instructs the provider to modify the timeout for a given job.|  
|[ICcmAlternatedownloadProvider : Resume Method](../../../../../develop/reference/core/servers/configure/iccmalternatedownloadprovider---resume-method.md)|Instructs the provider to resume a given job.|  
|[ICcmAlternatedownloadProvider : Suspend Method](../../../../../develop/reference/core/servers/configure/iccmalternatedownloadprovider---suspend-method.md)|Suspends a given job.|  

## Remarks  
 ISVs should implement this interface and create an instance of local CCM_DownloadProvider policy that corresponds to their implementation.  

> [!IMPORTANT]
>  This interface must be implemented out-of-process from ccmexec.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  

## See Also  
 [Configuration Manager Alternate Content Provider](../../../../../develop/reference/core/servers/configure/alternate-content-provider-classes.md)
