---
description: "Learn how to cancel a job in Configuration Manager using ICcmAlternateDownloadProvider::CancelJob method."
title: "ICcmAlternateDownloadProvider : CancelJob"
titleSuffix: Configuration Manager
ms.date: 07/25/2017
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 51a8436a-a9ef-449f-aaa3-49bd9768bd54
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
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
