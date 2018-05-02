---
title: "ICcmAlternateDownloadProvider : DownloadContent"
titleSuffix: "Configuration Manager"
ms.date: "07/25/2017"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: e3c904db-2838-47e2-ad60-68411e262778
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# ICcmAlternateDownloadProvider : DownloadContent Method
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

 The directory to which the content should be downloaded. This directory should already exist on this call, and the provider should not change any ACLs on the directory itself for any reason. When szManifest is `null`, this parameter should be ignored.  

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

 Either `null` or XML data representing file byte ranges to be downloaded from the destination.  See **Remarks** below.

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

Starting with version 1702, Configuration Manager integrates with Microsoft Office 365 click-to-run, which supports incremental download.  Alternate content providers should be updated to implement byte range download capabilities.  Byte range information is specified in an XML manifest specified in the **szFileManifest** parameter.

The manifest XML uses the following schema:

``` xml
<?xml version="1.0" encoding="utf-8"?> 
<xs:schema elementFormDefault="qualified" xmlns:xs="http://www.w3.org/2001/XMLSchema">
  <xs:element name="DTSManifest">
    <xs:complexType>
      <xs:sequence>
        <xs:element maxOccurs="200" minOccurs="1" name="File">
          <xs:complexType>
            <xs:sequence>
              <xs:element maxOccurs="500" minOccurs="0" name="Chunk">
                <xs:complexType>
                  <xs:attribute name="Length" type="xs:unsignedInt" use="required" />
                  <xs:attribute name="Offset" type="xs:unsignedInt" use="required" />
                </xs:complexType>
              </xs:element>
            </xs:sequence>
            <xs:attribute name="Destination" type="xs:string" use="required" />
            <xs:attribute name="Source" type="xs:string" use="required" />
          </xs:complexType>
        </xs:element>
      </xs:sequence>
      <xs:attribute name="Version" type="xs:unsignedByte" use="required" />
    </xs:complexType>
  </xs:element>
</xs:schema> 
```

The following example shows a manifest that downloads three files:

``` xml
<?xml version="1.0"?> 
<DTSManifest Version="1">
  <File Destination="C:\Prod\stream.dat" Source="Office/Data/6366.2036/stream.dat">
     <Chunk Length="43491" Offset="59247735"/>
     <Chunk Length="267118" Offset="69247735"/>
  </File>
  <File Destination="C:\Prod\s320.cab" Source="Office/Data/6366.2036/320.cab">
     <Chunk Length="512" Offset="50"/> 
  </File>
  <File Destination="C:\Prod\s640.cab" Source="Office/Data/16.0.6366.2036/s640.cab"/>
</DTSManifest> 
```

When processing the manifest, remember:

- There will be one or more `<file`> elements.
- If a `<file>` element contains `<chunk>` elements, each `<chunk>` specifies the length and byte offset of an incremental download.  
- If no `<chunk>` elements are specified, the entire file should be downloaded.

Should an alternate content provider fail to support incremental downloads, Configuration Manager automatically uses distribution points to download Office 365 content.  For other download scenarios, however, the alternate content provider works without additional impact.

> [!NOTE]
>  If the provider cannot handle the request for any reason, it should return an error.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).
