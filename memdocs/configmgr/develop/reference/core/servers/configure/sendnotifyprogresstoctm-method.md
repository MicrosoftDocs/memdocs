---
title: SendNotifyProgressToCTM Method
titleSuffix: Configuration Manager
description: The SendNotifyProgressToCTM method notifies Content Transfer Manager of the progress of a job.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 4adf2263-faa3-444b-b331-bb5ca4acfb4d
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SendNotifyProgressToCTM Method
The **SendNotifyProgressToCTM** method notifies Content Transfer Manager of the progress of a job.  

## Syntax  

```  
HRESULT stdcall SendNotifyProgressToCTM(  
    LPCWSTR szProgressType,   
    LPCWSTR szEndpoint,   
    LPCWSTR szID,   
    LPCWSTR szClientData,   
    LPCWSTR szBytesTotal,   
    LPCWSTR szBytesTransferred,   
    ULONG ulFilesTotal,   
    ULONG ulFilesTransferred  
);  

```  

#### Parameters  
 `szProgressType`  
 Data type: LPCWSTR  

 Qualifiers: [in]  

 Either one of the S_DTS_* constants for status changes or NULL/empty string for a bytes progress only.  

 `szEndpoint`  
 Data type: LPCWSTR  

 Qualifiers: [in]  

 The notification endpoint. This was passed into the call to **ICcmAlternateDownloadProvider::DownloadContent** (szNotifyEndpoint).  

 `szID`  
 Data type: UInt32  

 Qualifiers: [in]  

 The job to which the notification corresponds. This is the GUID originally returned by **ICcmAlternateDownloadProvider::DownloadContent**.  

 `szClientData`  
 Data type: LPCWSTR  

 Qualifiers: [in]  

 The client-specific data that was passed into the call to **ICcmAlternateDownloadProvider::DownloadContent** (szNotifyData).  

 `szBytesTotal`  
 Data type: LPCWSTR  

 Qualifiers: [in]  

 The total number of bytes in the job.  

 `szBytesTransferred`  
 Data type: LPCWSTR  

 Qualifiers: [in]  

 The number of bytes transferred so far.  

 `ulFilesTotal`  
 Data type: ULONG  

 Qualifiers: [in]  

 The total number of files in the job.  

 `ulFilesTransferred`  
 Data type: ULONG  

 Qualifiers: [in]  

 The number of files transferred so far.  

## Remarks  
 If the totals aren't yet known, pass 0 for the values. Once the provider has determined the total byte and file count, those values should be used.  

## Return Values  
 An `HRESULT` code. Possible values include, but aren't limited to, the following one:  

 S_OK  
 Success implies that discovery was triggered successfully. All other return values indicate failure.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  
