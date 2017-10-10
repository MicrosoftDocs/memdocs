---
title: "IAppContentExt::GetExcludedFileList"
titleSuffix: "Configuration Manager"
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
ms.assetid: cff72c0f-e94e-4047-aa6d-f92c5e9cdcacsearchScope: - ConfigMgr SDK
caps.latest.revision: 18
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# IAppContentExt::GetExcludedFileList
The `IAppContentExt::GetExcludedFileList` method, in Configuration Manager, gets the excluded file list for application content. This is used to support selective file download.  

## Syntax  

```  
[IDL]  
HRESULT GetExcludedFileList(  
     IWbemClassObject* pHandlerSynclet,  
     LPWSTR* pwszExcludedFileList,  
     BOOL* pbForceFileExclusion  
);  
```  

#### Parameters  
 `*pHandlerSynclet`  
 Data type: `IWbemClassObject`  

 Qualifiers: [in]  

 .   

 `pwszExcludedFileList`  
 Data type: `LPWSTR`  

 Qualifiers: [out]  

 The exclude file list is a single string separated by the ‘:’ character. For example, “File1.txt:File2.exe��?.  

 `pbForceFileExclusion`  
 Data type: `BOOL`  

 Qualifiers: [out]  

 `True` to force exclusion of files. If `False`, content framework will decide whether or not excluding them based on network condition and content configuration.  

## Return Values  
 An `HRESULT` code. Possible values include, but are not limited to, the following:  

 S_OK  
 Discovery was triggered successfully. All other return values indicate failure.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  

## See Also  
 [Microsoft.ConfigurationManagement.ApplicationManagement](https://msdn.microsoft.com/library/microsoft.configurationmanagement.applicationmanagement.aspx)]
 [System Center Configuration Manager Software Development Kit](../../../../../develop/core/misc/system-center-configuration-manager-sdk.md)   
 [Scenario: Extending Application Management](../../../../../develop/apps/scenario--extending-application-management.md)   
 [Configuration Manager Reference](../../../../../develop/reference/configuration-manager-reference.md)
