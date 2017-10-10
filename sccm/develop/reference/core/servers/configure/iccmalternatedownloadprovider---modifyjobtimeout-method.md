---
title: "ICcmAlternateDownloadProvider : ModifyJobTimeout"
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
ms.assetid: dec5c5c8-c0b3-400c-835e-08ade5256a30
searchScope:
 - ConfigMgr SDK
caps.latest.revision: 10
author: "lleonard-msft"
ms.author: "alleonar"
manager: "angrobe"
---
# ICcmAlternateDownloadProvider : ModifyJobTimeout Method
The **ICcmAlternateDownloadProvider::ModifyJobTimeout** method, in Configuration Manager, instructs the provider to modify the timeout for a given job.  

## Syntax  

```  
HRESULT ModifyJobTimeout(  
            REFGUID JobID,   
            DWORD dwTimeoutSeconds  
    );  

```  

#### Parameters  
 `JobID`  
 Data type: `REFGUID`  

 Qualifiers: [in]  

 The job on which to take action.  

 `dwTimeoutSeconds`  
 Data type: `DWORD`  

 Qualifiers: [in]  

 The new timeout.  

## Remarks  

> [!NOTE]
>  An error should be returned if the job is not found or if modification of the timeout failed. If the new timeout results in the job immediately timing out, the call should complete and then the provider should notify Content Transfer Manager of the error using SendNotifyErrorToCTM.  

## Return Values  
 An `HRESULT` code. Possible values include, but are not limited to, the following:  

 S_OK  
 Success implies that discovery was triggered successfully. All other return values indicate failure.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).
