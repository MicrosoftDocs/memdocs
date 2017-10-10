---
title: "ICcmAlternateDownloadProvider : CancelJob"
titleSuffix: "Configuration Manager"
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
ms.assetid: 51a8436a-a9ef-449f-aaa3-49bd9768bd54
searchScope:
 - ConfigMgr SDK
caps.latest.revision: 12
author: "lleonard-msft"
ms.author: "alleonar"
manager: "angrobe"
---
# ICcmAlternateDownloadProvider : CancelJob Method
The **ICcmAlternateDownloadProvider::CancelJob** method, in Configuration Manager, cancels a job.  

> [!NOTE]
>  An error should be returned if the job is not found or if cancellation failed.  

## Syntax  

```  
HRESULT CancelJob(  
            REFGUID JobID  
    );  

```  

#### Parameters  
 `JobID`  
 Data type: `REFGUID`  

 Qualifiers: [in]  

 The job upon which to take action.  

## Return Values  
 An `HRESULT` code. Possible values include, but are not limited to, the following:  

 S_OK  
 Success implies that discovery was triggered successfully. All other return values indicate failure.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).
