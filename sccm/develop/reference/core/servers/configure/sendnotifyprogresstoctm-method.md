---
title: "SendNotifyProgressToCTM Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 4adf2263-faa3-444b-b331-bb5ca4acfb4d
author: aczechowski
ms.author: aaroncz
manager: dougeby
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

## Remarks  
 If the totals are not yet known, pass 0 for the values. Once the provider has determined the total byte and file count, those values should be used.  

## Return Values  
 An `HRESULT` code. Possible values include, but are not limited to, the following:  

 S_OK  
 Success implies that discovery was triggered successfully. All other return values indicate failure.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  

## See Also  
 [Configuration Manager Alternate Content Provider](../../../../../develop/reference/core/servers/configure/alternate-content-provider-classes.md)
