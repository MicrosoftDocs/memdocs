---
description: Learn how to instruct the provider to modify the source location for a given job in Configuration Manager.
title: "ICcmAlternateDownloadProvider: ModifyJobSource"
titleSuffix: Configuration Manager
ms.date: 07/25/2017
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 13498951-c8f6-437b-91c3-d37acce33d49
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# ICcmAlternateDownloadProvider: ModifyJobSource Method
The **ICcmAlternateDownloadProvider::ModifyJobSource** method, in Configuration Manager, instructs the provider to modify the source location for a given job.  

## Syntax  

```  
HRESULT ModifyJobSource(  
            REFGUID JobID,   
            LPCWSTR szSourceURL,   
            DWORD dwFlags  
    );  

```  

#### Parameters  
 `JobID`  
 Data type: `REFGUID`  

 Qualifiers: [in]  

 The job on which to take action.  

 `szSourceURL`  
 Data type: `LPCWSTR`  

 Qualifiers: [in]  

 The new source location.  

 `dwFlags`  
 Data type: `DWORD`  

 Qualifiers: [in]  

 The new job flags. This can be ignored by alternate providers.  

## Return Values  
 An `HRESULT` code. Possible values include, but are not limited to, the following:  

 S_OK  
 Success implies that discovery was triggered successfully. All other return values indicate failure.  

## Remarks  

> [!NOTE]
>  An error should be returned if the job is not found or if modification of the source location failed or if the provider is using the old location and cannot handle the new location.  
>   
>  If the provider is not using the source location provided in the call to **ICcmAlternateDownloadProvider::DownloadContent** method, it can safely ignore this call, but it should not report an error.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).
