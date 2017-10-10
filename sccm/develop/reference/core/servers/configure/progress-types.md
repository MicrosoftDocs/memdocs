---
title: "Progress Types"
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
ms.assetid: 671f44e2-a86d-494f-a81e-235400f6db8dsearchScope: - ConfigMgr SDK
caps.latest.revision: 10
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# Progress Types
Progress states for a download.  

> [!NOTE]
>  For a non-status change (for example, if there was just transfer of bytes), specify NULL for progress type.  

## Syntax  

```  
//  Progress types:   
//******************************************************************************  
static const WCHAR S_DTS_PROGRESS_DOWNLOADING_MANIFEST[]    = L"DownloadingManifest";  
static const WCHAR S_DTS_PROGRESS_PROCESSING_MANIFEST[]     = L"ProcessingManifest";  
static const WCHAR S_DTS_PROGRESS_CREATING_DIRECTORIES[]    = L"CreatingDirectories";  
static const WCHAR S_DTS_PROGRESS_PREPARING_DOWNLOAD[]      = L"PreparingDownload";  
static const WCHAR S_DTS_PROGRESS_DOWNLOADING_DATA[]        = L"DownloadingData";  

```  

## Types  

|||  
|-|-|  
|S_DTS_PROGRESS_DOWNLOADING_MANIFEST|Determining list of files to download.|  
|S_DTS_PROGRESS_PROCESSING_MANIFEST|Processing list of files.|  
|S_DTS_PROGRESS_CREATING_DIRECTORIES|Creating subdirectories based on list of files.|  
|S_DTS_PROGRESS_PREPARING_DOWNLOAD|Manifest processing complete, starting download.|  
|S_DTS_PROGRESS_DOWNLOADING_DATA|Downloading files.|  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  

## See Also  
 [Configuration Manager Alternate Content Provider](../../../../../develop/reference/core/servers/configure/alternate-content-provider-classes.md)
