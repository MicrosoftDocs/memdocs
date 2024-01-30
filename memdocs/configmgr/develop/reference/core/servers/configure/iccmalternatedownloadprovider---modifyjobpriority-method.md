---
title: "ICcmAlternateDownloadProvider : ModifyJobPriority"
titleSuffix: Configuration Manager
description: A method that tells the provider to modify the priority for a given job.
ms.date: 07/25/2017
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: a9dd8eee-87cc-48cd-b59f-6424d3e6dc4a
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
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
 An `HRESULT` code. Possible values include, but aren't limited to, the following one:  

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
