---
title: "ICcmContentTransferManager4 Interface"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 0f3ed538-ef76-4549-96da-3b5182908e7c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# ICcmContentTransferManager4 Interface
The **ICcmContentTransferManager4** interface is used by clients to invoke the Content Transfer Manager.  

## Syntax  

```  
[  
    uuid(4712C69C-F3A1-4DC0-B894-AFFA08738CD2),   
    object,   
    pointer_default(unique)   
]   
interface ICcmContentTransferManager4 : IUnknown  
{  
    HRESULT DownloadContentEx3(  
             LPCWSTR szContentId,   
             LPCWSTR szContentVersion,   
             CCM_CONTENTTYPE eContentType,   
             CCM_CONTENTPRIORITY Priority,   
             DWORD dwDTSFlags,   
             DWORD dwFlags,   
             LPCWSTR szOriginalPath,   
             LPCWSTR szTempPath  
             LPCWSTR szDestPath,   
             LPCWSTR szMetaDestPath,   
             REFGUID NotifyClsId,   
             DWORD dwNotifyKBytes,   
             LPCWSTR szOwnerSID,   
             DWORD dwLocationTimeout,   
             DWORD dwDownloadTimeout,   
             DWORD dwPerDPInactivityTimeout,   
             DWORD dwTotalInactivityTimeout,   
             LPCWSTR szSignatureHash,   
             DWORD dwMaxChunkBatchSize,   
             LPCWSTR szAltProvSettings,   
             GUID *pJobID  
        );   
}  

```  

#### Parameters  
 `szContentId`  
 Data type: LPCWSTR  

 Qualifiers: [in]  

 The content/package ID to download.  

 `szContentVersion`  
 Data type: LPCWSTR  

 Qualifiers: [in]  

 The content/package version to download.  

 `eContentType`  
 Data type: CCM_CONTENTTYPE  

 Qualifiers: [in]  

 The type of content.

 `Priority`  
 Data type: CCM_CONTENTPRIORITY  

 Qualifiers: [in]  

 The content priority.

 `dwDTSFlags`  
 Data type: DWORD  

 Qualifiers: [in]  

 See the CCM_DTS_FLAG enumeration.  

 `dwFlags`  
 Data type: DWORD  

 Qualifiers: [in]  

 See the CCM_CONTENTFLAG enumeration.  

 `szOriginalPath`  
 Data type: LPCWSTR  

 Qualifiers: [in, unique]  

 The previous source directory, may be NULL.  

 `szTempPath`  
 Data type: LPCWSTR  

 Qualifiers: [in, unique]  

 The temporary work directory, may be NULL.  

 `szDestPath`  
 Data type: LPCWSTR  

 Qualifiers: [in]  

 The destination directory.  

 `szMetaDestPath`  
 Data type: LPCWSTR  

 Qualifiers: [in, unique]  

 The destination directory for metadata.  

 `NotifyClsId`  
 Data type: REFGUID  

 Qualifiers: [in]  

 The notification handler CLSID.  

 `dwNotifyKBytes`  
 Data type: DWORD  

 Qualifiers: [in]  

 dwNotifyKBytes

 `szOwnerSID`  
 Data type: LPCWSTR  

 Qualifiers: [in]  

 The user context in which the download should be performed.  

 `dwLocationTimeout`  
 Data type: DWORD  

 Qualifiers: [in]  

 The location request timeout in seconds.  

 `dwDownloadTimeout`  
 Data type: DWORD  

 Qualifiers: [in]  

 The download request timeout in seconds.  

 `dwPerDPInactivityTimeout`  
 Data type: DWORD  

 Qualifiers: [in]  

 The download inactivity timeout per distribution point in seconds.  

 `dwTotalInactivityTimeout`  
 Data type: DWORD  

 Qualifiers: [in]  

 The total download inactivity timeout in seconds.  

 `szSignatureHash`  
 Data type: LPCWSTR  

 Qualifiers: [in, unique]  

 The hexadecimal encoded hash of signature file for delta download, may be NULL.  

 `dwMaxChunkBatchSize`  
 Data type: DWORD  

 Qualifiers: [in]  

 The maximum number of chunks to download at once.  

 `szAltProvSettings`  
 Data type: LPCWSTR  

 Qualifiers: [in, unique]  

 The XML used to describe allowed alternate download providers and settings for each, may be NULL.  

```  
<AlternateDownloadSettings SchemaVersion="1.0">  
    <Provider Name="logical name here">        <Data>provider specific data here</Data>  
    </Provider>  
    <Provider Name="logical name here">   
        <Data>provider specific data here</Data>  
    </Provider>  
</AlternateDownloadSettings>  

```  

 `*pJobID`  
 Data type: GUID  

 Qualifiers: [in]  

 The job ID which should be used for reference on subsequent calls.  

## Return Values  
 None.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  
