---
title: "ICcmAlternateDownloadProvider : Suspend"
titleSuffix: Configuration Manager
description: "The ICcmAlternateDownloadProvider::Suspend method, in Configuration Manager, instructs the provider to suspend a given job."
ms.date: 07/25/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 5d6ef823-08b2-4e17-8e59-6dfc085f5064
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# ICcmAlternateDownloadProvider : Suspend Method
The **ICcmAlternateDownloadProvider::Suspend** method, in Configuration Manager, instructs the provider to suspend a given job.  

## Syntax  

```  
HRESULT Suspend(  
            REFGUID JobID  
    );  

```  

#### Parameters  
 `JobID`  
 Data type: `REFGUID`  

 Qualifiers: [in]  

 The job on which to take action.  

## Remarks  

> [!NOTE]
>  The provider must support Suspend being called on a job that is suspended. In that case, it should simply do nothing and not report an error. An error should be returned if the job is not found or if suspension failed.  

## Return Values  
 An `HRESULT` code. Possible values include, but aren't limited to, the following one:  

 S_OK  
 Success implies that discovery was triggered successfully. All other return values indicate failure.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).
