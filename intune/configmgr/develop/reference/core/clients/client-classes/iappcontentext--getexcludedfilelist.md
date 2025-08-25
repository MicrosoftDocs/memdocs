---
description: "Learn how to get the excluded file list for application content used to support selective file download with IAppContentExt::GetExcludedFileList method."
title: "IAppContentExt::GetExcludedFileList"
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: cff72c0f-e94e-4047-aa6d-f92c5e9cdcac
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart
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

 The exclude file list is a single string separated by the ':' character. For example, "File1.txt:File2.exe."

 `pbForceFileExclusion`
 Data type: `BOOL`

 Qualifiers: [out]

 `True` to force exclusion of files. If `False`, content framework decides whether or not excluding them based on network condition and content configuration.

## Return Values
 An `HRESULT` code. Possible values include, but aren't limited to, the following one:

 S_OK
 Discovery was triggered successfully. All other return values indicate failure.

## Requirements

## Runtime Requirements
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).

## Development Requirements
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).

## See Also
 [Microsoft.ConfigurationManagement.ApplicationManagement](/previous-versions/)]
 [Configuration Manager Software Development Kit](../../../../../develop/core/misc/system-center-configuration-manager-sdk.md)
 [Configuration Manager Reference](../../../../../develop/reference/configuration-manager-reference.md)
