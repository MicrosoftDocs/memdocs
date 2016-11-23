---
title: "ICcmAlternatedownloadProvider : DownloadContent | Microsoft Docs"
ms.custom: ""
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.reviewer: ""
ms.suite: ""
ms.technology:
  - "configmgr-other"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to:
  - "System Center Configuration Manager (current branch)"
ms.assetid: e3c904db-2838-47e2-ad60-68411e262778
caps.latest.revision: 10
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# ICcmAlternatedownloadProvider : DownloadContent Method
The **ICcmAlternateDownloadProvider::DownloadContent** method, in Configuration Manager, instructs the provider to download content.  

## Syntax  

```  
HRESULT DownloadContent(  
            LPCWSTR szContentId,   
            LPCWSTR szContentVersion,   
            LPCWSTR szRemotePath,   
            LPCWSTR szLocalPath,   
            LPCWSTR szNotifyEndpoint,   
            LPCWSTR szNotifyData,   
            CCM_DTS_PRIORITY Priority,   
            DWORD dwTimeoutSeconds,   
            DWORD dwChunkSize,   
            DWORD dwFlags,   
            LPCWSTR szLocationOptions,   
            LPCWSTR szFileManifest,   
            LPCWSTR szOwnerSID,   
            BOOL bDeleteJobOnError,   
            LPCWSTR szProviderData,   
            LPCWSTR szPackageData,   
            GUID *pJobID  
        );  

```  

#### Parameters  
 `szContentId`  
 Data type: `LPCWSTR`  

 Qualifiers: [in]  

 The content/package ID to download.  

 `szContentVersion`  
 Data type: `LPCWSTR`  

 Qualifiers: [in]  

 The content/package version to download.  

 `szRemotePath`  
 Data type: `LPCWSTR`  

 Qualifiers: [in]  

 A hint on where to download the content. The provider is free to ignore this and download using its own mechanisms.  

 `szLocalPath`  
 Data type: `LPCWSTR`  

 Qualifiers: [in]  

 The directory to which the content should be downloaded. This directory should already exist on this call, and the provider should not change any ACLs on the directory itself for any reason.  

 `szNotifyEndpoint`  
 Data type: `LPCWSTR`  

 Qualifiers: [in]  

 Endpoint to be used for notifying Content Transfer Manager. This should be passed verbatim into calls to SendNotify*ToCTM.  

 `szNotifyData`  
 Data type: `LPCWSTR`  

 Qualifiers: [in]  

 Notification data specified by Content Transfer Manager This should be passed verbatim into calls to SendNotify*ToCTM  

 `Priority`  
 Data type: `CCM_DTS_PRIORITY`  

 Qualifiers: [in]  

 The priority for the job. See notes on CCM_DTS_PRIORITY.  

 `dwTimeoutSeconds`  
 Data type: `DWORD`  

 Qualifiers: [in]  

 The timeout for the job. If the timeout is reached, the job should report an error through SendNotifyErrorToCTM.  

 `dwChunkSize`  
 Data type: `DWORD`  

 Qualifiers: [in]  

 The chunk size to use for notification. If progress notifications have been requested, Content Transfer Manager should be notified every dwChunkSize bytes.  

 `dwFlags`  
 Data type: `DWORD`  

 Qualifiers: [in]  

 Flags for the job. This corresponds to an OR of CCM_DTS_FLAG values.  

 `szLocationOptions`  
 Data type: `LPCWSTR`  

 Qualifiers: [in]  

 Reserved. Alternate providers should ignore this.  

 `szFileManifest`  
 Data type: `LPCWSTR`  

 Qualifiers: [in, unique]  

 Reserved. Alternate providers should ignore this.  

 `szOwnerSID`  
 Data type: `LPCWSTR`  

 Qualifiers: [in]  

 The user context in which the download should be performed.  

 `bDeleteJobOnError`  
 Data type: `BOOL`  

 Qualifiers: [in]  

 Indicates whether or not a job should immediately fail due to a transient error condition. If this is false, then transient errors should simply cause the provider to internally retry unless the job times out or is instructed otherwise by Content Transfer Manager.  

 `szProviderData`  
 Data type: `LPCWSTR`  

 Qualifiers: [in]  

 The provider-specific data specified in the CCM_DownloadProvider policy. This will be an empty string, if data was not specified.  

 `szPackageData`  
 Data type: `LPCWSTR`  

 Qualifiers: [in]  

 The package-specific data specified server-side, wrapped in a \<Data> XML element. This will be an empty string if data was not specified.  

 `*pJobID`  
 Data type: `GUID`  

 Qualifiers: [out]  

 The job ID which should be used for reference on subsequent calls.  

## Return Values  
 An `HRESULT` code. Possible values include, but are not limited to, the following:  

 S_OK  
 Success implies that discovery was triggered successfully. All other return values indicate failure.  

## Remarks  

> [!NOTE]
>  If the provider cannot handle the request for any reason, it should return an error.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client runtime requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client development requirements.md).
