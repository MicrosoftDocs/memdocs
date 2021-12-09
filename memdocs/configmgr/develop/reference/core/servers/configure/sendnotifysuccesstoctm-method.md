---
title: "SendNotifySuccessToCTM Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 574ffb2f-b576-473e-b60f-8caf7f635f96
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SendNotifySuccessToCTM Method
The **SendNotifySuccessToCTM** method notifies Content Transfer Manager of the success of a job.  

> [!NOTE]
>  When calling this method, the number of bytes/files transferred (`szBytesTransferred`) should equal the total (`szBytesTotal`).  

## Syntax  

```  
HRESULT stdcall SendNotifySuccessToCTM(  
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

 The client-specific data which was passed into the call to **ICcmAlternateDownloadProvider::DownloadContent** (szNotifyData).  

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

## Return Values  
 An `HRESULT` code. Possible values include, but are not limited to, the following:  

 S_OK  
 Success implies that discovery was triggered successfully. All other return values indicate failure.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  
