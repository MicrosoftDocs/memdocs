---
title: "ICcmAlternateDownloadProvider : ModifyJobPriority | Microsoft Docs"
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
ms.assetid: a9dd8eee-87cc-48cd-b59f-6424d3e6dc4a
searchScope:
 - ConfigMgr SDK
caps.latest.revision: 10
author: "lleonard-msft"
ms.author: "alleonar"
manager: "angrobe"
---
# ICcmAlternateDownloadProvider : ModifyJobPriority Method
The **ICcmAlternateDownloadProvider::ModifyJobPriority** method, in Configuration Manager, instructs the provider to modify the priority for a given job.  

## Syntax  

```  
HRESULT ModifyJobPriority(  
        [in] REFGUID JobID,   
        [in] CCM_DTS_PRIORITY Priority  
        );  

```  

#### Parameters  
 `JobID`  
 Data type: `REFGUID`  

 Qualifiers: [in]  

 The job on which to take action.  

 `Priority`  
 Data type: `CCM_DTS_PRIORITY`  

 Qualifiers: [in]  

 The new priority.  

## Return Values  
 An `HRESULT` code. Possible values include, but are not limited to, the following:  

 S_OK  
 Success implies that discovery was triggered successfully. All other return values indicate failure.  

## Remarks  

> [!NOTE]
>  An error should be returned if the job is not found or if modification of the priority failed. If any changes are required to make the guarantees described above on the comments on CCM_DTS_PRIORITY, the provider must make them. If the provider cannot honor that guarantee, it should report an error from this function.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).
