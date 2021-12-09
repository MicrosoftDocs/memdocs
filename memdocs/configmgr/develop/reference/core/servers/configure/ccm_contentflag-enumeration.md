---
title: "CCM_CONTENTFLAG Enumeration"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 759cd7fa-2980-4b1a-905a-1bb1a21402af
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# CCM_CONTENTFLAG Enumeration
The **CCM_CONTENTFLAG** enumeration contains options for transferring content.  

## Syntax  

```vb  
typedef enum  
{  
    CCM_CONTENTFLAG_LOCAL_ONLY                  = 0x00000001,   
    CCM_CONTENTFLAG_REMOTE_ONLY                 = 0x00000002,   
    CCM_CONTENTFLAG_LOCAL_OR_REMOTE             = 0x00000004,   
    CCM_CONTENTFLAG_PROTECTED_ONLY              = 0x00000008,   
    CCM_CONTENTFLAG_ALLOW_CACHING               = 0x00000010,   
    CCM_CONTENTFLAG_PEERDP                      = 0x00000020,   
    CCM_CONTENTFLAG_REMOTE_NOLOCALPEERDP        = 0x00000040,   
    CCM_CONTENTFLAG_DELTA_DOWNLOAD              = 0x00000080,   
    CCM_CONTENTFLAG_ALLOW_ALTERNATE_PROVIDERS   = 0x00000100  
}  
CCM_CONTENTFLAG;   
```  

## Members  

|Content flag|Description|  
|-|-|  
|CCM_CONTENTFLAG_LOCAL_ONLY|Local only.|  
|CCM_CONTENTFLAG_REMOTE_ONLY|Remote only.|  
|CCM_CONTENTFLAG_LOCAL_OR_REMOTE|Local or remote.|  
|CCM_CONTENTFLAG_PROTECTED_ONLY|Protected only.|  
|CCM_CONTENTFLAG_ALLOW_CACHING|Allow caching.|  
|CCM_CONTENTFLAG_PEERDP|Branch distribution point.|  
|CCM_CONTENTFLAG_REMOTE_NOLOCALPEERDP|No local branch distribution point.|  
|CCM_CONTENTFLAG_DELTA_DOWNLOAD|Delta download.|  
|CCM_CONTENTFLAG_ALLOW_ALTERNATE_PROVIDERS|Allow alternate providers.|  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  
